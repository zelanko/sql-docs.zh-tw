---
title: "在應用程式的程式碼中使用 FOR XML 結果 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, application code usage
- XML [SQL Server], FOR XML clause
- ASP.NET [SQL Server]
- .NET Framework [SQL Server], FOR XML data
- ADO [SQL Server]
- XML data islands [SQL Server]
- data islands [SQL Server]
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f687e8b100ea8810bf92b21b0467932c72d21237
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="use-for-xml-results-in-application-code"></a>在應用程式的程式碼中使用 FOR XML 結果
  藉由在 SQL 查詢中使用 FOR XML 子句，您就可以將查詢結果擷取為 XML 資料，以及將其轉換為 XML 資料。 如果可以在 XML 應用程式的程式碼中使用 FOR XML 查詢結果，此功能便能讓您執行下列功能：  
  
-   針對 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md) 值的執行個體，查詢 SQL 資料表  
  
-   套用 [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md) ，以 XML 格式傳回包含文字或影像類型資料的查詢結果  
  
 此主題提供範例來示範這些方式。  
  
## <a name="retrieving-for-xml-data-with-ado-and-xml-data-islands"></a>以 ADO 和 XML 資料島擷取 FOR XML 資料  
 當您使用 FOR XML 查詢時，支援 COM **IStream** 介面的 ADO **Stream** 物件或其他物件，例如 Active Server Pages (ASP) **Request** 和 **Response** 物件，可用來包含結果。  
  
 例如，下列 ASP 程式碼顯示在 AdventureWorks 範例資料庫的 Sales.Store 資料表中查詢 **xml** 資料類型資料行 Demographics 的結果。 該查詢尤其會在此資料行的執行個體值中尋找 CustomerID 等於 3 的資料列。  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
   Response.write "Connect String = " & sConn & "<BR/>"  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
   adoConn.Open  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
   Response.write "Query String = " & sQuery & "<BR/>"  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
