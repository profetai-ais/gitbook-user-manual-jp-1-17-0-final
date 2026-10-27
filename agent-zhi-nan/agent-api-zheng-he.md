---
description: >-
  この章では、外部システムから Agent を呼び出し、権限の確認、会話の継続、添付ファイルの処理、データの管理、トラブルシューティングを行う方法を説明します。実際の作業タスクの順に構成しており、システム連携、開発、運用の担当者を対象としています。
---

# Agent API の連携

このマニュアルでは Agent API の連携手順全体を説明し、外部システムから OpenAI 互換 API を使って Agent を呼び出し、会話を継続し、ファイルを送信し、会話履歴を照会・管理できるようにします。

このマニュアルは次の方を対象としています。

* Agent を既存の製品や企業システムに組み込む必要がある開発者
* API 連携のテスト、受け入れ、運用を担当する方
* Agent の権限、ファイル、会話データの扱いを確認する必要があるシステム管理者

初めて連携する場合は、まず「クイックスタート」に沿って最小限のリクエストを 1 件完了させ、その後、実際の要件に応じて会話の継続、ファイル、エラー時の再試行の仕組みを追加することをおすすめします。

> このマニュアルの `assistant id` は製品の Agent ID を、`thread_id` はシステム内部の session を指します。

## 始める前の準備

### 連携情報の準備

始める前に、システム管理者から次の情報を入手してください。

| 項目           | 説明                    | 例                |
| ------------ | --------------------- | ---------------- |
| システムのホストアドレス | Agent API がデプロイされている環境  | `https://{host}` |
| API Key      | API の呼び出しに使うアクセス認証情報    | `ask_xxx`        |
| Agent ID     | 呼び出す Agent の識別子          | `xxx`            |
| ユーザー ID      | 指定したユーザーとして呼び出す場合に使用   | `user-001`       |

API Key は大切に保管し、フロントエンドのコード、公開ドキュメント、公開されたコードリポジトリに書き込まないでください。

### Base URL の確認

このマニュアルでは、OpenAI 互換 API のパスのプレフィックスを `/v1` と表記します。実際の呼び出し URL は通常次のとおりです。

```
https://{host}/openai/v1
```

たとえば Chat Completions の完全なパスは次のとおりです。

```
https://{host}/openai/v1/chat/completions
```

実際の完全なパスは、デプロイ環境で提供される設定に従ってください。

### 認証方式

すべての `/v1/*` エンドポイントは Bearer Token を使います。Request Header に次を追加してください。

```http
Authorization: Bearer <api_key_plain>
```

よくある認証エラーは次のとおりです。

| HTTP ステータスコード | エラーコード             | 原因                                                    |
| ------------ | ------------------ | ----------------------------------------------------- |
| 401          | `invalid_header`   | `Authorization` Header がない、または形式が Bearer Token ではない |
| 401          | `invalid_api_key`  | API Key が無効                                          |
| 403          | `api_key_disabled` | API Key が無効化されている                                     |

### 対応している API

<table data-search="false"><thead><tr><th>機能</th><th>Method</th><th>Endpoint</th></tr></thead><tbody><tr><td>Agent の利用権限の確認</td><td>GET</td><td><code>/api/public/assistant/permissions/check</code></td></tr><tr><td>Agent の呼び出し</td><td>POST</td><td><code>/v1/chat/completions</code></td></tr><tr><td>会話一覧の照会</td><td>GET</td><td><code>/v1/threads</code></td></tr><tr><td>会話メッセージの照会</td><td>GET</td><td><code>/v1/threads/{thread_id}/messages</code></td></tr><tr><td>会話の削除</td><td>DELETE</td><td><code>/v1/threads/{thread_id}</code></td></tr><tr><td>ファイルのアップロード</td><td>POST</td><td><code>/v1/files</code></td></tr><tr><td>ファイル一覧の照会</td><td>GET</td><td><code>/v1/files</code></td></tr><tr><td>個別ファイルの照会</td><td>GET</td><td><code>/v1/files/{file_id}</code></td></tr><tr><td>ファイルの削除</td><td>DELETE</td><td><code>/v1/files/{file_id}</code></td></tr></tbody></table>

## クイックスタート：初めての Agent との会話

初めて連携する場合は、次の 3 つのステップを順に行うことをおすすめします。

1. API Key、Agent ID、利用権限を確認する
2. 最小限の Chat Completions リクエストを 1 件送信する
3. レスポンスを確認し、`thread_id` を保存する

