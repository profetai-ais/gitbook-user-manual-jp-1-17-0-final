# ワークフローのノード

## 概要

ワークフローには多様なノードが用意されており、柔軟でインテリジェントな、モジュール化された Agent を構築できます。各ノードは、システムのロジック、ユーザーとのやり取り、バックエンドとの連携において、それぞれ異なる役割を担います。

<figure><img src="../.gitbook/assets/image (764).png" alt=""><figcaption></figcaption></figure>

<table data-search="false"><thead><tr><th width="80">項目</th><th width="160">ノード名</th><th>ワークフローでの用途</th></tr></thead><tbody><tr><td>1</td><td>知識</td><td>社内のナレッジベースやドキュメントデータベースから関連情報を検索します。</td></tr><tr><td>2</td><td>LLM</td><td>言語モデル（GPT-5.2 Thinking／GPT-5.2 Instant／Gemini 3 など）でプロンプトを実行し、現在の入力に基づいて生成や推論を行います。</td></tr><tr><td>3</td><td>応答</td><td>ユーザーに実際に表示される内容を定義し、Agent の回答を出力・表示します。</td></tr><tr><td>4</td><td>注釈</td><td>キャンバスに内部用の注釈やメモを追加します。実際のロジックとは接続されません。</td></tr><tr><td>5</td><td>変数</td><td>前のステップの値を取得・保存・変換し、後続のノードで使えるようにします。</td></tr><tr><td>6</td><td>人による入力</td><td>ユーザーの選択を待ち、選ばれた操作に応じて対応する分岐を実行します。</td></tr><tr><td>7</td><td>ガードレール</td><td>フローの中で内容をチェック・制限し、個人データの漏えい、情報セキュリティ、コンプライアンスのリスクを低減して、出力を利用ルールと管理要件に沿ったものにします。</td></tr><tr><td>8</td><td>分類</td><td>あらかじめ定義したロジックやモデルによる分類に基づいて、入力にラベルを付けたり経路を振り分けたりします。</td></tr><tr><td>9</td><td>フォーク</td><td>ノード間のデータの流れと順序を定義し、タスクを自動実行できるようにします。</td></tr><tr><td>10</td><td>マージ</td><td>複数の分岐の出力を 1 つのノードにまとめ、後続のノードにまとめて渡します。</td></tr></tbody></table>

## **知識**

社内のナレッジベースやドキュメントデータベースから関連情報を検索します。

<div align="center" data-with-frame="true"><figure><img src="../.gitbook/assets/image (140).png" alt="" width="375"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>ナレッジ検索</td><td>Input の内容（「/」を入力して query を選択するとユーザーの質問になります）</td></tr><tr><td>2</td><td>ナレッジベースの参照</td><td>必要なナレッジベースを選択します</td></tr><tr><td>3</td><td>検索パラメーター</td><td>「ナレッジベースのテスト - 検索パラメーターの設定」を参照してください</td></tr></tbody></table>

## **LLM**

言語モデル（GPT-5.2 Thinking／GPT-5.2 Instant／Gemini 3 など）でプロンプトを実行し、現在の入力に基づいて生成や推論を行います。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (141).png" alt="" width="188"><figcaption></figcaption></figure></div>

<table data-search="false"><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>LLM 名</td><td>識別しやすいようにノード名を入力します</td></tr><tr><td>2</td><td>LLM パラメーターの調整</td><td>パラメーターを参照してください</td></tr><tr><td>3</td><td>モデル</td><td>ノードが使用する言語モデルを変更します（2 のモデル設定と同じです）</td></tr><tr><td>4</td><td>コンテキスト</td><td>Input の内容（「/」を入力して query を選択するとユーザーの質問になります）</td></tr><tr><td>5</td><td>ノードのファイルを使用</td><td>LLM が前のノードからどのファイルを取得できるかを設定します</td></tr><tr><td>6</td><td>ファイル処理</td><td>ファイル処理を参照してください</td></tr><tr><td>7</td><td>ナレッジベースを有効化</td><td>ナレッジベースのソースを参照してください</td></tr><tr><td>8</td><td>Coordination</td><td>Coordination を参照してください</td></tr><tr><td>9</td><td>スキル</td><td>スキルを参照してください</td></tr><tr><td>10</td><td>メモリーの参照</td><td>有効にすると、LLM が回答時にメモリーストアのメモリーを参照します。メモリーの保存方法は Agent Memory を参照してください</td></tr><tr><td>11</td><td>会話メモリー</td><td>パラメーター内の会話メモリーを参照してください</td></tr><tr><td>12</td><td>ツール</td><td>ツールを参照してください</td></tr></tbody></table>

## **応答**

応答ノード（Response Node）は **Agent の最終的な出力内容** を定義するノードで、フローの中でまとめた結果をユーザーに返したり、後続のシステム出力の応答として返したりします。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (142).png" alt="" width="246"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>ノード名</td><td>識別しやすいようにノード名を入力します</td></tr><tr><td>2</td><td>説明</td><td>このノードの用途を記入できます</td></tr><tr><td>3</td><td>変数の設定</td><td>/ を入力して変数を設定します</td></tr></tbody></table>

