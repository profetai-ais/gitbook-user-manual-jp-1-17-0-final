---
description: AI Studio でユーザーが利用できる機能と操作は、アカウントに割り当てられたロールによって決まります。
---

# AI Studio のロールと権限

## **AI Studio の機能ロール**

システムには既定で 3 種類の機能ロールがあります。

* **AI Studio 管理者：** プラットフォーム内のすべての機能メニューを閲覧でき、ほかのユーザーにナレッジベースと Agent 機能の高度な操作権限を付与できます。
* **AI Studio ドメインユーザー：** ナレッジベース、能力、分析、テンプレート、Agent の各機能メニューを閲覧でき、さまざまな分野やシナリオに合わせたドキュメントのナレッジベースや Agent を作成できます。
* **AI Studio ユーザー：** 社内の一般ユーザーです。ワークスペースで公開済みの Agent のみ利用できます。

### **ロールの比較**

<table data-full-width="false" data-search="false"><thead><tr><th>機能モジュール（第 1 階層）</th><th>機能モジュール（第 2 階層）</th><th>AI Studio 管理者</th><th>AI Studio ドメインユーザー</th><th>AI Studio ユーザー</th></tr></thead><tbody><tr><td><strong>ワークスペース</strong></td><td></td><td>O</td><td>O</td><td>O</td></tr><tr><td><strong>Agent</strong></td><td></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>ナレッジベース</strong></td><td></td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>Work</strong></td><td>スケジュール</td><td>O</td><td>O（自分のみ）</td><td>X</td></tr><tr><td></td><td>タスク</td><td>O</td><td>O（自分のみ）</td><td>X</td></tr><tr><td><strong>能力</strong></td><td>スキル</td><td>O</td><td>O</td><td>X</td></tr><tr><td></td><td>MCP</td><td>O</td><td>O</td><td>X</td></tr><tr><td></td><td>A2A</td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>テンプレート</strong></td><td>ワークフロー</td><td>O</td><td>O</td><td>X</td></tr><tr><td></td><td>プロンプト</td><td>O</td><td>O</td><td>X</td></tr><tr><td><strong>分析</strong></td><td>レポート</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>ジョブ管理</td><td>O</td><td>O（自分のみ）</td><td>X</td></tr><tr><td></td><td>会話モニタリング</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>監査ログ</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>Workforce モニター</td><td>O</td><td>X</td><td>X</td></tr><tr><td><strong>システム設定</strong></td><td>モデル</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>クォータ</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>構成</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>API Key</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>キー管理</td><td>O</td><td>X</td><td>X</td></tr><tr><td></td><td>タグ管理</td><td>O</td><td>X</td><td>X</td></tr></tbody></table>
