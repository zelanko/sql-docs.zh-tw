---
description: 資料流和保存
title: 資料流程和持續性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: rothja
ms.author: jroth
ms.openlocfilehash: 60e006733fd8ef5bd958328420ab43c1cbabc50e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979419"
---
# <a name="streams-and-persistence"></a>資料流和保存
[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件[Save](../../../ado/reference/ado-api/save-method.md)方法會儲存或保存檔案中的**記錄集** *，而* [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法會從該檔案還原**記錄集**。  
  
 使用 ADO 2.7 或更新版本時， **儲存** 和 **開啟** 方法也可以將 **記錄集** 保存到 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件。 當使用遠端資料服務 (RDS) 和 (ASP) 的 Active Server 頁面時，這項功能特別有用。  
  
 如需有關如何在 ASP 頁面上自行使用持續性的詳細資訊，請參閱目前的 ASP 檔集。  
  
 以下是一些示範如何使用 **資料流程** 物件和持續性的案例。  
  
## <a name="scenario-1"></a>實例 1  
 這種情況只會將 **記錄集** 儲存至檔案，然後儲存至 **資料流程**。 然後，它會將保存的資料流程開啟至另一個 **記錄集**。  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>案例 2  
 此案例會將 **記錄集** 保存為 XML 格式的 **資料流程** 。 然後，它會將 **串流** 讀入可供您檢查、操作或顯示的字串中。  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>案例 3  
 此範例程式碼會顯示 ASP 程式碼將 **記錄集** 以 XML 形式直接保存到 **回應** 物件：  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>案例 4  
 在此案例中，ASP 程式碼會以 ADTG 格式將 **記錄集** 的內容寫入至用戶端。 [適用于 OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)可以使用此資料來建立已中斷連線的**記錄集**。  
  
 RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) [URL](../../../ado/reference/rds-api/url-property-rds.md)上的新屬性會指向產生 **記錄集**的 .asp 頁面。 這表示您可以使用伺服器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件或撰寫商務物件的使用者，取得不含 RDS 的**記錄集**物件。 這可大幅簡化 RDS 程式設計模型。  
  
 伺服器端程式碼，名為 https://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 用戶端程式代碼：  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 開發人員也可以選擇在用戶端上使用 **記錄集** 物件：  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO 記錄集的 Open 方法) ](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [ (ADO) 的記錄物件 ](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
