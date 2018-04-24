---
title: 擷取結果集資料流 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16d1518d2ddbe5accc6b55fdc0b778a6381e1a5f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="retrieving-resultsets-into-streams"></a>擷取結果集資料流
而不是在傳統收到結果**資料錄集**物件、 ADO 可以改成資料流擷取查詢結果。 ADO**資料流**物件 (或其他物件，支援 COM **IStream**介面，例如 ASP**要求**和**回應**物件) 可用來包含這些結果。 這項功能的一個用法是擷取 XML 格式的結果。 與 SQL Server，例如 XML 結果可以傳回以多種方式，例如 SQL SELECT 查詢中使用 FOR XML 子句，或使用 XPath 查詢。  
  
 在資料流的格式，而不是在接收查詢結果**資料錄集**，您必須指定**adExecuteStream**常數從**的執行方式**為的參數**Execute**方法**命令**物件。 如果您的提供者會支援這項功能，將會在執行時，資料流中傳回結果。 您可能必須執行的程式碼之前，請指定其他提供者特有的屬性。 例如，使用 Microsoft OLE DB Provider for SQL Server，例如屬性**輸出資料流**中**屬性**集合**命令**物件必須是指定。 如需這項功能相關的 SQL Server 特有動態屬性的詳細資訊，請參閱 SQL Server 線上叢書 》 中的 XML-Related 屬性。  
  
## <a name="for-xml-query-example"></a>如需 XML 的查詢範例  
 下列範例是以 VBScript 與 Northwind 資料庫：  
  
```  
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
  
 FOR XML 子句指示 XML 文件的形式傳回資料的 SQL Server。  
  
### <a name="for-xml-syntax"></a>XML 語法  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FOR XML RAW 會產生具有屬性的資料行值的一般資料列項目。 FOR XML AUTO 會使用啟發學習法來產生階層樹狀結構與資料表名稱為基礎的項目名稱。 FOR XML EXPLICIT 會通用資料表產生完整中繼資料描述之關聯性。  
  
 範例 SQL SELECT FOR XML 陳述式如下：  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 可以在字串中指定的命令，如下所示更早版本，指派給**CommandText**，或指派給 XML 範本查詢形式**CommandStream**。 如需有關 XML 範本查詢的詳細資訊，請參閱[命令資料流](../../../ado/guide/data/command-streams.md)ADO 或使用 SQL Server 線上叢書 》 中的命令輸入資料流中。  
  
 為 XML 範本查詢，FOR XML 查詢會顯示如下：  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 這個範例會指定 ASP**回應**物件**輸出資料流**屬性：  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 接下來，指定**adExecuteStream**參數**Execute**。 這個範例會包裝 XML 標記，來建立 XML 資料島中的資料流：  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>備註  
 此時，已經傳送串流到用戶端瀏覽器的 XML，而且準備好可以顯示。 這是經由使用用戶端 VBScript 繫結至 DOM 和迴圈每個子節點，以建立 HTML 中的產品清單的執行個體的 XML 文件。
