**| C# Note | Reginald&copy;2021 | IG : Xirbust.tw(懶人書架) |**
# Response 物件
![[Response觀念.PNG]]
## .Write() 輸出資料
### Code Behind
>將Html與程式碼分開放在不同檔案，副檔名如 : 「.aspx.vb或.aspx.cs」
```C#
public partial class Ch01 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Response.Write("*** 我愛ASP.NET *** (Code Behind)");
    }
}
```

### Inline Code
>就是像義大利麵，把肉醬跟麵混在一起，如下面把Html跟程式碼混在.aspx檔
```C#
<div>
	<%=("Hello!The World") %>
	<% //--註解：用「=」代替 Response.Write()，如果結尾加「;」號會錯誤 %>

	<br />

	<% Response.Write("Hello!The World"); %>
	<% //--註解：這種寫法「一定」在C#程式的結尾加上「;」號才正確！ %>
	
	<br />
	<%="***您好！***" %>
</div>

```

#### Example1 : Write + Var_String
```C#
public partial class Ch02_3 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        String u_word = "我愛ASP.NET";
        //註解：宣告my_word變數為「字串型態」。

        //Response.Write(u_word);   
        //註解：變數名稱在Response.Write()裡面，「不」需要加上雙引號（”）
    }
}

```
#### Example2 : Write + Var_String
```C#
public partial class Ch02_3_1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
         String u_word;
         u_word = "我愛ASP.NET";
        //註解：宣告my_word變數為「字串型態」。

        Response.Write(u_word);
		//註解：變數名稱「不」需要加上雙引號（”）。
    }
}

```
---
## .WriteFile() 輸出檔案內資料
#### Example
```C#
public partial class Ch02_4 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Response.WriteFile("123.txt");
        //Response的 .WriteFile()方法
        //將文字檔案123.txt的內容，輸出到畫面
        //執行時，瀏覽器網頁編碼，改成Big-5正體中文防亂碼
    }
}
```
---
## .Redirect() 網頁重新導向
>* 可將網頁重新導向到其他外部網站
>* 而[[Server.Transfer( )]]只能在同個網站內進行導向
### 原網頁導向到Google.com
``` Html
<%@ Page Language="C#" AutoEventWireup="true" CodeFile="05.aspx.cs" Inherits="Ch02_5" %>
<!DOCTYPE html>
<html xmlns="https://www.google.com/">
<head runat="server">
    <title>Ch2</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
		<p>原網頁導向到Google.com</p>
    </div>
    </form>
</body>
</html>
```
### 用.Redirect()重新導向到Bing.com
``` C#
public partial class Ch02_5 : System.Web.UI.Page
{
	//重新導向到Bing.com
    protected void Page_Load(object sender, EventArgs e)
    {
        Response.Redirect("https://www.bing.com/"); 
    }
}
```
---
## .End() 中斷程式執行
``` C#
public partial class Ch02_5_1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
           Response.End();    
           //註解：程式在此中斷停止，下一行程式碼將永遠無法被執行
           Response.Redirect("http://www.find.org.tw/");
    }
}
```
## 延伸學習 & 注意事項
* **C#和VB的true和false大不同 : ** C#的t和f是小寫開頭，VB的T和F則是大寫開頭
* [使用.Redirect和IsClientConnected判斷用戶是否繼續導向到網站](https://docs.microsoft.com/zh-tw/dotnet/api/system.web.httpresponse.redirect?view=netframework-4.8)
* [[IsClientConnected屬性]]
* [[緩衝區處理 - 提升數據傳輸效率]]
---
## if...else判別式
* [複習C#運算子](https://ithelp.ithome.com.tw/articles/10213220)
### Example1
>* 如果a>10，顯示**"恭喜！a的值，大於10喔！"**
>* 如果a<10，顯示**"抱歉！a的值，小於10。"**
``` C#
public partial class Ch02_8_1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        //註解：判別「a」是否大於10？
        int a = 15;

        if (a > 10)
        {
            Response.Write("恭喜！a的值，大於10喔！");
        }
        else
        {
            Response.Write("抱歉！a的值，小於10。");
        }
    }
}
```
### Example2
>* 透過Request來擷取使用者在URL上的要求
>* 如下圖 : 使用者只要更改連結後面的15，網頁輸出的結果就會不一樣。![[url代表意義和數值傳遞.png]]
>* 此程式用到Http請求中的「Get」
>[Get和Post的差別](https://medium.com/@totoroLiu/http-post-%E5%92%8C-get-%E5%B7%AE%E7%95%B0-928829d29914)、[深入了解Http其他請求方法](https://developer.mozilla.org/zh-TW/docs/Web/HTTP/Methods)
``` C#
public partial class Ch02_8 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        //註解：判別「使用者輸入的值」是否大於10？
        
        int a = Convert.ToInt32(Request["u_number"]);
        //使用者傳來一個值，給這支程式來執行。
        //要用Request[“變數名稱”]來接收使用者傳來的值。
        //「Request[“u_number]」就等於是「15」的意思。
		//注意:C#把u_number視為字串，要用Convert.ToInt32轉成整數
		if  (a > 10) {
		      Response.Write("恭喜！您輸入的值，大於10喔！"); 
        }
		else {
		      Response.Write("抱歉！您輸入的值，小於10。");
        }
    }
}
```
### Example3
>在URL裡輸入很不方便，可加入TextBox(輸入數字的方框)
``` C#
	//Html
	<form id="form1" runat="server">
    <div>
        請輸入一個整數（1~20之間）<br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Button_大於10? 或是小於10?" onclick="Button1_Click" />
    </div>
    </form>
	//---
	//C#
    protected void Button1_Click(object sender, EventArgs e)
    {
        //註解：判別「使用者輸入的值」是否大於10？

        int a = Convert.ToInt32(TextBox1.Text);
        // C#語法比較嚴謹，務必先把輸入的值，轉成適當的格式
        //    （例如：本範例轉成 Int整數型態），否則就會報錯！

        if (a > 10)
        {
            Response.Write("恭喜！您輸入的值，大於10喔！");
        }
        else
        {
            Response.Write("抱歉！您輸入的值，小於10。");
        }
    }
```
### 延伸補充(尚未理解的新東西(?)
* .Net 4.5以上HttpRequest類別多了**.GetBufferedinputStream方法，可增強傳輸效能**，支援非同步傳輸，可讀取連入Http實體(entity)本文的Stream物件
* 爬文找到 : 
* [使用此方法出現問題的處理](https://blog.csdn.net/cp252819/article/details/104559798?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161063448616780299060843%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=161063448616780299060843&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-1-104559798.pc_search_result_no_baidu_js&utm_term=GetBufferedinputStream&spm=1018.2226.3001.4187)
* [InputStream和BufferedInputStream詳解](https://blog.csdn.net/iteye_15490/article/details/82603219?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522161063500916780299011669%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=161063500916780299011669&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_v2~rank_v29-9-82603219.pc_search_result_no_baidu_js&utm_term=GetBufferedinputStream%E7%94%A8%E6%B3%95&spm=1018.2226.3001.4187)
---
## 巢狀 if 判斷
>* **注意 : ** if判斷式如果要判斷太多東西，會變得不好用 !
>* 接下來會介紹「Switch判斷式」來解決這問題
``` C#
//Html
    <form id="form1" runat="server">
    <div>
        請輸入一個整數（1~20之間）<br />
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Button_大於10?等於10?或是小於10?"
		onclick="Button1_Click"/>
    </div>
    </form>
//C#
    protected void Button1_Click(object sender, EventArgs e)
    {
        //註解：判別「使用者輸入的值」是否大於10？
        if (Convert.ToInt32(TextBox1.Text) > 10)
        {
            Response.Write("恭喜！您輸入的值，大於10喔！");
        }
        else
        {
            //註解：如果使用者輸入的值「不大於10」，一定是「小於」或「等於」10，
            //再用一次if，就能正確判斷:使用者輸入的值=10。

            if (Convert.ToInt32(TextBox1.Text) == 10)
            {
                Response.Write("您輸入的值，剛好等於10。");
            }
            else
            {
                Response.Write("抱歉！您輸入的值，小於10。");
            }
        }
    }
```
## Switch...case判斷式
* **延伸範例 : **[判斷四季](https://blog.csdn.net/homedjy/article/details/8505014)
``` C#
	//加入textbox和button
	//Html
	<form id="form1" runat="server">
    <div>
        <asp:TextBox ID="TextBox1" runat="server"></asp:TextBox>
        <asp:Button ID="Button1" runat="server" Text="Button" onclick="Button1_Click"/>
    </div>
    </form>
	//---
	//C#
    protected void Button1_Click (object sender, EventArgs e)
    {
        int a = Convert.ToInt32(TextBox1.Text);
        //int u_int = Convert.ToInt32(Request["u_number"]);

        switch (a)
        {
            case 1:
                Response.Redirect("http://www.find.org.tw/");
                break;
            case 2:
                Response.Redirect("http://www.iii.org.tw/");
                break;
            case 3:
                Response.Redirect("http://www.yahoo.com.tw/");
                break;
            default:
                //註解：如果使用者不輸入數字的話，就會出現警告訊息。
                Response.Write("使用者務必輸入一個數字！限定1~3");
                break;
        }
    }
```
## For 記數迴圈
**範例 : 計算1+2+3+4+5+...+100的答案**
>**範例講解 : ** 一台卡車(變數)名字叫my_sum，int my_sum = 0;(設為0，代表沒貨物)，my_sum(卡車) = my_sum + i (值，就是卡車載的總貨物)。
>* **進第1次迴圈** => 現在 i 有1個貨物，my_sum(0) + i(1)，所以這時my_sum卡車上有1個貨物。
>* **進第2次迴圈** => 現在 i 有2個貨物，會先把前面的1個貨物卸掉，變回my_sum(0) + i(2)，卡車上有2個貨物，最後再把前面的1個貨物放回去，最後是my_sum(1) + i(2) = 1+2。
>* **思考 : **如果不卸貨，會是my_sum(1) + i(2) => my_sum(1) + i(3)。
``` C#
    protected void Page_Load(object sender, EventArgs e)
    {
        int my_sum = 0;

        for (int i = 1; i <= 100; i++)
        { //註解：請計算1+2+3+4+....+99+100 ，答案等於多少？
           my_sum = my_sum + i;
           Response.Write(i + "<br />");
        }
        Response.Write("從1累加到100；<hr />計算1+2+3+4+....+99+100，答案是--- " + my_sum);
    }
```
## 迴圈搭配字串連接
**範例 : 顯示出a1、a2、a3...a100**
>* 這部份很多地方都應用得到 ! (如檔案批次上傳)
>* 注意 : 過度使用字串連接，可能受到[SQL injection(資料隱碼攻擊)](https://medium.com/@gordonfang_85054/%E8%B3%87%E5%AE%89%E6%BB%B2%E9%80%8F%E6%94%BB%E9%98%B2%E7%AD%86%E8%A8%98-1-c9a6b8ada5fa)
>* 如果要從大型資料庫找出**大量**、多變化的字串，可以用**[[Syetem.Text.StringBulider]]**
```C#
    protected void Page_Load(object sender, EventArgs e)
    {
        //在畫面上，連續印出a1，a2，a3……，a100（解決範例14.aspx的缺失）
        for (int i = 1; i < 101; i++)
        {
            Response.Write("a" + i);  //註解：”a”是字串，而後面的 i是變數。

            //*************************************************
            // 範例14.aspx還有一個小缺點，就是到了最後一個 a100。程式就該結束，
            // 但畫面上卻多了一個「，」號，讓輸出畫面不美觀。
            // 我加上一個if判別式來解決這個問題
            //******************************************
            if (i < 100)//註解：寫成 if (i != 100)也可。!= 表示「不」等於
            {
                Response.Write(" ，<br />");
            }

        }
    }
```
## break暫時脫離迴圈

## While條件式迴圈