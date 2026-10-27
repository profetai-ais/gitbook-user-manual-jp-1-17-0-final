---
description: >-
  このページでは、システムに必要なキー（API Key）をまとめて管理します。キーの追加、確認、削除を行い、システムのサービスが安全かつ正しく動作するようにします。
---

# キー管理

## ページの概要

**Key Management** ページを開くと、作成済みのキーの一覧が表示されます。各欄の説明は次のとおりです。

<figure><img src="../.gitbook/assets/image (756).png" alt=""><figcaption></figcaption></figure>

<table data-search="false"><thead><tr><th width="210">名前</th><th>説明</th></tr></thead><tbody><tr><td>Type</td><td>キーの種類（SERPER、LiteLLM など）で、そのキーが対応するサービスの種類を示します</td></tr><tr><td>Name</td><td>キーの名前で、その API Key の用途を識別するために使います</td></tr><tr><td>Key</td><td>API Key の値です。セキュリティのため、マスクして表示されます</td></tr><tr><td>Tenant ID</td><td>所属するテナントの識別子です</td></tr><tr><td>Expire Date</td><td>キーの有効期限です</td></tr><tr><td>Creator</td><td>作成者です</td></tr><tr><td>Created Date</td><td>作成日時です</td></tr><tr><td>Modified Date</td><td>最終更新日時です</td></tr><tr><td>Actions</td><td>操作機能です。現在は削除（ゴミ箱のアイコン）を利用できます</td></tr></tbody></table>

## キーの追加

<figure><img src="../.gitbook/assets/image (757).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (758).png" alt=""><figcaption></figcaption></figure>

1. 右上の「+」をクリックすると、キーを追加する設定ウィンドウが開きます。次の設定を順に行ってください。
2. Type：キーの種類を選択します。
3. Name：この API Key の識別名を入力します。後から管理しやすいよう、具体的な用途（例：`litellm api key`）を記入することをおすすめします。
4. API Key：実際の API Key を入力します。
   * 欄は既定で非表示になっています。
   * 右側の **目** のアイコンで表示／非表示を切り替えられます。
5. 送信の確認：設定が終わったら **Ok** をクリックしてキーを保存します。保存しない場合は **キャンセル** をクリックします。

## キーの削除

<figure><img src="../.gitbook/assets/image (759).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (760).png" alt=""><figcaption></figcaption></figure>

1. その行の一番右にある **Actions** 欄のゴミ箱のアイコンをクリックします。
2. 確認をクリックすると削除が実行され、そのキーはすぐに一覧から削除されます。

### **注意事項**

* **削除したキーは元に戻せません。**
* その API Key がシステムやプロセスで使われている場合、削除すると関連する機能が正常に動作しなくなることがあります。
* 削除する前に、そのキーがどのサービスやプロセスからも参照されていないことを確認することをおすすめします。
