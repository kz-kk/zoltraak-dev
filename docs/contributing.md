
## コントリビューターの追加方法

コントリビューターを追加するには、以下の手順を実行してください:

1. issue またはプルリクエストに、以下の形式でコメントを残してください:

```
@all-contributors please add @username for <contributions>
```

`@username`をコントリビューターの GitHub ユーザー名に、`<contributions>`をコントリビュートのタイプに置き換えてください。コントリビュートのタイプは、[Emoji Key](https://allcontributors.org/docs/en/emoji-key)を参照してください。

2. ボットがコントリビューターをプロジェクトに追加するためのプルリクエストを作成します。

3. プルリクエストがマージされると、コントリビューターが README に追加されます。

<br>

## プロジェクトへの参加

1. リポジトリをクローンします:

   ```
   git clone https://github.com/dai-motoki/zoltraak.git
   ```

2. プロジェクトディレクトリに移動します:

   ```
   cd zoltraak
   ```

3. 仮想環境の作成
   まず、パッケージ開発用の独立した仮想環境を作成します。これにより、システム全体の Python とは分離された環境で開発できます。

```bash
python -m venv zoltraak-dev
source zoltraak-dev/bin/activate  # Linuxの場合
zoltraak-env\Scripts\activate.bat  # Windowsの場合
```

4. 必要なパッケージのインストール
   開発に必要な依存パッケージをインストールします。例えば、`setuptools`と`wheel`は最低限必要です。

```bash
pip install setuptools wheel
```

5. パッケージのインストール
   開発中のパッケージを仮想環境にインストールします。

```bash
pip install -e .
```

これで、仮想環境内でパッケージを使用したり、変更を加えたりできるようになります。

4. Anthropic API キーを設定します:
   - プロジェクトのルートディレクトリに`.env`ファイルを作成します。
   - 以下の行を`.env`ファイルに追加し、`YOUR_API_KEY`を実際の Anthropic の API キーに置き換えます:
     ```
     ANTHROPIC_API_KEY=YOUR_API_KEY
     ```

### 追加コマンド（以下はオーナーのみ）

update_and_upload.sh

```sh

echo "バージョンをアップデート中..."
python update_version.py

echo "パッケージをビルド中..."
python setup.py sdist bdist_wheel

echo "ビルドしたパッケージをPyPIにアップロード中..."
twine upload dist/*
```

## 魔導書構成

```
zoltraak/grimoires/
├── compiler: 詠唱から自然言語への変換器
│   ├── akirapp.md
│   ├── func.md
│   ├── lisp.md
│   ├── obj.md
│   ├── obj_mermaid.md
│   ├── obj_lisp.md
│   ├── obj_lisp_g.md
│   ├── obj_lisp_g_base64.md
│   └── reqdef.md
├── encryption: 暗号化ツール
│   └── emoji.md
├── formatter: プロンプトフォーマッタ
│   ├── md_comment.md
│   ├── md_comment_xx.md (md_commentの言語指定：en, zhなどに対応。ご利用の言語の略称でまずは動くか確認して、動かない場合は追加対応をお待ちください)
│   └── py_comment.md
├── interpretspec: インタプリタ型LLM強化プロンプト
│   └── hirokichi.md
└── softdb: 柔らかいDB


memo: grimoires内の全てのベンチマークは各々やるような実験システムもいれたい

```

## 使用方法

Markdown ファイルを Python コードに変換するには、以下のコマンドを使用します。

はい、以下に英語の README を日本語に翻訳しました。

## キャッシング

Zoltraak は、変更されていない Markdown ファイルの不要な変換を避けるために、キャッシングメカニズムを実装しています。各 Markdown ファイルのハッシュ値を計算し、`hashes.txt`ファイルに保存します。変換コマンドを実行すると、Zoltraak は現在のハッシュ値を保存されているものと比較します。ハッシュ値が一致する場合、Markdown ファイルが変更されていないことを示しているため、変換はスキップされ、以前に生成された Python コードが使用されます。

## CI/CD との統合

Zoltraak は CI/CD ワークフローに統合して、変換プロセスを自動化することができます。`run_tests.sh`スクリプトは、この統合を容易にするために提供されています。以下の手順を実行します。

1. 仮想環境を作成し、アクティベートします。

2. 必要な依存関係をインストールします。

3. Markdown ファイルを Python コードに変換します。

4. 生成された Python コードを実行します。

5. 対応するユニットテストを実行します。

`run_tests.sh`スクリプトを CI/CD パイプラインで使用するには、CI/CD システムがビルドプロセスの一部としてスクリプトを実行するように設定してください。



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


# 超大事なことメモ

起動式にグリモワを全部詰め込む！！！！
忘れないように



## 魔導書構成

```
zoltraak/grimoires/
├── compiler: 詠唱から自然言語への変換器
│   ├── akirapp.md
│   ├── func.md
│   ├── lisp.md
│   ├── obj.md
│   ├── obj_mermaid.md
│   ├── obj_lisp.md
│   ├── obj_lisp_g.md
│   ├── obj_lisp_g_base64.md
│   └── reqdef.md
├── encryption: 暗号化ツール
│   └── emoji.md
├── formatter: プロンプトフォーマッタ
│   ├── md_comment.md
│   ├── md_comment_xx.md (md_commentの言語指定：en, zhなどに対応。ご利用の言語の略称でまずは動くか確認して、動かない場合は追加対応をお待ちください)
│   └── py_comment.md
├── interpretspec: インタプリタ型LLM強化プロンプト
│   └── hirokichi.md
└── softdb: 柔らかいDB


memo: grimoires内の全てのベンチマークは各々やるような実験システムもいれたい

```

## 使用方法

Markdown ファイルを Python コードに変換するには、以下のコマンドを使用します。

はい、以下に英語の README を日本語に翻訳しました。

## キャッシング

Zoltraak は、変更されていない Markdown ファイルの不要な変換を避けるために、キャッシングメカニズムを実装しています。各 Markdown ファイルのハッシュ値を計算し、`hashes.txt`ファイルに保存します。変換コマンドを実行すると、Zoltraak は現在のハッシュ値を保存されているものと比較します。ハッシュ値が一致する場合、Markdown ファイルが変更されていないことを示しているため、変換はスキップされ、以前に生成された Python コードが使用されます。

## CI/CD との統合

Zoltraak は CI/CD ワークフローに統合して、変換プロセスを自動化することができます。`run_tests.sh`スクリプトは、この統合を容易にするために提供されています。以下の手順を実行します。

1. 仮想環境を作成し、アクティベートします。

2. 必要な依存関係をインストールします。

3. Markdown ファイルを Python コードに変換します。

4. 生成された Python コードを実行します。

5. 対応するユニットテストを実行します。

`run_tests.sh`スクリプトを CI/CD パイプラインで使用するには、CI/CD システムがビルドプロセスの一部としてスクリプトを実行するように設定してください。
