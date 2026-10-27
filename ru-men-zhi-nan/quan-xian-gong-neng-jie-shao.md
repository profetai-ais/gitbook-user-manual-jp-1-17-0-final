---
description: このページでは、各モジュールの権限について説明します。
---

# モジュール別の権限ロール

## **Agent モジュールの権限**

### **Agent 一覧** <a href="#agent-qing-dan" id="agent-qing-dan"></a>

以下の表は「Agent 一覧」レベルでできることを示しています。「Agent 一覧」は 1 つの管理範囲と考えてください。項目を作成できるか、メンバーを管理できるか、すべての項目を閲覧・編集できるかは、この機能一覧で付与されたロールによって決まります。

<figure><img src="../.gitbook/assets/image (594).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>Agent 一覧管理者</th><th>Agent 一覧ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>Agent 一覧と Agent のすべての機能を操作できるロール</td><td>自分の Agent を作成・編集できるロール</td></tr><tr><td><strong>Agent の作成</strong></td><td>O</td><td>O</td></tr><tr><td><strong>Agent 一覧のメンバー管理</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべての Agent の閲覧</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべての Agent の編集</strong></td><td>O</td><td>X</td></tr></tbody></table>

### Agent <a href="#agent" id="agent"></a>

以下の表は「Agent」レベルでできることを示しています。このレベルでは通常、**Agent 管理者** または **Agent 編集者** がメンバーを管理し、編集者やユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (595).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>Agent 管理者</th><th>Agent 編集者</th><th>Agent ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>Agent を完全に管理できる</td><td>Agent の利用と内容の調整を補助できる</td><td>ワークスペースで Agent を利用することのみできるロール</td></tr><tr><td><strong>ワークスペースでの Agent の利用</strong></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>Agent 一覧での Agent の閲覧</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>Agent のメンバー管理</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>Agent の編集</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>Agent の削除</strong></td><td>O</td><td>X</td><td>X</td></tr></tbody></table>

> 注意：Agent 管理者と Agent 編集者は、ナレッジベース、ツール、スキル、SubAgent、プロンプトテンプレートの利用権限を持っていなくても、Agent の設定からその項目を削除できます。

## **ナレッジベースモジュールの権限**

### ナレッジベース一覧 <a href="#zhi-shi-ku-qing-dan" id="zhi-shi-ku-qing-dan"></a>

以下の表は「ナレッジベース一覧」レベルでできることを示しています。「ナレッジベース一覧」は 1 つの管理範囲と考えてください。項目を作成できるか、メンバーを管理できるか、すべての項目を閲覧・編集できるかは、この機能一覧で付与されたロールによって決まります。

<figure><img src="../.gitbook/assets/image (596).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>ナレッジベース一覧管理者</th><th>ナレッジベース一覧ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>ナレッジベースとナレッジのすべての機能を操作できるロール</td><td>自分のナレッジを作成・編集できるロール</td></tr><tr><td><strong>ナレッジの作成</strong></td><td>O</td><td>O</td></tr><tr><td><strong>ナレッジベースのメンバー管理</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのナレッジの閲覧</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのナレッジの編集</strong></td><td>O</td><td>X</td></tr></tbody></table>

### ナレッジ <a href="#zhi-shi" id="zhi-shi"></a>

以下の表は「ナレッジ」レベルでできることを示しています。このレベルでは通常、**ナレッジ管理者** または **ナレッジ編集者** がメンバーを管理し、編集者やユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (597).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>ナレッジ管理者</th><th>ナレッジ編集者</th><th>ナレッジユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>ナレッジを完全に管理できる</td><td>ナレッジの内容の調整を補助できる</td><td>ナレッジの読み取りのみできるロール</td></tr><tr><td><strong>Agent へのナレッジの追加</strong></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>ナレッジベース一覧でのナレッジの閲覧</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ナレッジのメンバー管理</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ナレッジの編集</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ナレッジの削除</strong></td><td>O</td><td>X</td><td>X</td></tr></tbody></table>

### **データセット** <a href="#shu-ju-ji" id="shu-ju-ji"></a>

ユーザー、グループ、または組織をデータセットに割り当てることで、管理者はそのデータセットをほかの機能（Agent の設定、テスト、そのほかナレッジを利用する機能など）で使えるユーザーを制御できます。

権限設定を保存すると、選択したユーザー、グループ、または組織が、対応する機能でそのデータセットにアクセスして利用できるようになります。

<figure><img src="../.gitbook/assets/image (598).png" alt=""><figcaption></figcaption></figure>

## **スキルモジュールの権限**

### **スキル一覧**