### ユーザーが Agent の権限を持っているか確認する

外部システムが実際のユーザーの代わりに Agent を呼び出す場合は、そのユーザーが Agent の利用権限を持っているかを先に確認することをおすすめします。

Endpoint：

```http
GET /api/public/assistant/permissions/check
```

Query Parameters：

| パラメーター        | 必須 | 説明      |
| ------------- | -- | ------- |
| `userId`      | はい | ユーザー ID |
| `assistantId` | はい | Agent ID |

リクエストの例：

```
https://{host}/api/public/assistant/permissions/check?userId=user-001&assistantId=xxx
```

権限がある場合、`hasPermission` は `true` を返します。

```json
{
  "resultSet": {
    "hasPermission": true,
    "acl": ["READ"],
    "message": "Permission granted."
  }
}
```

権限がない場合、`hasPermission` は `false` を返します。

```json
{
  "resultSet": {
    "hasPermission": false,
    "acl": [],
    "message": "Permission denied."
  }
}
```

現在、`userId` または `assistantId` が欠けていても、システムが HTTP 200 を返し、内容で権限なしを示すことがあります。

```json
{
  "resultSet": {
    "hasPermission": false,
    "acl": [],
    "message": "Missing userId or assistantId."
  }
}
```

そのため、呼び出しを続けてよいかは HTTP ステータスコードだけでなく、`resultSet.hasPermission` で判断してください。

### 最初のメッセージを送信する

Endpoint：

```http
POST /v1/chat/completions
```

Headers：

```http
Content-Type: application/json
Authorization: Bearer <api_key_plain>
```

最小限の有効なリクエスト：

```bash
curl -X POST "https://{host}/openai/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer ask_xxx" \
  -d '{
    "model": "xxx",
    "messages": [
      {
        "role": "user",
        "content": "こんにちは"
      }
    ],
    "stream": false
  }'
```

この API では、`model` は呼び出す Agent ID を表します。次の 2 つの形式を使えます。

```
xxx
assistant:xxx
```

プレフィックスを付けない Agent ID をそのまま使うことをおすすめします。

```json
{
  "model": "xxx"
}
```

### レスポンスを確認して thread\_id を保存する

成功すると、Agent の回答と今回の会話の `thread_id` が返されます。

```json
{
  "id": "chatcmpl-xxx",
  "object": "chat.completion",
  "created": 1710000000,
  "model": "xxx",
  "thread_id": "thread-abc123",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "..."
      },
      "text": "...",
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 123,
    "completion_tokens": 45,
    "total_tokens": 168
  }
}
```

連携時には次の点を確認してください。

* `choices[0].message.content` に Agent の回答があるか
* `thread_id` が正しく返されているか
* 後で会話を続ける必要がある場合、今回の `thread_id` を保存したか

API が返した `thread_id` はそのままの値で保存し、`thread-` プレフィックスを削除したり独自に追加したりしないことをおすすめします。

## メッセージの送信と会話の継続

### Messages の基本形式

`messages` はメッセージの配列です。最も基本的なテキストメッセージの形式は次のとおりです。

```json
{
  "role": "user",
  "content": "このドキュメントを要約してください"
}
```

`content` は配列形式でも指定できます。

```json
{
  "role": "user",
  "content": [
    {
      "type": "text",
      "text": "添付ファイルの内容を分析してください"
    }
  ]
}
```

対応している `content` の形式：

* 文字列：単一の `text` の内容に変換されます
* 配列：テキストとファイルを同時に含められます
* オブジェクト：要素が 1 つの配列に変換されて処理されます

### メッセージの処理方法

現在、システムは `role` が `user` の最後のメッセージを主なテキスト入力として使います。

そのメッセージの `content` が配列の場合、`type` が `text` のすべての要素を改行でつなげます。それより前のメッセージは、Agent 内部の workflow の履歴として完全には再構築されません。

そのため、連携時は次の原則に従ってください。

* Agent に実際に回答してほしい質問は、最後の user message に入れる
* 文脈を引き継ぐ必要がある場合は、同じ `thread_id` を使う
* 会話を続けるために、履歴全体の messages を再送することだけに頼らない

### 同じ会話を続ける

最初の呼び出しに成功したら、レスポンスの `thread_id` を次のリクエストに含めます。

```json
{
  "model": "xxx",
  "thread_id": "thread-abc123",
  "messages": [
    {
      "role": "user",
      "content": "続けて、前の回答を表にしてください"
    }
  ]
}
```

