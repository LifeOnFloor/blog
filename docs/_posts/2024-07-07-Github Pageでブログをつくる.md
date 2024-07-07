# 目的
- 無料
- Markdownで書ける
- デザインをいじってみたい

Github Pageでできそう　→　やってみる。

# やり方
## Github
1. Githubで新リポジトリを作成。
### Settings
1. Githubの上部メニューから`Settings`を選択。
2. サイドパネルのCode and automationから`Pages`を選択。
3. 「Build and deployment」の「Source」で`Github Actions`を選択。
4. （たしか`github-pages`というActionを選択した気がします。スクショし忘れ）
### Repository
1． mainブランチに`_post`ディレクトリを作り
2. その中に`yyyy-mm-dd-title.md`という感じの（e.g. `2024-07-07-sample.md`）ファイルを作ります。

後は自動でActionが実行され、`https://ユーザ名.github.io/リポジトリ名`にサイトが公開されます。
