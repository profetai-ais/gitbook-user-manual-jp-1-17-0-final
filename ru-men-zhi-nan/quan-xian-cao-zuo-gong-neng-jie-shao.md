---
description: このページでは、Root 権限と Object 権限の操作方法を説明します。
---

# 権限の操作

## **Root 権限** <a href="#root-quan-xian" id="root-quan-xian"></a>

### **開き方**

Root の権限設定は、モジュール右上の **その他** ボタンにあります。クリックすると権限管理ウィンドウが開きます。

<figure><img src="../.gitbook/assets/image (614).png" alt=""><figcaption></figcaption></figure>

### ページの概要

<figure><img src="../.gitbook/assets/image (615).png" alt=""><figcaption></figcaption></figure>

| 項目 | 操作名       | 説明                                      |
| -- | --------- | --------------------------------------- |
| 1  | ユーザーの選択   | 名前またはアカウントで検索してユーザーを追加します               |
| 2  | 権限の選択     | 付与する一覧権限を選択します                          |
| 3  | 追加済みのユーザー | 追加済みのユーザーとその権限設定を確認し、権限の変更やユーザーの削除を行います |

### **メンバーの追加**

<figure><img src="../.gitbook/assets/image (616).png" alt=""><figcaption></figcaption></figure>

1. キーワードを入力して、追加するユーザーを検索します。
2. 付与する権限を設定します。
3. **追加** をクリックして完了します。権限は相手がページを再読み込みした後に有効になります。

### **メンバーの権限の変更**

<figure><img src="../.gitbook/assets/image (617).png" alt=""><figcaption></figcaption></figure>

1. 権限を変更するユーザーを探します。
2. 右側のドロップダウンメニューをクリックして権限を変更します。

### **メンバーの削除**

<figure><img src="../.gitbook/assets/image (618).png" alt=""><figcaption></figcaption></figure>

1. 削除するユーザーを探します。
2. 右側のドロップダウンメニューをクリックし、**削除** を選択します。

## Object 権限

Object 権限の方式は機能によって異なる場合があります。主な方式は、ロール型の権限とアクセス権限の 2 種類です。

### **開き方**

権限設定は各モジュールのオブジェクト内にあります。対象のオブジェクトをクリックし、詳細ページの **権限** タブを選択すると、権限管理ページが表示されます。ここでは Agent モジュールを例に説明します。

<figure><img src="../.gitbook/assets/image (619).png" alt=""><figcaption></figcaption></figure>

### ロール権限 <a href="#jue-se-quan-xian" id="jue-se-quan-xian"></a>

ロール権限では、ロールごとにユーザーが実行できる操作が分かれています。オブジェクトごとに 2〜3 種類の権限ロールを設定でき、作成者は **権限** からほかのユーザーにアクセス権を付与できます。権限の高いユーザーは通常、オブジェクトの設定管理、内容の調整、アクセス対象の管理ができ、権限の低いユーザーはオブジェクトの閲覧や利用のみ可能な場合があります。

主なケース：

* オブジェクトを管理できる
* オブジェクトを編集できる
* オブジェクトを閲覧・利用できる

> 注意：実際のロール名と操作できる範囲は機能の設計によって異なります（ロールの定義は [モジュール別の権限ロール](quan-xian-gong-neng-jie-shao.md) を参照してください）。

### ページの概要

<figure><img src="../.gitbook/assets/image (620).png" alt=""><figcaption></figcaption></figure>

<table data-search="false"><thead><tr><th>項目</th><th>操作名</th><th>説明</th></tr></thead><tbody><tr><td>1</td><td>表の編集</td><td>表の表示方法を変更できます</td></tr><tr><td>2</td><td>更新</td><td>クリックすると一覧を更新します</td></tr><tr><td>3</td><td>フィルター</td><td>特定の内容を詳細に絞り込みます</td></tr><tr><td>4</td><td>一括削除</td><td>項目を選択すると左上に削除ボタンが表示され、複数の項目をまとめて削除できます</td></tr><tr><td>5</td><td>検索欄</td><td>名前で検索します</td></tr><tr><td>6</td><td>招待</td><td>組織またはメンバーを招待します</td></tr><tr><td>7</td><td>操作</td><td>自分のロールを譲渡するか、選択したユーザーを削除します</td></tr></tbody></table>

