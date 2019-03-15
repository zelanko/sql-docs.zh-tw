---
title: 將資料流結果集擷取 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad9c21deb365428a6642f3ee9b7f48396d7c4f9
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57973497"
---
# <a name="retrieving-resultsets-into-streams"></a>將結果集擷取為資料流
而不是接收結果中的典型**資料錄集**物件時，ADO 可以改為擷取成資料流的查詢結果。 ADO **Stream**物件 (或其他物件，支援 COM **IStream**介面，例如 ASP**要求**並**回應**物件) 可以用來包含這些結果。 這項功能的其中一種用法是擷取 XML 格式的結果。 使用 SQL Server，比方說，XML 結果可以傳回以多種方式，例如使用 SQL SELECT 查詢中使用 FOR XML 子句，或使用 XPath 查詢。  
  
 資料流格式，而不是在接收查詢結果**資料錄集**，您必須指定**adExecuteStream**從常數**的執行方式**的參數**Execute**方法**命令**物件。 如果您的提供者支援這項功能，則會在執行時的資料流中傳回結果。 您可能必須執行的程式碼之前，請指定其他提供者特有的屬性。 例如，使用 Microsoft OLE DB Provider for SQL Server，這類的屬性**輸出 Stream**中**屬性**集合**命令**物件必須是指定此項目。 如需這項功能與相關的 SQL Server 特定動態屬性的詳細資訊，請參閱 < SQL Server 線上叢書 》 中的 XML-Related 屬性。  
  
## <a name="for-xml-query-example"></a>FOR XML 查詢範例  
 下列範例是以 VBScript 與 Northwind 資料庫：  
  
```html
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
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
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
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
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
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
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
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
  
 FOR XML 子句會指示 XML 文件的形式傳回資料的 SQL Server。  
  
### <a name="for-xml-syntax"></a>如需 XML 語法  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FOR XML RAW 會產生具有屬性的資料行值的泛型資料列項目。 FOR XML AUTO 會使用啟發學習法來產生階層式樹狀結構有根據資料表名稱的項目名稱。 FOR XML EXPLICIT 會產生一個通用資料表關聯性的中繼資料的完整說明。  
  
 SQL SELECT FOR XML 陳述式範例如下：  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 可以在字串中指定的命令，之前所示，指派給**CommandText**，或在 XML 範本查詢指派給表單**CommandStream**。 如需有關 XML 範本查詢的詳細資訊，請參閱 <<c0> [ 命令資料流](../../../ado/guide/data/command-streams.md)ADO 或使用 SQL Server 線上叢書 》 中的命令輸入的資料流中。  
  
 為 XML 範本查詢，FOR XML 查詢看起來像這樣：  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 這個範例會指定 ASP**回應**物件**輸出 Stream**屬性：  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 接下來，指定**adExecuteStream**的參數**Execute**。 此範例會包裝 XML 標記來建立 XML 資料島中的資料流：  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>備註  
 此時，已串流處理至用戶端瀏覽器的 XML，而且準備好可以顯示。 這是由繫結至 DOM 和循環使用每個子節點，來建置一份產品在 HTML 中的執行個體的 XML 文件中使用用戶端 VBScript。