`thread_id` は次の形式に対応しています。

```
thread-<sessionId>
<sessionId>
```

形式の変換ミスを防ぐため、前回の API が返した値をそのまま使うことをおすすめします。

### 指定したユーザーとして実行する

指定したユーザーの権限で実行するには、リクエストに次を含めます。

```json
{
  "metadata": {
    "user_id": "user-001"
  }
}
```

`metadata.user_id` を使う前に、権限確認 API を呼び出して、そのユーザーが指定した Agent の利用権限を持っていることを確認することをおすすめします。

## Agent にファイルを渡す

Agent にファイルを渡す方法は次の 2 つです。

| 方法                               | 適した場面                                 |
| -------------------------------- | ------------------------------------- |
| 先にファイルをアップロードし、`file_id` で参照する     | 同じファイルを繰り返し使う場合、またはファイルを別途管理する必要がある場合 |
| Chat リクエストで `file_data` を直接送信する | ファイルを 1 回だけ使い、外部システムで Base64 を生成できる場合  |

### 方法 1

#### 先にファイルをアップロードする

Endpoint：

```http
POST /v1/files
```

Content-Type：

```http
multipart/form-data
```

Form Fields：

| フィールド     | 型       | 必須  | 既定値          | 説明           |
| --------- | ------- | --- | ------------ | ------------ |
| `file`    | file    | はい  | -            | アップロードするファイル |
| `purpose` | string  | いいえ | `assistants` | ファイルの用途      |
| `is_temp` | boolean | いいえ | `false`      | 一時ファイルかどうか   |

リクエストの例：

```bash
curl -X POST "https://{host}/openai/v1/files" \
  -H "Authorization: Bearer ask_xxx" \
  -F "file=@demo.pdf" \
  -F "purpose=assistants" \
  -F "is_temp=false"
```

成功時のレスポンス：

```json
{
  "id": "file-abc123",
  "object": "file",
  "bytes": 123,
  "created_at": 1735280000,
  "filename": "demo.pdf",
  "purpose": "assistants",
  "status": "uploaded"
}
```

ファイルをアップロードすると、システムは API Key とファイルを紐づけます。レスポンスの `id` を保存し、後続の Chat リクエストで使用してください。

#### Chat で既存の file\_id を参照する

テキストとファイルを同じ `content` 配列に入れます。

```json
{
  "model": "xxx",
  "messages": [
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "添付ファイルを要約してください"
        },
        {
          "type": "file",
          "file": {
            "filename": "demo.pdf",
            "file_id": "file-abc123"
          }
        }
      ]
    }
  ]
}
```

`file_id` は `file-xxx` 形式と、`file-` プレフィックスなしの形式の両方に対応しています。ファイルアップロード API が返した値をそのまま使うことをおすすめします。

### 方法 2

#### file\_data を直接送信する

`file_data` には Base64 または data URI を使えます。

```json
{
  "model": "xxx",
  "messages": [
    {
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": "このドキュメントを分析してください"
        },
        {
          "type": "file",
          "file": {
            "filename": "demo.txt",
            "file_data": "data:text/plain;base64,SGVsbG8="
          }
        }
      ]
    }
  ]
}
```

data URI を使う場合、システムは `base64,` の後ろの文字列を取り出してデコードします。デコードに成功すると、ファイルは既存のアップロード処理を経て、API Key とファイルが紐づけられます。

### ファイルの権限とセキュリティ上の制限

システムはファイルを Agent の workflow に渡す前に、そのファイルが今回使用している API Key に紐づいているかを確認します。

確認を通過したファイルだけが workflow に渡されます。すべてのファイルが確認を通過しなかった場合、最終的に送られる `fileIds` は `null` になります。

照会したファイルが存在しない場合、またはファイルが現在の API Key に属していない場合、システムは 404 を返します。

```json
{
  "error": {
    "message": "File not found.",
    "type": "invalid_request_error",
    "code": "not_found"
  }
}
```

## ファイルの管理

### ファイル一覧の照会

```http
GET /v1/files
```

レスポンスの形式：

```json
{
  "object": "list",
  "data": []
}
```

### 個別ファイルの照会

```http
GET /v1/files/{file_id}
```

`file_id` は次の形式に対応しています。

```
file-<id>
<id>
```

### ファイルの削除

```http
DELETE /v1/files/{file_id}
```

成功時のレスポンス：

