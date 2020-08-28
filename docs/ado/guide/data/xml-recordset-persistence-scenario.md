---
description: XML 資料錄集保存案例
title: XML 記錄集持續性案例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: rothja
ms.author: jroth
ms.openlocfilehash: 91066d8dd42d1bcd4a11aab093661a9061a7d7d1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978819"
---
# <a name="xml-recordset-persistence-scenario"></a>XML 資料錄集保存案例
在此案例中，您將建立 Active Server Pages (ASP) 應用程式，將記錄集物件的內容直接儲存至 ASP 回應物件。  
  
> [!NOTE]
>  此案例要求您的伺服器必須已安裝 Internet information Server 5.0 (IIS) 或更新版本。  
  
 傳回的記錄集會使用 [DataControl 物件 (RDS) ](../../reference/rds-api/datacontrol-object-rds.md)顯示在 Internet Explorer 中。  
  
 若要建立此案例，必須執行下列步驟：  
  
-   設定應用程式  
  
-   取得資料  
  
-   傳送資料  
  
-   接收及顯示資料  
  
## <a name="step-1-set-up-the-application"></a>步驟1：設定應用程式  
 使用腳本許可權，建立名為 "XMLPersist" 的 IIS 虛擬目錄。 在虛擬目錄指向的資料夾中建立兩個新的文字檔，一個名為 "XMLResponse"，另一個名為 "Default.htm"。  
  
## <a name="step-2-get-the-data"></a>步驟2：取得資料  
 在此步驟中，您將撰寫程式碼來開啟 ADO 記錄集，並準備將它傳送至用戶端。 使用文字編輯器（例如 [記事本]）開啟檔案 XMLResponse，然後插入下列程式碼。  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 請務必將中的參數值變更 `Data Source` `strCon` 為 Microsoft SQL Server 電腦的名稱。  
  
 讓檔案保持開啟，然後繼續進行下一個步驟。  
  
## <a name="step-3-send-the-data"></a>步驟3：傳送資料  
 現在您有了記錄集，您必須將它以 XML 形式儲存至 ASP 回應物件，以將其傳送至用戶端。 將下列程式碼新增至 XMLResponse 的底部。  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 請注意，ASP 回應物件指定為記錄集 [儲存方法](../../reference/ado-api/save-method.md)的目的地。 Save 方法的目的地可以是任何支援 IStream 介面的物件，例如 ado [資料流程物件 (ado) ](../../reference/ado-api/stream-object-ado.md)，或是包含要儲存記錄集之完整路徑的檔案名。  
  
 請先儲存並關閉 XMLResponse，然後再繼續進行下一個步驟。 此外，請從預設的 ADO 程式庫安裝資料夾將 adovbs 檔案複製到您儲存 XMLResponse .asp 檔案的相同資料夾。  
  
## <a name="step-4-receive-and-display-the-data"></a>步驟4：接收和顯示資料  
 在這個步驟中，您將建立一個 HTML 檔案，其中包含內嵌 [DataControl 物件 (RDS) ](../../reference/rds-api/datacontrol-object-rds.md) 物件，該物件指向 XMLResponse .asp 檔案以取得記錄集。 使用文字編輯器（例如 [記事本]）開啟 default.htm，然後加入下列程式碼。 將 URL 中的 "sqlserver" 取代為您的伺服器名稱。  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 關閉 default.htm 的檔案，並將它儲存到您儲存 XMLResponse 的相同資料夾中。 使用 Internet Explorer 4.0 或更新版本，開啟 HTTPs://*sqlserver*/XMLPersist/default.htm 的 URL，並觀察結果。 資料會顯示在系結的 DHTML 資料表中。 現在開啟 URL HTTPs:// *sqlserver* /XMLPersist/XMLResponse.asp 並觀察結果。 XML 隨即顯示。  
  
## <a name="see-also"></a>另請參閱  
 [Save 方法](../../reference/ado-api/save-method.md)   
 [以 XML 格式保存記錄](./persisting-records-in-xml-format.md)