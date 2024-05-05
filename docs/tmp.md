

## TODO

### 急ぎ

- [ ] https://x.com/ai_syacho/status/1782956863912649114
- [ ] zoltraak "slkajfka" -c ファイルパス（これで自作もいける様にする）

```
ModuleNotFoundError系は
pip install ~~~~
で解決されます。

今回は
pip install anthropic
を行うことで解決されます。

↓
pip install zoltraak
一発で依存関係全て入る様に調整します。
```

### CLI コマンド関連

- [ ] zoltraak -p "manim 動画を作りたい" これで要件定義書とプログラムが生成

  -

### ドキュメント生成

- [ ] 出力された Python ファイルと詳細設計書のドキュメントを欲しい。
  - python ファイルからドキュメントを生成したい
    - 例: `Zoltraakgenerated/calc.py` のように python ファイルを指定すると、そのファイルに対応するマークダウンドキュメントを生成、更新できるようにする
    - python ファイルの docstring やコメントからドキュメントを自動生成する
    - 生成されたドキュメントはマークダウン形式で出力する

### テスト

- [ ] テストファイルは別途作成し、必要なタイミングで git push などによりテストが実行されるようにしたい。

### Issue 管理

- [ ] issue を記述したい。

### ファイル管理

- [x] 繰り返し利用する場合は、Markdown ファイルと Python ファイルを自動的に紐付けたい。（変更がある場合のみ再コンパイル）

### 要件定義関連

- [ ] 読み上げ文章から要件定義書を生成するプログラムをあきらさんのプロジェクトで実装する。
  - 宣言型と手続き型はごちゃっと入れた方が良さそう
- [ ] ZoltraakAAA.md 〜したい で定義書を修正
- [ ] あると嬉しいのは要件定義を決める際のプロンプトドキュメント
  - コンパイラファイルは選択したい
- [ ] プログラムから要件定義に戻すフローが必要。

### その他

