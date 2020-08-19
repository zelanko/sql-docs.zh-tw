---
description: 將結果集擷取為資料流
title: 正在將結果集取出至資料流程 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 53dcb66eb2abb311b1114928a8696c6502454770
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452920"
---
# <a name="retrieving-resultsets-into-streams"></a>將結果集擷取為資料流
ADO 可以改為將查詢結果取出至資料流程，而不是在傳統 **記錄集** 物件中接收結果。 ADO **資料流程** 物件 (或其他支援 COM **IStream** 介面的物件，例如 ASP **要求** 和 **回應** 物件) 可以用來包含這些結果。 這項功能的其中一個用途是取得 XML 格式的結果。 例如，有了 SQL Server，就可以用多種方式傳回 XML 結果，例如搭配使用 FOR XML 子句和 SQL SELECT 查詢，或使用 XPath 查詢。  
  
 若要接收串流格式的查詢結果，而不**是記錄集**，您必須將**ExecuteOptionEnum**中的**adExecuteStream**常數指定為**Command**物件之**Execute**方法的參數。 如果您的提供者支援這項功能，則會在執行時于資料流程中傳回結果。 在程式碼執行之前，您可能需要指定其他提供者特定的屬性。 例如，使用適用于 SQL Server 的 Microsoft OLE DB 提供者時，必須指定**命令**物件的**properties**集合中的屬性，例如**輸出資料流程**。 如需這項功能的相關 SQL Server 特定動態屬性的詳細資訊，請參閱 SQL Server 線上叢書中的 XML 相關屬性。  
  
## <a name="for-xml-query-example"></a>FOR XML 查詢範例  
 下列範例是以 VBScript 撰寫給 Northwind 資料庫：  
  
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
  
 FOR XML 子句會指示 SQL Server 傳回 XML 檔案格式的資料。  
  
### <a name="for-xml-syntax"></a>FOR XML 語法  
  
```syntax
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 FOR XML RAW 會產生具有資料行值做為屬性的泛型資料列元素。 FOR XML AUTO 使用啟發學習法來產生階層式樹狀結構，其中包含以資料表名稱為基礎的元素名稱。 FOR XML EXPLICIT 產生的通用資料表具有由中繼資料完整描述的關聯性。  
  
 SQL SELECT FOR XML 語句的範例如下：  
  
```sql
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 您可以如先前所示、指派給 **CommandText**，或以指派給 **CommandStream**的 XML 範本查詢形式，在字串中指定命令。 如需 XML 範本查詢的詳細資訊，請參閱 ADO 中的 [命令資料流程](../../../ado/guide/data/command-streams.md) 或在 SQL Server 線上叢書中使用命令輸入的資料流程。  
  
 XML 範本查詢的 FOR XML 查詢會如下所示：  
  
```xml
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 這個範例會指定**輸出資料流程**屬性的 ASP**回應**物件：  
  
```vb
adoCmd.Properties("Output Stream") = Response  
```  
  
 接下來，指定**Execute**的**adExecuteStream**參數。 此範例會將資料流程包裝在 XML 標記中，以建立 XML 資料島：  
  
```vb
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>備註  
 至此，XML 已串流至用戶端瀏覽器，而且已可供顯示。 這是藉由使用用戶端 VBScript 將 XML 檔系結至 DOM 的實例來完成，並在每個子節點之間迴圈，以建立 HTML 的產品清單。
