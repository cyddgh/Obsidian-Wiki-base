# 重新導向到"自己"的網頁
1. 直接在伺服器上請求，不是要求瀏覽器重新發出一個新的HTTP請求，**可減輕伺服器負荷**
2. 只能導向到自己的網頁，想重新導向到外部網站，只能用 .Redirect()
> Server.Transfer可讓**重新導向的目標網頁**，讀取**來源網頁**上的控制項與公用屬性的值，如果不要保留資訊到目標網頁，請設定參數為**「false」**
``` C#
Server.Transfer(https://www.google.com.tw/?hl=zh-TW,false)
```
## 注意事項
- 網頁有**ScriptManager**和**UpdatePanel**，用Server.Transfer會出錯
- [參考原文 .Transfer和.Redirect區別](https://dotblogs.com.tw/atowngit/2010/07/20/16648)
- [參考原文 ScriptManager 和 UpdatePanel遇到 .Transfer出錯](https://www.huanlintalk.com/2008/05/updatepanel-syswebformspagerequestmanag.html)
- [延伸理解 : 微軟官方教學](https://docs.microsoft.com/zh-tw/dotnet/api/system.web.httpserverutility.transfer?view=netframework-4.8)