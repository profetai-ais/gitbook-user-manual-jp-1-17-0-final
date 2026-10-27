# API Key

## 概要

API Key を使うと、専用のキーを作成して、外部システムから AI Studio が提供するオープン API を呼び出せます。API Key があれば、外部プログラム、連携サービス、サードパーティのツールは、アカウントとパスワードでログインしなくても、キーに紐づくユーザーとして API を呼び出せます。ここでは新しい API Key を作成したり、API ドキュメントを開いて利用できる API の仕様を確認したりできます。

各 API Key はそのキーを作成したユーザーに紐づき、システムはそのユーザーの権限に基づいてアクセスできる API の範囲を判断します。

{% hint style="info" %}
API Key の入口は **システム設定 → API Key** にあり、AI Studio 管理者のみが利用できます。AI Studio ドメインユーザーと AI Studio ユーザーは API Key を作成できません。以前の右上のアバターメニューにあった入口は削除されました。
{% endhint %}

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

## API Key の設定

API Key を開いて生成ボタンをクリックすると、キーが生成されます。

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

> 注意：API Key の作成後、キーの全体が表示されるのは 1 回だけです。セキュリティ上の理由から、キーの全体が再び表示されることはなく、元のキーを取り戻すこともできません。キーを紛失した場合は、元のキーを削除してから作成し直してください。\
> 1 人のユーザーが作成できる API Key は最大 1 つです。新しい API Key を生成する場合は、先に既存の API Key を削除してから生成し直してください。

### API Key の管理

API Key を作成すると、自分が作成したすべてのキーを確認できます。キーの安全を守るため、一覧には次のようにマスクされた形式でのみ表示されます。

```
gak_abc*******xyz
```

API Key を無効化または削除すると、外部システムはそのキーで API を呼び出せなくなります。キーに有効期限を設定している場合は、期限が過ぎると自動的に無効になります。

> 注意：フロントエンドのコード、公開された Git リポジトリ、保護されていないドキュメントなど、公開された環境に API Key を置かないでください。API Key が漏えいした疑いがある場合は、すぐにそのキーを無効化または削除し、新しい API Key を作成し直してください。

## API ドキュメント

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

API ドキュメントのブロックで **API ドキュメントを開く** をクリックします。API ドキュメントには利用できる API の仕様が表示され、Swagger UI の画面で API のパス、パラメーター、テストリクエストを確認できます。

> 注意：一部の API ではナレッジベースの識別子（`kbId`）またはデータセットの識別子（`datasetId`）の指定が必要です。これらの識別子は、対象の項目の編集ウィンドウで確認・コピーできます。詳しくは [ナレッジベースの管理－ナレッジベース ID の確認とコピー](../zhi-shi-ku-zhi-nan/guan-li-zhi-shi-ku.md#cha-kan-yu-fu-zhi-zhi-shi-ku-id) を参照してください。

## 利用履歴

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

利用履歴タブに切り替えると、API Key の利用履歴を確認できます。利用履歴を使うと、外部システムの呼び出し状況を追跡し、異常なリクエストがないかを確認できます。日付の範囲を指定して、特定の期間の API の呼び出し履歴を照会することもできます。
