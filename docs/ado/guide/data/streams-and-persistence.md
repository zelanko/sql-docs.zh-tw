---
title: "資料流和持續性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: af1ecf7ed9f4702d986d6f1881b3264ab8171c87
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="streams-and-persistence"></a>資料流和持續性
[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件[儲存](../../../ado/reference/ado-api/save-method.md)方法存放區，或*持續發生*、**資料錄集**在檔案中，而[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法還原**資料錄集**從該檔案。  
  
 以 ADO 2.7 或更新版本，**儲存**和**開啟**方法可以保存**資料錄集**至[資料流](../../../ado/reference/ado-api/stream-object-ado.md)以及物件。 使用遠端資料服務 (RDS) 和 Active Server Pages (ASP) 時，這項功能會很實用。  
  
 如需有關如何持續性可由本身 ASP 網頁上的詳細資訊，請參閱目前 ASP 文件。  
  
 以下是幾個案例示範如何**資料流**可以使用物件和持續性。  
  
## <a name="scenario-1"></a>實例 1  
 此案例只儲存**資料錄集**到檔案，然後以**資料流**。 接著它會開啟永續性資料流到另一個**資料錄集**。  
  
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
 這種情況下仍然存在**資料錄集**到**資料流**以 XML 格式。 它接著會讀取**資料流**成字串，您可以檢查、 操作或顯示。  
  
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
 這個程式碼範例顯示 ASP 程式碼保存**資料錄集**為直接 XML 至**回應**物件：  
  
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
 在此案例中，ASP 程式碼的內容寫入**資料錄集**ADTG 格式，用戶端。 [Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)可以使用此資料來建立已中斷連線**資料錄集**。  
  
 新的屬性上 RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)， [URL](../../../ado/reference/rds-api/url-property-rds.md)，指向產生的.asp 頁面**資料錄集**。 這表示**資料錄集**物件可透過 RDS 不使用伺服器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件或使用者撰寫的商務物件。 這樣可大幅簡化 RDS 程式設計模型。  
  
 伺服器端程式碼中，名為 http://server/directory/recordset.asp:  
  
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
  
 用戶端程式碼：  
  
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
    <PARAM NAME="URL" VALUE="http://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 開發人員也可以選擇使用**資料錄集**用戶端上的物件：  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "http://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)