```json
{
  "id": "file-abc123",
  "object": "file",
  "deleted": true
}
```

ファイルを削除する前に、ほかのプロセスや外部システムがそのファイルを共有していないかを確認し、既存の機能に影響しないようにしてください。

## 会話の照会と管理

### 会話一覧の照会

Endpoint：

```http
GET /v1/threads
```

Query Parameters：

| パラメーター  | 型       | 既定値    | 説明    |
| ------- | ------- | ------ | ----- |
| `limit` | integer | 50     | 返す件数  |
| `order` | string  | `desc` | 並び順   |

レスポンスの例：

```json
{
  "object": "list",
  "data": [
    {
      "id": "thread-<sessionId>",
      "object": "thread",
      "created_at": 1735280000,
      "metadata": {},
      "tool_resources": {}
    }
  ]
}
```

> 現在、`order` パラメーターは実際には並び順に反映されません。連携側はこのパラメーターだけに頼ってデータの順序を判断しないでください。

### 会話メッセージの照会

Endpoint：

```http
GET /v1/threads/{thread_id}/messages
```

Query Parameters：

| パラメーター   | 型       | 既定値   | 説明                    |
| -------- | ------- | ----- | --------------------- |
| `order`  | string  | `asc` | 並び順                   |
| `limit`  | integer | 50    | 返す件数                  |
| `after`  | string  | -     | 互換性のために残されていますが、現在は機能しません |
| `before` | string  | -     | 互換性のために残されていますが、現在は機能しません |

レスポンスの例：

```json
{
  "object": "list",
  "data": [
    {
      "id": "<messageId>",
      "object": "thread.message",
      "created_at": 1735280000,
      "role": "user",
      "content": [
        {
          "type": "text",
          "text": {
            "value": "..."
          }
        }
      ],
      "thread_id": "thread-<sessionId>"
    }
  ]
}
```

### 会話の削除

```http
DELETE /v1/threads/{thread_id}
```

成功時のレスポンス：

```json
{
  "deleted": true,
  "thread_id": "thread-<sessionId>"
}
```

## ストリーミングレスポンス

Chat Completions の Request Body には `stream` フィールドがあります。

```json
{
  "stream": true
}
```

現在、仕様書によってストリーミングの動作に関する記述が一致していません。

* ある仕様では、Controller は常に JSON を返すが、`stream` は Service に渡されるとされています。
* 別の説明では、`stream=true` の場合は `text/event-stream` を使い、SSE で chunk と `[DONE]` を送信するとされています。

そのため、逐次表示や SSE の処理を正式に導入する前に、現在のデプロイ環境でストリーミング機能が有効になっているかを確認してください。確認できていない場合は、次の設定を使うことをおすすめします。

```json
{
  "stream": false
}
```

## Rate Limit と再試行の処理

### 残りの呼び出し枠の確認

`POST /v1/chat/completions` が成功すると、Response Header には通常次の情報が含まれます。

```
X-RateLimit-Limit-Requests
X-RateLimit-Remaining-Requests
X-RateLimit-Reset-Requests
```

制限を超えて呼び出すと、システムは HTTP 429 を返し、次の情報を提供します。

```
X-RateLimit-Limit-Requests
X-RateLimit-Remaining-Requests: 0
X-RateLimit-Reset-Requests
Retry-After
```

エラーレスポンスの例：

```json
{
  "error": {
    "message": "Rate limit exceeded. Please retry after <N> seconds.",
    "type": "rate_limit_error",
    "code": "rate_limit_exceeded"
  }
}
```

### 推奨する再試行の方針

| ステータスコード | 推奨する対応                                                        |
| -------- | ------------------------------------------------------------- |
| 401、403  | 自動で再試行しないでください。まず API Key、Bearer の形式、無効化の状態を確認します            |
| 404      | すぐに再試行しないでください。まず `thread_id`、`file_id` と API Key の紐づきを確認します |
| 422      | すぐに再試行しないでください。まず不足している、または形式が誤っている Request Body を修正します     |
| 429      | `Retry-After` に従って待ってから再試行します                                 |
| 500      | エラー内容に応じて回数を限定して再試行し、エラー記録を残します                               |
| 503、504  | 回数を限定した遅延再試行と backoff を行います                                  |

無制限の再試行や、間を置かない連続した再試行は、サービスの負荷を高めるため避けてください。何度再試行しても失敗する場合は、そのプロセスを停止し、機密情報を除いた Request の概要、ステータスコード、エラーコード、発生日時を記録して、後の調査に使えるようにしてください。