- [ ] 各種高級言語の変な癖を解消するための中間ファイルを事前に用意しておくのがよい。
- [ ] このファイルで、色合いに相当する部分のプロンプトの行数を教えて
- [ ] 差分をプロンプトとして伝達したい。
- [ ] 全て１から作り直す。md ファイルから
      ![image](assets/images//graph.png)

## 全体の流れ

- ① 曖昧で抽象的：初期のプロンプトがこれに相当。「ほにゃらしたい」という曖昧な要求。

shell

```
zoltraak "本書きたい"
```

↓

md ファイル
gen*def*{goal}.md

```
# ゴール: 本を書きたい
要件定義書:
{def}
```

↓

- ② 厳密で抽象的：要件定義書など。プロンプトから定義書を作成することで曖昧さが排除され、抽象的な状態になる。
  def\_{goal}.md

```
書籍執筆要件定義書:
import {def}
import {def}
import {def}

~~~~~~~
~~~~~~~
~~~~~~~
~~~~~~~
~~~~~~~
```

↓

- ③ 曖昧で具体的：具体的な行動は伴っているが、まだ試行錯誤している段階。対話型（インタプリタ）とも言える。
  exe\_{goal}.py

```
プログラム # コメント
プログラム # コメント
プログラム # コメント
プログラム # コメント
```

- ④ 厳密で具体的：1 本の具体的な行動に落とし込まれており、マニュアル化（ドキュメント型、コンパイル）された状態。

exe\_{goal}.md

```
詳細手順書（暗号化、抽象化、使い手がわかりやすい状態にする。[]

```

zoltraak book.md

### 自然言語プログラミングの系譜

```
*ChatGPT登場
    |→ プロンプトエンジニアリング
        *プロンプトのシステム開発適用の必要性
            |→ プロンプトプログラミング
                * Claude3 Opusの出現
                |→ ドキュメントプログラミング
                    |→ 自然言語プログラミング
                            motoki → arbor → zoltraak
                                        * Groq x Llama3の対話不可能な高速テキスト出力制御
                                                |→ 自然言語フレームワーク zoltraak
                                                |→ プログラミング統一言語 babel
                                                                        ↑ イマココ
```

### アップロードの仕方

PyPI にパッケージをアップロードする手順は以下の通りです。

1. パッケージの準備:

   - プロジェクトのディレクトリ構成を適切に設定します。
   - [setup.py](file:///Users/motokidaisuke/motoki/setup.py#1%2C1-1%2C1)ファイルを作成し、パッケージの情報（名前、バージョン、依存関係など）を記述します。
   - [README.md](file:///Users/motokidaisuke/motoki/README.md#1%2C1-1%2C1)ファイルを作成し、パッケージの説明や使用方法を記載します。

2. アカウントの作成と API トークンの取得:

   - PyPI の Web サイト（ https://pypi.org/ ）にアクセスします。
   - 新しいアカウントを作成するか、既存のアカウントにログインします。
   - アカウントの設定ページで、API トークンを生成します。

3. ビルドとアップロード用ツールのインストール:

   - `twine`と`setuptools`をインストールします。
     ```
     pip install twine setuptools
     ```

4. パッケージのビルド:

   - プロジェクトのルートディレクトリで以下のコマンドを実行し、パッケージをビルドします。
     ```
     python setup.py sdist bdist_wheel
     ```
   - これにより、`dist`ディレクトリにパッケージの配布用ファイルが生成されます。

5. PyPI へのアップロード:

   - 以下のコマンドを実行し、パッケージを PyPI にアップロードします。
     ```
     twine upload dist/*
     ```
   - ユーザー名とパスワードの代わりに、取得した API トークンを使用します。

6. アップロードの確認:
   - PyPI の Web サイトにアクセスし、アップロードしたパッケージが正しく表示されていることを確認します。

これで、`zoltraak`パッケージが PyPI に公開されました。ユーザーは`pip install zoltraak`コマンドを使用してパッケージをインストールできます。

注意点:

- パッケージ名は一意である必要があります。既に存在する名前は使用できません。
- バージョン番号は、新しいバージョンをアップロードするたびに増やす必要があります。
- `setup.py`ファイルには、適切なメタデータと依存関係を記述してください。
- `README.md`ファイルには、パッケージの説明や使用方法を明確に記載してください。

以上が、PyPI へのパッケージのアップロード手順です。問題がある場合は、PyPI のドキュメンテーションを参照するか、コミュニティに質問してください。

## 仮想環境を用いて実行

`pyenv` は Python のバージョン管理ツールですが、直接的に仮想環境を作成する機能は持っていません。仮想環境を作成するためには、`pyenv-virtualenv` というプラグインを使用する必要があります。

以下は `pyenv-virtualenv` を使用して仮想環境を作成する手順です。

1. **pyenv-virtualenv のインストール**

   まずは `pyenv-virtualenv` プラグインをインストールします。これは `pyenv` が既にインストールされていることを前提としています。

   ```bash
   git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
   ```

   インストール後、シェルの設定ファイル (例えば `.bashrc` や `.zshrc`) に以下を追加して、シェルを再起動します。

   ```bash
   eval "$(pyenv init --path)"
   eval "$(pyenv virtualenv-init -)"
   ```

2. **Python のインストール**

   `pyenv` を使用して、仮想環境用の Python バージョンをインストールします。

   ```bash
   pyenv install 3.8.5  # 例として Python 3.8.5 をインストール
   ```

3. **仮想環境の作成**

   次に、指定した Python バージョンで仮想環境を作成します。

   ```bash
   pyenv virtualenv 3.8.5 my-virtual-env-3.8.5
   ```

   ここで `my-virtual-env-3.8.5` は仮想環境の名前です。

4. **仮想環境のアクティベーション**

   作成した仮想環境をアクティブにします。

   ```bash
   pyenv activate my-virtual-env-3.8.5
   ```

   これで、指定した仮想環境がアクティブになります。

5. **仮想環境のデアクティベーション**

   仮想環境をデアクティブにするには、以下のコマンドを使用します。

   ```bash
   pyenv deactivate
   ```

これで `pyenv` と `pyenv-virtualenv` を使用して Python の仮想環境を作成し、管理する方法を説明しました。

ローカル環境

pip install -e .

を行うと
Users/motokidaisuke/.pyenv/versions/3.11.5
に入ってしまうらしい

python setup.py sdist bdist_wheel
twine upload --verbose dist/\*

仮想環境
deactivate
rm -rf /Users/motokidaisuke/aaaaa/zoltraak-env
python3 -m venv /Users/motokidaisuke/aaaaa/zoltraak-env
source /Users/motokidaisuke/aaaaa/zoltraak-env/bin/activate

# アイデア（重要）

呪文 → 文書 → 構造体 → 情報構造体 → 実行
|→ 自然言語 |→ 自然言語
|→ プログラミング言語

# メモ

```

import compiler.dev.obj
import writer.book.lecture

```

# TODO

- [ ] ディレクトリ構築はペーストではなくシステムから構築するか聞かれるようにする
- [ ] Python のファイル取得部は関数化して外部ファイル化ける
- [ ] デザイナーと開発者を導入。

# 0.1.25 更新情報

2024_04_28

- setting → grimoires に変更
- react & fast API の要件定義書を記載しディレクトリを構築する dev_react_fast_api を追加
- formatter 25 パターンほど追加
- 実行フローを整理、アニメーション追加

# チップス

zoltraak "かぞく情報データ分析 v4" -c dev_react_fastapi

とやると要件定義書名にバージョンを記載してくれる。

## コントリビューターの追加方法

コントリビューターを追加するには、以下の手順を実行してください:

1. issue またはプルリクエストに、以下の形式でコメントを残してください:

```
@all-contributors please add @username for <contributions>
```

`@username`をコントリビューターの GitHub ユーザー名に、`<contributions>`をコントリビュートのタイプに置き換えてください。コントリビュートのタイプは、[Emoji Key](https://allcontributors.org/docs/en/emoji-key)を参照してください。

2. ボットがコントリビューターをプロジェクトに追加するためのプルリクエストを作成します。

3. プルリクエストがマージされると、コントリビューターが README に追加されます。

# 超大事なことメモ

起動式にグリモワを全部詰め込む！！！！
忘れないように