#### **メンバーの追加**

<figure><img src="../.gitbook/assets/image (621).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (622).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (623).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (624).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (625).png" alt=""><figcaption></figcaption></figure>

1. **追加** をクリックして **メンバーの追加** ダイアログを開きます。
2. 入力欄で組織またはユーザーを検索します。
3. 対応する権限を選択します。
4. 組織／ユーザーは次の 2 つの方法で選択できます。
   * クリックして組織から検索する
   * キーワードを入力して該当する組織／ユーザーを表示し、右側の階層ボタンをクリックしてロールの階層を確認する
5. 対象の組織／ユーザーを選択した後、タグをクリックすると表示メニューが開き、組織の階層とロール内のすべてのユーザーを確認できます。
6. **追加** ボタンをクリックして招待を完了します。

> 注意：選択済みの組織やユーザーは一覧でチェック状態になり、組織一覧はまとめて全選択することもできます。選択済みの項目は入力欄に最大 3 行まで表示され、それを超える分は「+N」と表示されます。

#### **メンバーの権限の変更**

<figure><img src="../.gitbook/assets/image (626).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (627).png" alt=""><figcaption></figcaption></figure>

1. 権限を変更する組織／ユーザーを探し、編集ボタンをクリックします。
2. 権限を変更します。
3. **保存** をクリックして完了します。

#### **所有者の譲渡**

<figure><img src="../.gitbook/assets/image (629).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (630).png" alt=""><figcaption></figcaption></figure>

1. 所有権を譲渡するユーザーを探し、権限譲渡ボタンをクリックします。
2. 譲渡先のユーザー情報を確認します。
3. **譲渡** をクリックして完了します。

> 注意：
>
> 1. 所有者の譲渡はユーザーに対してのみ行えます。組織に所有者を譲渡することはできません。
> 2. 譲渡後、オブジェクトの所有者と作成者は自動的に新しいユーザーに変わります。ご自身の Object 権限は譲渡前の設定のまま維持されます。

#### **メンバーの削除**

<figure><img src="../.gitbook/assets/image (631).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (632).png" alt=""><figcaption></figcaption></figure>

1. 削除する組織／ユーザーを探し、削除ボタンをクリックします。
2. 削除するか再確認し、削除ボタンをクリックします。

### アクセス権限 <a href="#cun-qu-quan-xian" id="cun-qu-quan-xian"></a>

アクセス権限は組織または個々のユーザーに付与できます。組織に付与した場合、その組織内のすべてのユーザーがそのデータを利用できます。ここではナレッジベースのデータセットを例に説明します。

{% hint style="info" %}
AI Studio で現在アクセス権限の設定があるオブジェクトは、**ナレッジベースのデータセット** と **MCP の MCPツール** です。
{% endhint %}

#### **メンバーの追加**

<figure><img src="../.gitbook/assets/image (633).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (634).png" alt=""><figcaption></figcaption></figure>

1. **ナレッジ設定メニュー** の _データセットの権限_ をクリックします。
2. ボタンをクリックして、データセットに権限を一括追加します。
3. **データセット** エリアで、権限を設定するファイルを選択します。
4. 右側のエリアで **組織** タブをクリックし、権限を付与する組織の階層にチェックを入れます。
5. 右側のエリアで **ユーザー** タブをクリックし、権限を付与するユーザーを選択します。
6. **ユーザーメニュー** で追加するユーザーを検索します。
7. 組織とユーザーの変更が終わったら、**OK** ボタンをクリックして設定を保存します。

#### **メンバーの削除**

<figure><img src="../.gitbook/assets/image (635).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (635).png" alt=""><figcaption></figcaption></figure>

1. 変更するデータセットの編集ボタンをクリックします。
2. 削除する組織またはユーザーを選択し、削除ボタンをクリックします。
3. **保存** をクリックして完了します。