## よくあるエラーと対処方法

<table data-search="false"><thead><tr><th>HTTP</th><th>type</th><th>code</th><th>原因と対処の方向性</th></tr></thead><tbody><tr><td>401</td><td><code>invalid_request_error</code></td><td><code>invalid_header</code></td><td><code>Authorization</code> Header があるか、形式が <code>Bearer &#x3C;API Key></code> になっているかを確認します</td></tr><tr><td>401</td><td><code>invalid_request_error</code></td><td><code>invalid_api_key</code></td><td>API Key が正しいかを確認します</td></tr><tr><td>403</td><td><code>invalid_request_error</code></td><td><code>api_key_disabled</code></td><td>管理者に連絡して API Key の状態を確認します</td></tr><tr><td>404</td><td><code>invalid_request_error</code></td><td><code>not_found</code></td><td>thread または file が存在するか、現在の API Key に属しているかを確認します</td></tr><tr><td>422</td><td><code>invalid_request_error</code></td><td><code>invalid_request</code></td><td><code>model</code> などの必須フィールドとデータ形式を確認します</td></tr><tr><td>429</td><td><code>rate_limit_error</code></td><td><code>rate_limit_exceeded</code></td><td><code>Retry-After</code> に従って待ってから再試行します</td></tr><tr><td>429</td><td><code>rate_limit_error</code></td><td><code>controller_throttle</code></td><td>サービスが混雑しています。しばらくしてから再試行します</td></tr><tr><td>429</td><td><code>rate_limit_error</code></td><td><code>chat_throttle_timeout</code></td><td>利用可能な処理枠の待機がタイムアウトしました。しばらくしてから再試行します</td></tr><tr><td>500</td><td><code>server_error</code></td><td><code>workflow_failed</code></td><td>Agent の workflow の実行に失敗しました</td></tr><tr><td>500</td><td><code>server_error</code></td><td><code>cancelled</code></td><td>ジョブがキャンセルされました</td></tr><tr><td>500</td><td><code>server_error</code></td><td><code>chat_failed</code></td><td>Chat の実行に失敗しました</td></tr><tr><td>503</td><td><code>server_error</code></td><td><code>database_busy</code></td><td>データベース接続の使用量が高すぎるか、上限に達しています</td></tr><tr><td>503</td><td><code>server_error</code></td><td><code>database_unavailable</code></td><td>データベースに一時的に接続できません</td></tr><tr><td>503</td><td><code>server_error</code></td><td><code>chat_interrupted</code></td><td>利用可能な処理枠を待っている間に中断されました</td></tr><tr><td>504</td><td><code>server_error</code></td><td><code>database_timeout</code></td><td>データベースの照会がタイムアウトしました</td></tr><tr><td>504</td><td><code>server_error</code></td><td><code>timeout</code></td><td>Request の実行がタイムアウトしました</td></tr></tbody></table>

このほか、個別の説明文書にのみ記載されており、現在のバージョンで正式に実装されているか確認できていないエラーコードもあります。

```
api_key_expired
assistant_disabled
assistant_permission_denied
budget_exceeded
guardrails_blocked
streaming_unavailable
```

正式に確認されるまでは、上記のエラーコードだけに頼って中核となる処理を設計しないことをおすすめします。

## Request と Response のフィールドリファレンス

### Chat Completions Request Body

| フィールド              | 型       | 必須  | 説明                                  |
| ------------------ | ------- | --- | ----------------------------------- |
| `model`            | string  | はい  | Agent ID。`assistant:` プレフィックスに対応     |
| `messages`         | array   | はい  | 今回送信するメッセージ                         |
| `thread_id`        | string  | いいえ | 会話または session の ID。`thread-` プレフィックスに対応 |
| `stream`           | boolean | いいえ | ストリーミングを使うかどうか。使う前に環境の対応状況を確認してください  |
| `tools`            | array   | いいえ | 現在は互換性のためだけに残されており、正式な機能として頼ることはおすすめしません |
| `metadata.user_id` | string  | いいえ | 指定したユーザーの権限で実行する場合に使います              |

### Chat Completions Response