以下の表は「スキル一覧」レベルでできることを示しています。「スキル一覧」は 1 つの管理範囲と考えてください。項目を作成できるか、メンバーを管理できるか、すべての項目を閲覧・編集できるかは、この機能一覧で付与されたロールによって決まります。

<figure><img src="../.gitbook/assets/image (599).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>スキル一覧管理者</th><th>スキル一覧ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>スキル一覧とスキルのすべての機能を操作できるロール</td><td>自分のスキルを作成・編集できるロール</td></tr><tr><td><strong>スキルの作成</strong></td><td>O</td><td>O</td></tr><tr><td><strong>スキルのメンバー管理</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのスキルの閲覧</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのスキルの編集</strong></td><td>O</td><td>X</td></tr></tbody></table>

### **スキル**

以下の表は「スキル」レベルでできることを示しています。このレベルでは通常、**スキル管理者** または **スキル編集者** がメンバーを管理し、編集者やユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (600).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>スキル管理者</th><th>スキル編集者</th><th>スキルユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>スキルを完全に管理できる</td><td>スキルの内容の調整を補助できる</td><td>スキルの読み取りのみできるロール</td></tr><tr><td><strong>Agent へのスキルの追加</strong></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>スキル一覧でのスキルの閲覧</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>スキルのメンバー設定</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>スキルの編集</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>スキルの削除</strong></td><td>O</td><td>X</td><td>X</td></tr></tbody></table>

## **MCP モジュールの権限**

### **MCP 一覧** <a href="#mcp-qing-dan" id="mcp-qing-dan"></a>

以下の表は「**MCP** 一覧」レベルでできることを示しています。「**MCP** 一覧」は 1 つの管理範囲と考えてください。項目を作成できるか、メンバーを管理できるか、すべての項目を閲覧・編集できるかは、この機能一覧で付与されたロールによって決まります。

<figure><img src="../.gitbook/assets/image (601).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>MCP 一覧管理者</th><th>MCP 一覧ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>MCP 一覧と MCP のすべての機能を操作できるロール</td><td>自分の MCP を作成・編集できるロール</td></tr><tr><td><strong>MCP の作成</strong></td><td>O</td><td>O</td></tr><tr><td><strong>MCP のメンバー管理</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべての MCP の閲覧</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべての MCP の編集</strong></td><td>O</td><td>X</td></tr></tbody></table>

### **MCP** <a href="#mcp" id="mcp"></a>

以下の表は「MCP」レベルでできることを示しています。このレベルでは通常、**MCP 管理者** または **MCP 編集者** がメンバーを管理し、編集者やユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (602).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>MCP 管理者</th><th>MCP 編集者</th><th>MCP ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>MCP を完全に管理できる</td><td>MCP の内容の調整を補助できる</td><td>MCP の読み取りのみできるロール</td></tr><tr><td><strong>Agent への MCP の追加</strong></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>MCP 一覧での MCP の閲覧</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>MCP のメンバー設定</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>MCP の編集</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>MCP の削除</strong></td><td>O</td><td>X</td><td>X</td></tr></tbody></table>

### MCPツール <a href="#mcp-gong-ju" id="mcp-gong-ju"></a>

ユーザー、グループ、または組織をツールに割り当てることで、管理者はそのツールをほかの機能（Agent の設定、テスト、そのほかツールを利用する機能など）で使えるユーザーを制御できます。

権限設定を保存すると、選択したユーザー、グループ、または組織が、対応する機能でそのツールにアクセスして利用できるようになります。

<figure><img src="../.gitbook/assets/image (603).png" alt=""><figcaption></figcaption></figure>

## **ワークフローテンプレートモジュールの権限**

### **ワークフローテンプレート一覧** <a href="#gong-zuo-liu-cheng-mu-ban-qing-dan" id="gong-zuo-liu-cheng-mu-ban-qing-dan"></a>

以下の表は「ワークフローテンプレート一覧」レベルでできることを示しています。「ワークフローテンプレート一覧」は 1 つの管理範囲と考えてください。項目を作成できるか、メンバーを管理できるか、すべての項目を閲覧・編集できるかは、この機能一覧で付与されたロールによって決まります。

<figure><img src="../.gitbook/assets/image (604).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>ワークフローテンプレート一覧管理者</th><th>ワークフローテンプレート一覧ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>ワークフローテンプレート一覧とワークフローテンプレートのすべての機能を操作できるロール</td><td>自分のワークフローテンプレートを作成・編集できるロール</td></tr><tr><td><strong>ワークフローテンプレートの作成</strong></td><td>O</td><td>O</td></tr><tr><td><strong>ワークフローテンプレート一覧のメンバー管理</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのワークフローテンプレートの閲覧</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのワークフローテンプレートの編集</strong></td><td>O</td><td>X</td></tr></tbody></table>

