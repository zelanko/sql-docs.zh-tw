---
title: XML 資料錄集保存案例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 252df4b5133861b6ff9892600bfe1c53206fefec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789216"
---
# <a name="xml-recordset-persistence-scenario"></a>XML 資料錄集保存案例
在此案例中，您將建立 Active Server Pages (ASP) 應用程式，直接將資料錄集物件的內容將 ASP 回應物件。  
  
> [!NOTE]
>  此案例需要，您的伺服器安裝 Internet Information Server 5.0 (IIS) 或更新版本。  
  
 傳回的資料錄集隨即出現在 Internet Explorer 中使用[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)。  
  
 建立此案例所需的下列步驟︰  
  
-   設定應用程式  
  
-   取得資料  
  
-   將資料傳送  
  
-   接收並顯示資料  
  
## <a name="step-1-set-up-the-application"></a>步驟 1： 設定應用程式  
 建立名為"XMLPersist 」 指令碼的權限的 IIS 虛擬目錄。 虛擬目錄指向，一個具名"XMLResponse.asp，「 其他具名"Default.htm。 」 的資料夾中建立兩個新的文字檔案  
  
## <a name="step-2-get-the-data"></a>步驟 2： 取得資料  
 在此步驟中，您將撰寫程式碼以開啟 ADO 資料錄集，並準備將它傳送至用戶端。 開啟檔案 XMLResponse.asp 使用文字編輯器，例如 [記事本]，並插入下列程式碼。  
  
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
  
 請務必變更的值`Data Source`中的參數`strCon`為您的 Microsoft SQL Server 電腦的名稱。  
  
 開啟，請移至下一個步驟，請保留的檔案。  
  
## <a name="step-3-send-the-data"></a>步驟 3： 將資料傳送  
 有了資料錄集之後，您必須用戶端傳送以 xml 格式儲存的 ASP 回應物件。 將下列程式碼新增至 XMLResponse.asp 底部。  
  
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
  
 請注意，ASP 回應物件會指定為資料錄集目的地[Save 方法](../../../ado/reference/ado-api/save-method.md)。 Save 方法的目的地可以是任何物件支援的 IStream 介面，例如 ADO [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)，或檔案名稱，其中包含有要儲存的資料錄集的完整路徑。  
  
 儲存並關閉 XMLResponse.asp 再移至下一個步驟。 也將 adovbs.inc 檔案從預設的 ADO 程式庫安裝資料夾複製到您儲存 XMLResponse.asp 檔案相同的資料夾。  
  
## <a name="step-4-receive-and-display-the-data"></a>步驟 4： 接收及顯示資料  
 您將在此步驟中建立 HTML 檔案與內嵌[DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) XMLResponse.asp 檔案，以取得資料錄集所指向的物件。 使用文字編輯器，例如 [記事本]，開啟 default.htm，並新增下列程式碼。 在 URL 中的"sqlserver"取代為您伺服器的名稱。  
  
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
  
 關閉 default.htm 檔案，並將它儲存到您用來儲存 XMLResponse.asp 相同的資料夾。 使用 Internet Explorer 4.0 或更新版本中，開啟 URL http://*sqlserver*/XMLPersist/default.htm，並觀察結果。 資料會顯示在 繫結的 DHTML 資料表。 現在開啟 URL http:// *sqlserver* /XMLPersist/XMLResponse.asp，並觀察結果。 XML 會顯示。  
  
## <a name="see-also"></a>另請參閱  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)   
 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)
