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