### ワークフローテンプレート <a href="#gong-zuo-liu-cheng-mu-ban" id="gong-zuo-liu-cheng-mu-ban"></a>

以下の表は「ワークフローテンプレート」レベルでできることを示しています。このレベルでは通常、**ワークフローテンプレート管理者** または **ワークフローテンプレート編集者** がメンバーを管理し、編集者やユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (605).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>ワークフローテンプレート管理者</th><th>ワークフローテンプレート編集者</th><th>ワークフローテンプレートユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>ワークフローテンプレートを完全に管理できる</td><td>ワークフローテンプレートの内容の調整を補助できる</td><td>ワークフローテンプレートの読み取りのみできるロール</td></tr><tr><td><strong>ワークスペースでのワークフローテンプレートの利用</strong></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>ワークフローテンプレート一覧での閲覧</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ワークフローテンプレートのメンバー設定</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ワークフローテンプレートの編集</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ワークフローテンプレートの削除</strong></td><td>O</td><td>X</td><td>X</td></tr></tbody></table>

## **プロンプトテンプレートモジュールの権限**

### **プロンプトテンプレート一覧** <a href="#ti-shi-ci-mu-ban-qing-dan" id="ti-shi-ci-mu-ban-qing-dan"></a>

以下の表は「プロンプトテンプレート一覧」レベルでできることを示しています。「プロンプトテンプレート一覧」は 1 つの管理範囲と考えてください。項目を作成できるか、メンバーを管理できるか、すべての項目を閲覧・編集できるかは、この機能一覧で付与されたロールによって決まります。

<figure><img src="../.gitbook/assets/image (606).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>プロンプトテンプレート一覧管理者</th><th>プロンプトテンプレート一覧ユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>プロンプトテンプレート一覧とプロンプトテンプレートのすべての機能を操作できるロール</td><td>自分のプロンプトテンプレートを作成・編集できるロール</td></tr><tr><td><strong>プロンプトテンプレートの作成</strong></td><td>O</td><td>O</td></tr><tr><td><strong>プロンプトテンプレート一覧のメンバー管理</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのプロンプトテンプレートの閲覧</strong></td><td>O</td><td>X</td></tr><tr><td><strong>すべてのプロンプトテンプレートの編集</strong></td><td>O</td><td>X</td></tr></tbody></table>

### プロンプトテンプレート <a href="#ti-shi-ci-mu-ban" id="ti-shi-ci-mu-ban"></a>

以下の表は「プロンプトテンプレート」レベルでできることを示しています。このレベルでは通常、**プロンプトテンプレート管理者** または **プロンプトテンプレート編集者** がメンバーを管理し、編集者やユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (607).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>プロンプトテンプレート管理者</th><th>プロンプトテンプレート編集者</th><th>プロンプトテンプレートユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>プロンプトテンプレートを完全に管理できる</td><td>プロンプトテンプレートの内容の調整を補助できる</td><td>プロンプトテンプレートの読み取りのみできるロール</td></tr><tr><td><strong>ワークスペースでのプロンプトテンプレートの利用</strong></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>プロンプトテンプレート一覧での閲覧</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>プロンプトテンプレートのメンバー設定</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>プロンプトテンプレートの編集</strong></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>プロンプトテンプレートの削除</strong></td><td>O</td><td>X</td><td>X</td></tr></tbody></table>

## **モデルモジュールの権限**

{% hint style="info" %}
モデルモジュールは AI Studio 管理者のみが利用できるため、一覧レベルの権限設定はありません。
{% endhint %}

### **モデル** <a href="#mo-xing" id="mo-xing"></a>

以下の表は「モデル」レベルでできることを示しています。このレベルでは通常、**モデル割り当て担当者** がメンバーを管理し、ユーザーに適切な権限を割り当てます。

<figure><img src="../.gitbook/assets/image (608).png" alt=""><figcaption></figcaption></figure>

<table data-full-width="true"><thead><tr><th>ロール</th><th>モデル割り当て担当者</th><th>モデルユーザー</th></tr></thead><tbody><tr><td><strong>説明</strong></td><td>モデルの設定とモデル一覧を管理でき、アクセス可能なモデルを利用できる</td><td>アクセス可能なモデルを利用できるが、モデルは管理できない</td></tr><tr><td><strong>ワークスペースで、そのモデルを使う Agent と会話する</strong></td><td>O</td><td>O</td></tr><tr><td><strong>モデル一覧でのモデルの選択</strong></td><td>O</td><td>X</td></tr></tbody></table>