## **注釈**

キャンバスに内部用の注釈やメモを追加します。実際のロジックとは接続されません。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (143).png" alt="" width="249"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>ノード名</td><td>識別しやすいようにノード名を入力します</td></tr><tr><td>2</td><td>メモ</td><td>後から識別できるようにメモの内容を入力します</td></tr></tbody></table>

## **変数**

前のステップの値を取得・保存・変換し、後続のノードで使えるようにします。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (144).png" alt="" width="375"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="200">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>変数（グローバル変数名）</td><td>書き込む<strong>グローバル変数のキー</strong>（例：<code>global.age</code>）を選択・指定し、後続のノードで同じ名前で読み取り・参照できるようにします。</td></tr><tr><td>2</td><td>変数の内容（変数の値）</td><td>そのグローバル変数の<strong>実際の値（Value）</strong>を設定し、後続のノードで直接利用できるようにします。</td></tr></tbody></table>

## ガードレール

フローの中で内容をチェック・制限し、設定に応じてブロックまたはマスクを行って、個人データの漏えい、情報セキュリティ、コンテンツのコンプライアンスのリスクを低減します。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (145).png" alt="" width="375"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>変数の設定</td><td>/ を入力して変数を設定します</td></tr><tr><td>2</td><td>ブロック／マスク</td><td>ガードレールの動作モードを選択します</td></tr><tr><td>3</td><td>カテゴリ</td><td>種類ごとにブロック／マスクする内容を選択します</td></tr></tbody></table>

## **分類**

あらかじめ定義したロジックやモデルによる分類に基づいて、入力にラベルを付けたり経路を振り分けたりします。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (146).png" alt="" width="375"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>モデル</td><td>ノードが使用する言語モデルを変更します</td></tr><tr><td>2</td><td>コンテキスト</td><td>Input の内容（「/」を入力して query を選択するとユーザーの質問になります）</td></tr><tr><td>3</td><td>カテゴリ</td><td>質問を分類します。ノードに既定のカテゴリはなくなったため、必要に応じてカテゴリを追加してください</td></tr></tbody></table>

> 分類ノードを含む既存のワークフローを開くと、元の「デフォルト」カテゴリは自動的に「その他」に変更されます。保存すると新しい形式で保存されます。接続済みの分岐には影響しません。

## フォーク

ノード間のデータの流れと順序を定義し、タスクを自動実行できるようにします。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (147).png" alt="" width="375"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>分岐</td><td>現在の分岐の数を確認します</td></tr><tr><td>2</td><td>分岐の状態</td><td>現在の分岐の状態を確認します</td></tr></tbody></table>

## マージ

複数の分岐の出力を 1 つのノードにまとめ、後続のノードにまとめて渡します。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/image (148).png" alt="" width="375"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>待機</td><td>待機中のノードの数を確認します</td></tr><tr><td>2</td><td>入力の状態</td><td>現在の入力の状態を確認します</td></tr><tr><td>3</td><td>待機のタイムアウト</td><td>待機のタイムアウトを設定します</td></tr></tbody></table>

## **人による入力**

フローを一時停止してメッセージと操作ボタンを表示し、ユーザーの選択を待ってから、選ばれた操作に対応する分岐を実行します。ほかの人に確認を依頼することもでき、上長や担当者の承認を得てから続行するフローに適しています。

<div data-with-frame="true"><figure><img src="../.gitbook/assets/Frame 343.png" alt="" width="300"><figcaption></figcaption></figure></div>

<table><thead><tr><th width="80">項目</th><th width="160">機能名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>メッセージ</td><td>回答者に表示するメッセージです。/ を入力して変数を設定します。各操作の補足説明もここに記載してください</td></tr><tr><td>2</td><td>ユーザーの操作</td><td>選択できる操作を設定します。各操作に入力する値は 1 つだけで（100 文字まで）、ボタンに表示されると同時に分岐の判定にも使われます。少なくとも 1 つの操作が必要です</td></tr><tr><td>3</td><td>確認者</td><td>回答する人を選択します。フローは確認者の回答を待ってから続行します：<br>• <strong>現在のユーザー</strong>：この会話で Agent とやり取りしているユーザーが回答します<br>• <strong>指定ユーザー</strong>：Agent とやり取りしているユーザーにかかわらず、選択したユーザーが回答します。確認者を 1 人選択する必要があり、自分またはほかの人を選択できます</td></tr><tr><td>4</td><td>通知</td><td>システム通知はデフォルトでオンになっており、オフにすることはできません。フローが回答待ちになると確認者に通知されます。メール通知を選択すると、メールでも確認者に通知されます</td></tr><tr><td>5</td><td>タイムアウト</td><td>待機時間と単位（秒、分、時間、日）を設定します。期限内に回答がない場合、フローはタイムアウトの出口から続行します</td></tr></tbody></table>

{% hint style="info" %}
操作のテキストはそのままボタンに表示されるため、1〜2 行程度の短く分かりやすい表現にしてください。ボタンにはマウスオーバー時の説明が表示されないため、各操作の意味を説明する必要がある場合は「メッセージ」に記載してください。
{% endhint %}