<table data-search="false"><thead><tr><th>フィールド</th><th>型</th><th>説明</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>レスポンス ID。形式は <code>chatcmpl-...</code></td></tr><tr><td><code>object</code></td><td>string</td><td>常に <code>chat.completion</code></td></tr><tr><td><code>created</code></td><td>number</td><td>作成日時。形式は epoch seconds</td></tr><tr><td><code>model</code></td><td>string</td><td>Request の <code>model</code> をそのまま返します</td></tr><tr><td><code>thread_id</code></td><td>string</td><td>今回の会話の ID。形式は <code>thread-...</code></td></tr><tr><td><code>choices</code></td><td>array</td><td>回答の結果。現在は常に choice が 1 件です</td></tr><tr><td><code>usage</code></td><td>object</td><td>Token の統計。システムが取得できた場合に返されます</td></tr></tbody></table>

`choices[0]` のフィールド：

| フィールド             | 説明                                   |
| ----------------- | ------------------------------------ |
| `message.role`    | 常に `assistant`                       |
| `message.content` | Agent の回答テキスト                        |
| `text`            | `message.content` と同じ。旧クライアントとの互換性のため |
| `finish_reason`   | 常に `stop`                            |

## 既知の制限事項

連携する前に、次の制限事項に注意してください。

* `tools` フィールドは現在インターフェースの互換性のためだけに残されており、正式な機能として頼ることはおすすめしません。
* それより前の messages は、Agent 内部の workflow の履歴として完全には反映されません。
* 会話を続ける場合は、同じ `thread_id` を使ってください。
* `GET /v1/threads` の `order` は、現在は実際には並び順に反映されません。
* `GET /v1/threads/{thread_id}/messages` の `after` と `before` は互換性のために残されていますが、現在は機能しません。
* ファイルは workflow に渡される前に API Key との紐づきが確認されます。
* 共有ファイルを削除する前に、影響範囲を外部システム側で判断する必要があります。
* ストリーミングの動作に関する文書の記述が現在一致していないため、導入前にデプロイ環境を確認する必要があります。

## 連携の受け入れチェックリスト

正式にリリースする前に、次の点を順に確認することをおすすめします。

* 正しいホストアドレス、API Key、Agent ID を入手している
* API Key が Bearer Token の認証を正常に通過することを確認している
* 指定したユーザーとして実行する場合、Agent の権限確認を完了している
* `stream=false` の最小限の Chat リクエストが 1 件成功している
* `choices[0].message.content` を正しく読み取れている
* API が返した `thread_id` を保存している
* 同じ `thread_id` で会話の継続を検証している
* 添付ファイルが必要な場合、ファイルのアップロード、`file_id` の参照、API Key との紐づきを検証している
* 429、503、504 に対して、回数を限定した retry と backoff を設計している
* 必要なエラー記録と追跡情報を残している
* SSE が必要な場合、現在の環境が `stream=true` に実際に対応していることを確認している
* thread や file を削除しても、使用中のほかのプロセスに影響しないことを確認している

## よくある質問

<details>

<summary>API が 401 を返すのはなぜですか？</summary>

Request Header に次が含まれているかを確認してください。

```http
Authorization: Bearer <api_key_plain>
```

形式が正しい場合は、API Key が有効かどうかを確認してください。

</details>

<details>

<summary>権限確認が HTTP 200 を返したのに、Agent を利用できないのはなぜですか？</summary>

権限確認 API は、パラメーターが不足している場合や権限がない場合でも HTTP 200 を返すことがあります。`resultSet.hasPermission` の値で判断してください。

</details>

<details>

<summary>messages をすべて渡しているのに、Agent が前の内容を引き継がないのはなぜですか？</summary>

現在、システムは最後の user message を主な入力として使い、それより前のメッセージは workflow の履歴として完全には再構築されません。同じ `thread_id` を保存して渡し、会話を継続してください。

</details>

<details>

<summary>Agent が添付ファイルを読み取らないのはなぜですか？</summary>

次の点を確認してください。

1. `file_id` が正しいか
2. ファイルが現在使用している API Key でアップロードされたものか
3. `content` 内のファイル項目が `type: "file"` を使っているか
4. `file_data` が正しくデコードできる Base64 または data URI か

</details>

<details>

<summary>429 が発生した場合、どのくらい待ってから再試行すればよいですか？</summary>

Response Header の `Retry-After` を読み取り、指定された時間だけ待ってから再試行してください。

</details>

<details>

<summary>stream=true をそのまま有効にしてもよいですか？</summary>

現在、仕様書によってストリーミング対応に関する記述が一致していません。正式に使う前に、デプロイ環境が SSE に対応しているかをシステム管理者に確認してください。確認できていない場合は `stream=false` を使ってください。

</details>
