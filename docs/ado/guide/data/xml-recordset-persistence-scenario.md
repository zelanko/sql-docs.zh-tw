---
title: XML 資料錄集持續性案例 |Microsoft 文件
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
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4aa455c004305f1350fef0006ba1986932ea692c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="xml-recordset-persistence-scenario"></a>持續性案例中 XML 資料錄集
在此案例中，您將建立資料錄集物件的內容直接將 ASP 回應物件的 Active Server Pages (ASP) 應用程式。  
  
> [!NOTE]
>  此案例需要，您的伺服器安裝 Internet Information Server 5.0 (IIS) 或更新版本。  
  
 傳回的資料錄集隨即在 Internet Explorer 中使用[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)。  
  
 下列步驟建立所需此案例中：  
  
-   設定應用程式  
  
-   取得資料  
  
-   傳送資料  
  
-   接收和顯示資料  
  
## <a name="step-1-set-up-the-application"></a>步驟 1： 設定應用程式  
 建立名為"XMLPersist 」 指令碼的權限的 IIS 虛擬目錄。 虛擬目錄指向，一個具名"XMLResponse.asp，「 其他具名"Default.htm。 」 的資料夾中建立兩個新的文字檔  
  
## <a name="step-2-get-the-data"></a>步驟 2： 取得資料  
 在此步驟中，您將撰寫開啟 ADO 資料錄集，並準備將它傳送至用戶端程式碼。 使用記事本之類的文字編輯器開啟檔案 XMLResponse.asp，插入下列程式碼。  
  
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
  
 請務必變更的值`Data Source`中的參數`strCon`Microsoft SQL Server 電腦的名稱。  
  
 保留的檔案，開啟，請移至下一個步驟。  
  
## <a name="step-3-send-the-data"></a>步驟 3： 將資料傳送  
 有一個資料錄集之後，您必須用戶端傳送至 ASP 回應物件儲存為 XML。 將下列程式碼加入至 XMLResponse.asp 底部。  
  
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
  
 請注意，ASP 回應物件會指定為資料錄集目的地[Save 方法](../../../ado/reference/ado-api/save-method.md)。 Save 方法目的地可以是任何物件支援 IStream 介面，例如 ADO[資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)，或包含資料錄集是儲存的完整路徑的檔案名稱。  
  
 儲存並關閉 XMLResponse.asp 再繼續下一個步驟。 也將 adovbs.inc 檔案從預設 ADO 程式庫安裝資料夾複製到儲存 XMLResponse.asp 檔案的相同資料夾。  
  
## <a name="step-4-receive-and-display-the-data"></a>步驟 4： 接收和顯示資料  
 在此步驟會建立 HTML 檔案與內嵌[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) XMLResponse.asp 檔案，以取得資料錄集所指向的物件。 使用文字編輯器，例如 [記事本]，開啟 default.htm 並加入下列程式碼。 在 URL 中的"sqlserver"取代為您的伺服器名稱。  
  
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
  
 關閉 default.htm 檔案，並將它儲存到儲存 XMLResponse.asp 的相同資料夾。 使用 Internet Explorer 4.0 或更新版本中，開啟 URL http://*sqlserver*/XMLPersist/default.htm，並觀察結果。 資料會顯示在 繫結的 DHTML 資料表。 現在開啟 URL http:// *sqlserver* /XMLPersist/XMLResponse.asp，並觀察結果。 則會顯示 XML。  
  
## <a name="see-also"></a>另請參閱  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)   
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
