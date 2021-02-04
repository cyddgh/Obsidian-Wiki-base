# 功能 : 
>用來檢查用戶是否還跟伺服器連線，如果有則傳回true，沒有的話就是false
* [微軟官方教學文章](https://docs.microsoft.com/zh-tw/dotnet/api/system.web.httpresponse.isclientconnected?view=netframework-4.8)
## 正確程式範例 : 
``` C#
public partial class Ch02_6 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
            if (Response.IsClientConnected)  
            {
                Response.Write("連線中….");
            }
            else 
            {
                Response.Write("已經離線了….掰掰！"); 
            }
    
    }
}
```
## 錯誤程式範例 (if後面不能加 ;)
``` C#
public partial class Ch02_6_1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        //*************************************************
        if (Response.IsClientConnected);   //==|||這裡有錯！
        {
           /* 註：if這一行程式，後面沒有分號(;)結尾。
           * if判別式，是同一區塊。在if這一行程式加上分號，如：
           * if (Response.IsClientConnected);  
           * 這樣底下的內容就不會被執行！
           */
            Response.Write("連線中….");
        }
        else     
        {    //註解：else這邊會出現紅底線，表示有錯！

            Response.Write("已經離線了….掰掰！");
            //本程式是錯誤的，不能執行 !
        }
    
    }
}
```