ユーザーの操作ごとにノード上に対応する出口が作成され、さらに **タイムアウト** の出口が 1 つ必ずあります。ワークフローを保存するには、すべての出口を後続のノードに接続する必要があります。

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

後続のノードで / を入力して「ノード名.{selected}」を選ぶと、ユーザーが選んだ操作の値を取得できます。フローがタイムアウトの出口から続行した場合、この値は空になります。

### 回答する人

「確認者」の設定によって、人による入力ノードに回答する人が決まります。どちらを選択した場合も、フローが回答待ちになるとシステム通知で確認者に知らせます。

<table><thead><tr><th width="240">設定</th><th>回答方法</th></tr></thead><tbody><tr><td>現在のユーザー</td><td>Agent と会話しているユーザーが回答します。会話内のカードで直接回答するか、通知から回答できます</td></tr><tr><td>指定ユーザー（確認者が会話中のユーザー本人の場合）</td><td>会話内のカードで直接回答するか、通知から回答できます</td></tr><tr><td>指定ユーザー（確認者が会話中のユーザー以外の場合）</td><td>カードに「○○ の回答を待っています」と表示されます。会話中のユーザーは回答できず、確認者が通知から回答するのを待つ必要があります</td></tr></tbody></table>

「指定ユーザー」を選択した場合、誰が Agent と会話していても、同じ確認者が回答します。たとえば確認者を上長に設定すると、誰がこのノードを実行しても、上長が確認するまでフローは続行しません。

確認者は Agent の権限がなくても回答できます。権限のない確認者も、システム通知やメールで操作をクリックして回答できますが、会話に戻ることはできません。

### 会話内のカード

フローが人による入力ノードに到達すると、会話にメッセージ、操作ボタン、期限が表示されたカードが表示されます。回答すると、フローは選ばれた操作の出口から続行します。

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>人による入力ノードのトリガー</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>人による入力ノードのタイムアウト</p></figcaption></figure>

* 回答待ちの間は、回答が完了するまで同じ会話で新しいメッセージを送信できません。
* カードの状態には「回答待ち」「回答済み」「タイムアウト済み」「キャンセル済み」があります。確認者が指定されている場合、待機中のカードには「（確認者名） の回答待ち」と表示されます。回答済みでフローがまだ続行していない場合、カードには「待機中」と表示されます。ステータスラベルは省略されずにすべて表示されます。
* 会話を開き直しても待機中のカードは残っており、続けて回答できます。
* 待機中に回答を停止すると、カードはキャンセル済みと表示され、フローは続行しません。
* 確認者はシステム通知上で操作をクリックして直接回答するか、「会話に戻る」をクリックして元の会話で回答できます。回答後は通知上の操作ボタンが折りたたまれ、タイムアウトまたはキャンセル後は通知上の操作ボタンをクリックできなくなります。通知の表示については[システム通知](../ping-tai-zhi-nan/xi-tong-tong-zhi.md)を参照してください。
* メール通知を選択している場合、確認者はメール内で直接回答することもできます。下記の「メール通知」を参照してください。
* Coordination 経由で人による入力ノードを含むワークフロー Agent を呼び出すことには、現在対応していません。

### メール通知

メール通知を選択すると、フローが回答待ちになったときに、確認者に Profet AI AIS（ais@profetai.com）からメールが届きます。AIS を開かなくても、メール内で操作を選んで回答できます。

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>人による入力ノードのメール通知</p></figcaption></figure>

メールには次の内容が含まれます：

<table><thead><tr><th width="160">項目</th><th>説明</th></tr></thead><tbody><tr><td>件名</td><td>送信元の Agent と「Your response is needed」に続けて、確認が必要な内容が表示されます</td></tr><tr><td>本文</td><td>Agent 名、確認が必要な内容、ノードで設定したメッセージが表示されます</td></tr><tr><td>回答期限</td><td>「有効期限」の後に回答期限が表示されます。現在は UTC で表示されます。期限を過ぎると、フローはタイムアウトの出口から続行します</td></tr><tr><td>操作ボタン</td><td>ノードで設定したユーザーの操作と同じです。クリックすると回答が送信されます</td></tr></tbody></table>

操作方法：

1. メールを開き、確認が必要な内容と回答期限を確認します。
2. メール内の操作ボタンのいずれかをクリックします。回答を送信する前に AIS へのサインインが必要です。
3. ブラウザーに結果ページが表示されます。「送信済み」 と表示されれば回答は完了し、フローは選んだ操作に従って続行します。
4. 「トップページに戻る」 をクリックすると、AIS のホームページに戻ります。

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>回答の送信完了</p></figcaption></figure>

結果ページにエラーメッセージ（例：「The selected human input action does not exist.」）が表示された場合、回答は送信されていません。AIS の会話に戻り、カードの現在の状態（タイムアウト、キャンセル済み、すでに別の方法で回答済みなど）を確認してください。

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>回答の送信失敗</p></figcaption></figure>
