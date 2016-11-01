## Public Preview Now Closed  

# Coming Soon! Digital Authentication Guideline: Public Comment Period  

A huge thank you to all that contributed to the public preview of draft Special Publication 800-63-3. We are suspending the collection of issues and comments for the public preview to get ready for our next phase. As we mentioned when we launched this May, we will be transitioning into a more formal process of gathering feedback from the stakeholder community in a maaner that aligns with how agencies and NIST expect to participate in reviewing SP 800-63-3.  This next part of our process is quickly coming.  Until then, the public preview pages will remain viewable.  You can find more details about next steps at [our blog site](http://nstic.blogs.govdelivery.com/).

Source information, current standards, and public comments received through May 2015 can be found [here](http://csrc.nist.gov/groups/ST/eauthentication/sp800-63-2_call-comments.html).

Full HTML version can be viewed at https://pages.nist.gov/800-63-3


# 翻訳の進め方

## ローカルサーバーの環境設定

NIST 800-63-3 のドキュメント群は, Github Pages で公開できる Web サイトとして開発されています.

このサイトをローカル環境で確認するには, [Ruby](https://www.ruby-lang.org/) + [Bundler](http://bundler.io) + [Jekyll](http://jekyllrb.com) が必要です.


### Ruby 環境のセットアップ

MacOS の場合は Ruby 2.0 の環境は整っているはずです.

Windows の場合は, [RubyInstaller](http://rubyinstaller.org) というのがあるようです.

### Bundler 環境のセットアップ

Rails 等の開発をしたことがある方は, すでに Bundler はインストールされていると思います.

ターミナルで `gem list` と打ってみて表示されるインストール済 rubygem 一覧に bundler が含まれていない場合は, 以下のコマンドで bundler gem をインストールしてください.

```
gem install bundler # sudo 必要かもしれません
```

### Jekyll 環境のセットアップ

Bundler 環境が整っていれば, 以下のコマンドで Jekyll 環境が整うはずです.

```
git clone git@github.com:openid-foundation-japan/800-63-3.git
cd 800-63-3
bundle install
```

### ローカルサーバーの立ち上げ

Repository Root で以下のコマンドを実行すると, [http://localhost:4000/800-63-3/](http://localhost:4000/800-63-3/) にローカルサーバーが立ち上がります.

```
jekyll server
```

Rails 開発等を行っているマシンでは, 以下のように `bundle exec` をつける必要があるかもしれません.

```
bundle exec jekyll server
```

なお, 各ファイルへの変更は自動的に反映されるため, 明示的に Markdown ファイルを HTML に変換する必要はありません.

また, Repository Root に `sp800-63-3.ja.md` というファイルを作成した場合, [http://localhost:4000/800-63-3/sp800-63-3.ja.html](http://localhost:4000/800-63-3/sp800-63-3.ja.html) でそのページが確認できます.

## 翻訳対象ファイルの作成

`sp800-63c` ディレクトリをみると, Section ごとの Markdown ファイルが確認できると思います.

このディレクトリでは, `sec1_2_introduction.md` を翻訳する場合, 以下のような手順を踏んでいます. (以下の各 Step は, Current ディレクトリが Repository Root である前提で書いています)

0. `cp sp800-63c.md sp800-63c.ja.md` (初回だけ)
1. `cp sp800-63c/sec1_2_introduction.md sp800-63c/sec1_2_introduction.ja.md`
2. `sp800-63c.md` 内で `sec1_2_introduction.md` を読み込んでいる部分を `sec1_2_introduction.ja.md` に変更
3. `sp800-63c/sec1_2_introduction.ja.md` を翻訳
4. 適宜ブラウザで確認

他のドキュメントでも, 同様のステップで翻訳を進めることを推奨します.

なお, 本レポジトリには以下の3つの branch が存在しますが, 翻訳作業は必ず `gh-pages` branch に対して行うようにしてください.

* master
* nist-pages (英語版のデフォルト Branch, 適宜英語版に追随するために利用)
* gh-pages (日本語版のデフォルト Branch, ここに push された変更は自動的に日本語版の [Github Pages](https://openid-foundation-japan.github.io/800-63-3/) に反映されます)

## 英語版の変更への追随

[英語版](https://github.com/usnistgov/800-63-3) でも活発に Commit がなされているため, 数日経つと英語版と日本語版で差異が生じます.

定期的に日本語版のレポジトリの `nist-pages` branch を git rebase し, 変更点を確認後, 日本語版に適宜反映していく必要があります.  
不要な変更反映作業を避けるため, 翻訳開始していない Section に関しては, `*.ja.md` ファイルを作成しないことを推奨します.

git rebase の仕方がわからない場合は, @nov に連絡していただければ rebase します.  
基本的には @nov が以下のコマンドを実行して, 各担当者に変更があった旨を通知するので, 各担当者が git log や [GitHub 上の commit history](https://github.com/openid-foundation-japan/800-63-3/commits/gh-pages) 等から, 自分の最後の commit 以降の英語版の変更を確認しながら, 更新分を日本語版に反映していくのが良いかなと思っています.

```
git remote add nist git@github.com:usnistgov/800-63-3.git # 最初だけ
git checkout -t origin/nist-pages # 最初だけ
git checkout nist-pages
git fetch nist
git rebase nist/nist-pages
git checkout gh-pages
git merge nist-pages # commit history 上で英語版の更新分を日本語版の最終 commit より後に持ってくるために, rebase ではなく merge
```
