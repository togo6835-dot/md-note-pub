# Markdown チートシート（コピペ用 + 表示イメージ付き）

このノートは、**Markdown の記法をコピペしやすい形**でまとめつつ、  
**実際にどう表示されるか**も横に確認できるようにしたチートシートです。

GitHub でよく使う記法、特に `> [!IMPORTANT]` などの **GitHub Alerts / Callouts** も含めています。

---

# 目次

- [1. 見出し](#1-見出し)
- [2. 段落と改行](#2-段落と改行)
- [3. 強調](#3-強調)
- [4. リスト](#4-リスト)
- [5. 引用](#5-引用)
- [6. コード](#6-コード)
- [7. 区切り線](#7-区切り線)
- [8. リンク](#8-リンク)
- [9. 画像](#9-画像)
- [10. 表](#10-表)
- [11. チェックリスト](#11-チェックリスト)
- [12. 折りたたみ](#12-折りたたみ)
- [13. 数式](#13-数式)
- [14. エスケープ](#14-エスケープ)
- [15. GitHub 特有の記法](#15-github-特有の記法)
- [16. GitHub Alerts / Callouts](#16-github-alerts--callouts)
- [17. よく使うテンプレート](#17-よく使うテンプレート)

---


# 1. 見出し

## コピペ用

```markdown
# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6
```

## 表示イメージ

# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6

---

# 2. 段落と改行

## コピペ用

```markdown
これは1つ目の段落です。

これは2つ目の段落です。
```

## 表示イメージ

これは1つ目の段落です。

これは2つ目の段落です。

## 行末で改行したい場合

### コピペ用

```markdown
1行目の末尾に半角スペースを2つ入れる  
2行目
```

### 表示イメージ

1行目の末尾に半角スペースを2つ入れる  
2行目

## HTML の `<br>` を使う場合

### コピペ用

```markdown
1行目<br>
2行目
```

### 表示イメージ

1行目<br>
2行目

---

# 3. 強調

## 太字

### コピペ用

```markdown
**太字**
__太字__
```

### 表示イメージ

**太字**  
__太字__

## 斜体

### コピペ用

```markdown
*斜体*
_斜体_
```

### 表示イメージ

*斜体*  
_斜体_

## 太字 + 斜体

### コピペ用

```markdown
***太字かつ斜体***
```

### 表示イメージ

***太字かつ斜体***

## 打ち消し線

### コピペ用

```markdown
~~取り消したい文字~~
```

### 表示イメージ

~~取り消したい文字~~

## インラインコード

### コピペ用

```markdown
`print("Hello")`
```

### 表示イメージ

`print("Hello")`

---

# 4. リスト

## 箇条書き

### コピペ用

```markdown
- りんご
- みかん
- ぶどう
```

### 表示イメージ

- りんご
- みかん
- ぶどう

## 別の書き方

### コピペ用

```markdown
* りんご
* みかん
* ぶどう
```

```markdown
+ りんご
+ みかん
+ ぶどう
```

## 入れ子リスト

### コピペ用

```markdown
- 親
  - 子
    - 孫
```

### 表示イメージ

- 親
  - 子
    - 孫

## 番号付きリスト

### コピペ用

```markdown
1. 手順1
2. 手順2
3. 手順3
```

### 表示イメージ

1. 手順1
2. 手順2
3. 手順3

---

# 5. 引用

## 基本

### コピペ用

```markdown
> これは引用です。
```

### 表示イメージ

> これは引用です。

## 入れ子

### コピペ用

```markdown
> 親の引用
>> 子の引用
```

### 表示イメージ

> 親の引用
>> 子の引用

---

# 6. コード

## コードブロック（言語指定なし）

### コピペ用

````markdown
```
ここにコードを書く
```
````

### 表示イメージ

```text
ここにコードを書く
```

## コードブロック（Python）

### コピペ用

````markdown
```python
def hello():
    print("Hello")
```
````

### 表示イメージ

```python
def hello():
    print("Hello")
```

## よく使うコードブロック例

### Bash

#### コピペ用

````markdown
```bash
python -m venv .venv
source .venv/bin/activate
```
````

#### 表示イメージ

```bash
python -m venv .venv
source .venv/bin/activate
```

### PowerShell

#### コピペ用

````markdown
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```
````

#### 表示イメージ

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### JSON

#### コピペ用

````markdown
```json
{
  "name": "sample",
  "version": "1.0.0"
}
```
````

#### 表示イメージ

```json
{
  "name": "sample",
  "version": "1.0.0"
}
```

### YAML

#### コピペ用

````markdown
```yaml
name: CI
on: [push]
```
````

#### 表示イメージ

```yaml
name: CI
on: [push]
```

### C

#### コピペ用

````markdown
```c
#include <stdio.h>

int main(void) {
    printf("Hello\n");
    return 0;
}
```
````

#### 表示イメージ

```c
#include <stdio.h>

int main(void) {
    printf("Hello\n");
    return 0;
}
```

---

# 7. 区切り線

## コピペ用

```markdown
---
```

または

```markdown
***
```

または

```markdown
___
```

## 表示イメージ

---

---

# 8. リンク

## 通常のリンク

### コピペ用

```markdown
[OpenAI](https://openai.com)
```

### 表示イメージ

[OpenAI](https://openai.com)

## URL をそのまま書く

### コピペ用

```markdown
https://github.com
```

### 表示イメージ

https://github.com

## タイトル付きリンク

### コピペ用

```markdown
[GitHub](https://github.com "GitHub公式サイト")
```

### 表示イメージ

[GitHub](https://github.com "GitHub公式サイト")

## 参照形式リンク

### コピペ用

```markdown
[GitHub][github-link]
[OpenAI][openai-link]

[github-link]: https://github.com
[openai-link]: https://openai.com
```

### 表示イメージ

[GitHub][github-link]  
[OpenAI][openai-link]

[github-link]: https://github.com
[openai-link]: https://openai.com

---

# 9. 画像

## 基本

### コピペ用

```markdown
![代替テキスト](image.png)
```

### 表示イメージ

![代替テキスト](image.png)

## タイトル付き

### コピペ用

```markdown
![代替テキスト](image.png "画像タイトル")
```

### 表示イメージ

![代替テキスト](image.png "画像タイトル")

## 画像をクリック可能にする

### コピペ用

```markdown
[![代替テキスト](image.png)](image.png)
```

### 表示イメージ

[![代替テキスト](image.png)](image.png)

---

# 10. 表

## 基本

### コピペ用

```markdown
| 名前 | 年齢 | 所属 |
|---|---:|:---:|
| 田中 | 20 | 学生 |
| 佐藤 | 25 | 会社員 |
```

### 表示イメージ

| 名前 | 年齢 | 所属 |
|---|---:|:---:|
| 田中 | 20 | 学生 |
| 佐藤 | 25 | 会社員 |

## 配置の意味

- `:---` 左寄せ
- `---:` 右寄せ
- `:---:` 中央寄せ

## 別例

### コピペ用

```markdown
| 左寄せ | 右寄せ | 中央寄せ |
|:---|---:|:---:|
| A | 100 | X |
| B | 200 | Y |
```

### 表示イメージ

| 左寄せ | 右寄せ | 中央寄せ |
|:---|---:|:---:|
| A | 100 | X |
| B | 200 | Y |

---

# 11. チェックリスト

## コピペ用

```markdown
- [ ] 未完了
- [x] 完了
- [ ] あとでやる
```

## 表示イメージ

- [ ] 未完了
- [x] 完了
- [ ] あとでやる

---

# 12. 折りたたみ

GitHub では HTML の `<details>` が使えます。

## コピペ用

```markdown
<details>
<summary>クリックして開く</summary>

ここに隠したい内容を書く。

- 項目1
- 項目2

</details>
```

## 表示イメージ

<details>
<summary>クリックして開く</summary>

ここに隠したい内容を書く。

- 項目1
- 項目2

</details>

---

# 13. 数式

Markdown 環境によっては数式に対応しています。  
GitHub や一部のプレビュー環境では表示されます。

## インライン数式

### コピペ用

```markdown
\( E = mc^2 \)
```

### 表示イメージ

\( E = mc^2 \)

## ディスプレイ数式

### コピペ用

```markdown
\[
\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}
\]
```

### 表示イメージ

\[
\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}
\]

---

# 14. エスケープ

Markdown の記号をそのまま表示したいときは `\` を付けます。

## コピペ用

```markdown
\* これは箇条書きではない
\# これは見出しではない
\` これはコードではない
```

## 表示イメージ

\* これは箇条書きではない  
\# これは見出しではない  
\` これはコードではない

---

# 15. GitHub 特有の記法

## メンション

### コピペ用

```markdown
@username
```

### 表示イメージ

@username

## Issue / PR 番号参照

### コピペ用

```markdown
#123
owner/repo#123
```

### 表示イメージ

#123  
owner/repo#123

## コミットハッシュ参照

### コピペ用

```markdown
abc1234
```

### 表示イメージ

abc1234

## ファイル名を目立たせる

### コピペ用

```markdown
`README.md`
`src/main.py`
`requirements.txt`
```

### 表示イメージ

`README.md`  
`src/main.py`  
`requirements.txt`

---

# 16. GitHub Alerts / Callouts

GitHub でよく使う注意ボックスです。  
`>` と `[!NOTE]` などを組み合わせて書きます。

## NOTE

### コピペ用

```markdown
> [!NOTE]
> これは補足情報です。
```

### 表示イメージ

> [!NOTE]
> これは補足情報です。

## TIP

### コピペ用

```markdown
> [!TIP]
> これはヒントです。
```

### 表示イメージ

> [!TIP]
> これはヒントです。

## IMPORTANT

### コピペ用

```markdown
> [!IMPORTANT]
> これは重要事項です。
```

### 表示イメージ

> [!IMPORTANT]
> これは重要事項です。

## WARNING

### コピペ用

```markdown
> [!WARNING]
> これは警告です。
```

### 表示イメージ

> [!WARNING]
> これは警告です。

## CAUTION

### コピペ用

```markdown
> [!CAUTION]
> これは特に注意が必要な内容です。
```

### 表示イメージ

> [!CAUTION]
> これは特に注意が必要な内容です。

## 複数行で書く場合

### コピペ用

```markdown
> [!IMPORTANT]
> この設定は一度変更すると戻しにくいです。  
> 実行前にバックアップを取ってください。
```

### 表示イメージ

> [!IMPORTANT]
> この設定は一度変更すると戻しにくいです。  
> 実行前にバックアップを取ってください。

## 箇条書きを入れる場合

### コピペ用

```markdown
> [!TIP]
> 次の順で進めると楽です。
> - Python を入れる
> - 仮想環境を作る
> - 必要なパッケージを入れる
```

### 表示イメージ

> [!TIP]
> 次の順で進めると楽です。
> - Python を入れる
> - 仮想環境を作る
> - 必要なパッケージを入れる

---

# 17. よく使うテンプレート

## 17.1 学習ノート用テンプレート

### コピペ用

```markdown
# 学習ノート: タイトル

## 目的
- 何を理解したいか
- 何を実装したいか

## 要点
- ポイント1
- ポイント2
- ポイント3

## コード
```python
print("sample")
```

## メモ
> [!NOTE]
> 補足や気づきを書く。

## 次にやること
- [ ] 続きを読む
- [ ] 実装する
- [ ] 復習する
```

## 17.2 README 用テンプレート

### コピペ用

```markdown
# プロジェクト名

## 概要
このプロジェクトは〇〇を行うためのものです。

## 特徴
- 特徴1
- 特徴2
- 特徴3

## 動作環境
- Python 3.12
- JAX
- NumPy

## インストール
```bash
pip install -r requirements.txt
```

## 使い方
```bash
python main.py
```

## 注意
> [!IMPORTANT]
> 実行前に仮想環境を有効化してください。
```

## 17.3 手順書用テンプレート

### コピペ用

```markdown
# 作業手順書

## 1. 目的
この手順書は〇〇のためのものです。

## 2. 前提条件
- Python がインストール済み
- VS Code がインストール済み

## 3. 手順

### 3.1 フォルダ作成
```powershell
mkdir sample-project
cd sample-project
```

### 3.2 仮想環境作成
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3.3 パッケージ導入
```powershell
pip install jupyterlab numpy matplotlib
```

## 4. 注意
> [!WARNING]
> 仮想環境を有効化してから作業してください。
```

---

# 18. よく使う記法だけを最短で確認したい人向け

## コピペ用まとめ

```markdown
# 見出し1
## 見出し2

**太字**
*斜体*
~~打ち消し~~
`コード`

- 箇条書き
- 箇条書き

1. 番号付き
2. 番号付き

- [ ] 未完了
- [x] 完了

> 引用

[リンク](https://example.com)

![画像](image.png)

| 項目 | 内容 |
|---|---|
| A | B |

```python
print("Hello")
```

> [!IMPORTANT]
> 重要事項を書く
```

## 表示イメージ

# 見出し1
## 見出し2

**太字**  
*斜体*  
~~打ち消し~~  
`コード`

- 箇条書き
- 箇条書き

1. 番号付き
2. 番号付き

- [ ] 未完了
- [x] 完了

> 引用

[リンク](https://example.com)

![画像](image.png)

| 項目 | 内容 |
|---|---|
| A | B |

```python
print("Hello")
```

> [!IMPORTANT]
> 重要事項を書く

---

# 19. よくあるミス

## 見出しのあとにスペースがない

### 悪い例

```markdown
#見出し
```

### 良い例

```markdown
# 見出し
```

## 入れ子リストのインデント不足

### 悪い例

```markdown
- 親
- 子
```

### 良い例

```markdown
- 親
  - 子
```

## コードブロックの閉じ忘れ

コードフェンスを閉じ忘れると、その後の表示が全部崩れます。

## 表の区切りがずれる

列数がそろっていないと表が崩れます。

---

# 20. 実用サンプル

以下は、実際によくある「Python 仮想環境の説明」の Markdown 例です。

## コピペ用

```markdown
# Python 仮想環境の作成

## 目的
Python のプロジェクトごとに環境を分ける。

## 手順

### 1. フォルダを作る
```powershell
mkdir sample-project
cd sample-project
```

### 2. 仮想環境を作る
```powershell
python -m venv .venv
```

### 3. 有効化する
```powershell
.venv\Scripts\Activate.ps1
```

### 4. パッケージを入れる
```powershell
pip install numpy matplotlib jupyterlab
```

> [!IMPORTANT]
> 仮想環境を有効化してから `pip install` すること。

> [!TIP]
> VS Code では Python インタープリタを `.venv` に切り替えると便利です。

## 次にやること
- [ ] JupyterLab を起動する
- [ ] Notebook を作る
- [ ] サンプルコードを動かす
```

## 表示イメージ

# Python 仮想環境の作成

## 目的
Python のプロジェクトごとに環境を分ける。

## 手順

### 1. フォルダを作る
```powershell
mkdir sample-project
cd sample-project
```

### 2. 仮想環境を作る
```powershell
python -m venv .venv
```

### 3. 有効化する
```powershell
.venv\Scripts\Activate.ps1
```

### 4. パッケージを入れる
```powershell
pip install numpy matplotlib jupyterlab
```

> [!IMPORTANT]
> 仮想環境を有効化してから `pip install` すること。

> [!TIP]
> VS Code では Python インタープリタを `.venv` に切り替えると便利です。

## 次にやること
- [ ] JupyterLab を起動する
- [ ] Notebook を作る
- [ ] サンプルコードを動かす

---

# 21. 最後に

最初に覚えるべき頻出記法は次のあたりです。

- 見出し
- 箇条書き
- コードブロック
- リンク
- 画像
- 表
- 引用
- チェックリスト
- GitHub Alerts

特に GitHub 用なら、次の 3 つはかなり便利です。

- コードブロック
- チェックリスト
- `> [!IMPORTANT]` などの Alert 記法