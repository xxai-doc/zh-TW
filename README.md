[‼️]: ✏️README.mdt

<p align="center"><a href="https://xxai.art"><img src="https://cdn.jsdelivr.net/gh/xxai-art/doc/logo.svg"/></a><br/><a href="https://xxai.art"><img src="https://cdn.jsdelivr.net/gh/xxai-art/doc/xxai.svg"/></a></p><p align="center"><a href="https://github.com/xxai-art/doc#readme"><img alt="I18N" src="https://cdn.jsdelivr.net/gh/wactax/img/t.svg"/></a>　<a href="https://groups.google.com/u/0/g/xxai-art"><img alt="Google Groups" src="https://cdn.jsdelivr.net/gh/wactax/img/g-groups.svg"/></a></p>

# xxAI.art

網站代碼部分開源，歡迎幫忙優化翻譯。

## 前端代碼

* [前端代碼](https://github.com/xxai-art/web)
* [網站整體的語言包](https://github.com/xxai-art/web/tree/main/i18n)
* [登錄模塊的語言包](https://github.com/wacpkg/user/tree/main/ui.i18n)
* [網站多語言文檔](https://github.com/xxai-doc)

前端的編程語言是 [@w5/coffee_plus](http://npmjs.com/@w5/coffee_plus) ，在 coffeescript 語法的基礎上增加了一些特性，參見 [./coffee_plus.md](./coffee_plus.md)。

## 網站、文檔國際化

基於以下 3 個項目構建

* [@w5/mdt](https://www.npmjs.com/package/@w5/mdt)

  後綴為 `.mdt`, 可以用類似 `<+ ./coffee_plus/import.js>` 的語法引用外部文件，生成後綴為 `.md` 的 markdown。

* [@w5/trmd](https://www.npmjs.com/package/@w5/trmd)

  markdown 翻譯，不會翻譯代碼和鏈接，會緩存翻譯過的句子，如果修改了譯文但沒有修改原文，再次執行不會覆蓋對譯文的修改。

* [@w5/i18n](https://www.npmjs.com/package/@w5/i18n)

  用於翻譯 `yaml` 生成網站的語言文件。

### 文檔翻譯自動化說明

請參見代碼庫 [xxai-art/doc](https://github.com/xxai-art/doc)

建議先安裝 nodejs, [direnv](https://direnv.net), [bun](https://github.com/oven-sh/bun)，然後進入目錄後 `direnv allow` ( 進入目錄後會自動執行 [.envrc](https://github.com/xxai-art/doc/blob/main/.envrc) )。

為了避免翻譯成幾百種語言的代碼庫過大，我把每種語言單獨創建了一個代碼代碼庫，並創立一個組織來存放這個代碼庫

設置環境變量 `GITHUB_ACCESS_TOKEN` 然後運行 [create.github.coffee](https://github.com/xxai-art/doc/blob/main/create.github.coffee) 會自動創建代碼庫。

當然你也可以放到一個代碼庫中。

翻譯腳本參考 [run.sh](https://github.com/xxai-art/doc/blob/main/run.sh)

腳本代碼解讀如下：

[bunx](https://bun.sh/docs/cli/bunx) 是 npx 的替代品，更快，當然如果你沒有安裝 bun，用 `npx` 替代也可以。

`bunx mdt zh` 把 zh 目錄下的 `.mdt` 渲染為 `.md`，參見下面 2 個鏈接的文件

* [coffee_plus.mdt](https://github.com/xxai-doc/zh/blob/main/coffee_plus.mdt)
* [coffee_plus.md](https://github.com/xxai-doc/zh/blob/main/coffee_plus.md)

`bunx i18n` 是翻譯的核心代碼（如果你只安裝了 `nodejs`，沒有安裝 `bun` 和 `direnv`，也可以運行 `npx i18n` 來翻譯）。

它會解析 [i18n.yml](https://github.com/xxai-art/doc/blob/main/i18n.yml) ，本文檔的 `i18n.yml` 配置如下：

```
en:
zh: ja ko en
```

含義是 : 中文翻譯為日文、韓文、英文，英文翻譯為其他所有語種。如果你只想支持中文、英文，可以只寫 `zh: en`。

最後是 [gen.README.coffee](https://github.com/xxai-art/doc/blob/main/gen.README.coffee)，它是提取每個語種 `README.md` 大標題 和 第一個子標題 之間的內容，來生成一個入口的 `README.md` 。代碼很簡單，可以自己看一下。

用到了谷歌 API 來免費翻譯。如不能訪問谷歌，請配置並設置代理，比如 :

```
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7890
```

翻譯腳本將在 `.i18n` 目錄下生成翻譯的緩存，請用 `git status` 查看並將其添加到代碼代碼庫，避免重複翻譯。

每次修改譯文之後請運行 `bunx i18n`，更新緩存。

如果同時修改了原文和譯文，會造成緩存錯亂，所以如果要修改，只能修改一個，然後運行 `bunx i18n` 更新緩存。