%>  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
</SCRIPT>  
</HEAD>  
<BODY>  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
```  
  
 此範例 ASP 頁面包含伺服器端 VBScript，它使用 ADO 來執行 FOR XML 查詢，並在 XML 資料島 MyDataIsle 內傳回 XML 結果。 然後此 XML 資料島會傳回瀏覽器中，以進行其他用戶端處理。 接著，會使用其他用戶端 VBScript 程式碼來處理 XML 資料島的內容。 執行此程序之後，才會將內容顯示為結果 DHTML 的一部份，並開啟訊息方塊來顯示 XML 資料島之預先處理過的內容。  
  
#### <a name="to-test-this-example"></a>若要測試此範例  
  
1.  確認已安裝 IIS，而且也為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝了 AdventureWorks 範例資料庫。  
  
     此範例需要安裝 Internet Information Services (IIS) 5.0 版或更新版本，並已啟用 ASP 支援。 同時，也必須安裝 AdventureWorks 範例資料庫。  
  
2.  複製先前提供的程式碼範例，並將它貼到 XML 或您使用的文字編輯器中。 以 RetrieveResults.asp 的名稱，將檔案另存於 IIS 使用的根目錄中。 此目錄通常是 C:Inetpub\wwwroot。  
  
3.  使用下列 URL，在瀏覽器視窗中開啟 ASP 頁面。 首先，將 'MyServer' 取代成 "localhost" 或安裝了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 IIS 之伺服器的實際名稱。  
  
    ```  
    http://MyServer/RetrieveResults.asp  
    ```  
  
 產生的 HTML 頁面結果類似下列範例輸出：  
  
##### <a name="server-side-processing"></a>伺服器端處理  
 Page Generated @ 3/11/2006 3:36:02 PM  
  
 Connect String = Provider=SQLOLEDB;Data Source=MyServer;Initial Catalog=AdventureWorks;Integrated Security=SSPI;  
  
 ADO Version = 2.8  
  
 adoConn.State = 1  
  
 Query String = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 將 XML 發送至用戶端進行處理  
  
##### <a name="client-side-processing-of-xml-document-mydataisle"></a>XML 文件 MyDataIsle 的用戶端處理  
  
-   **AnnualSales:** 1500000  
  
-   **AnnualRevenue:** 150000  
  
-   **BankName:** Primary International  
  
-   **BusinessType:** OS  
  
-   **YearOpened:** 1974  
  
-   **Specialty:** Road  
  
-   **SquareFeet:** 38000  
  
-   **Brands:** 3  
  
-   **Internet:** DSL  
  
-   **NumberEmployees:** 40  
  
 VBScript 訊息方塊會顯示下列由 FOR XML 查詢結果所傳回之原始而未篩選過的 XML 資料島內容。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
      <StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
        <AnnualSales>1500000</AnnualSales>  
        <AnnualRevenue>150000</AnnualRevenue>  
        <BankName>Primary International</BankName>  
        <BusinessType>OS</BusinessType>  
        <YearOpened>1974</YearOpened>  
        <Specialty>Road</Specialty>  
        <SquareFeet>38000</SquareFeet>  
        <Brands>3</Brands>  
        <Internet>DSL</Internet>  
        <NumberEmployees>40</NumberEmployees>  
      </StoreSurvey>  
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## <a name="retrieving-for-xml-data-with-aspnet-and-the-net-framework"></a>使用 ASP.NET 和 .NET Framework 來擷取 FOR XML 資料  
 如前一範例所示，下列 ASP.NET 程式碼顯示在 AdventureWorks 範例資料庫的 Sales.Store 資料表中查詢 **xml** 資料類型資料行 Demographics 的結果。 如前一範例所示，此查詢會在此資料行的執行個體值中尋找 CustomerID 等於 3 的資料列。  
  
 在此範例中，使用了下列 Microsoft .NET Framework 管理的 API 來完成 FOR XML 查詢結果的傳回和轉譯作業：  
  
1.  **SqlConnection** 用來開啟 SQL Server 的連接，並以指定之連接字串變數 strConn 的內容為基礎。  
  
2.  **SqlDataAdapter** 則做為資料配接器使用，它使用 SQL 連接和指定的 SQL 查詢字串來執行 FOR XML 查詢。  
  
3.  執行查詢之後，會呼叫 **SqlDataAdapter.Fill** 方法，並傳遞 **DataSet,** 的執行個體 (MyDataSet)，以便在資料集內填入 FOR XML 查詢的輸出。  
  
4.  接著會呼叫 **DataSet.GetXml** 方法，將查詢結果當作可在伺服器所產生 HTML 頁面中顯示的字串，予以傳回。  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
    <TITLE>FOR XML Query Example</TITLE>  
    <STYLE>  
       BODY  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
       H3  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
    </STYLE>  
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### <a name="to-test-this-example"></a>若要測試此範例  
  
1.  確認已安裝 IIS，而且也為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝了 AdventureWorks 範例資料庫。  
  
     此範例需要安裝 Internet Information Services (IIS) 5.0 版或更新版本，並已啟用 ASP.NET 支援。 同時，也必須安裝 AdventureWorks 範例資料庫。  
  
2.  複製先前提供的程式碼，並將它貼到 XML 或您使用的文字編輯器中。 以 RetrieveResults.asp 的名稱，將檔案另存於 IIS 使用的根目錄中。 此目錄通常是 C:Inetpub\wwwroot。  
  
3.  使用下列 URL，在瀏覽器視窗中開啟 ASP.NET 頁面。 首先，將 'MyServer' 取代成 "localhost" 或安裝了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 IIS 之伺服器的實際名稱。  
  
    ```  
    http://MyServer/RetrieveResults.aspx  
    ```  
  
 產生的 HTML 頁面結果類似下列範例輸出：  
  
##### <a name="server-side-processing"></a>伺服器端處理  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**XML** 資料類型支援可讓您藉由指定 **TYPE 指示詞** ，要求以 [XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md)資料類型的形式傳回 FOR XML 查詢的結果，而不以字串或影像類型資料的形式傳回。 如果在 FOR XML 查詢中使用了 TYPE 指示詞時，它會提供以程式方式存取 FOR XML 結果 (類似 [在應用程式中使用 XML 資料](../../relational-databases/xml/use-xml-data-in-applications.md)中所顯示)。  
  
## <a name="see-also"></a>另請參閱  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
