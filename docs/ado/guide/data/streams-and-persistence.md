---
title: 資料流和保存 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22fbf503196c467a7816bf4e9c76151276cc6d4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924023"
---
# <a name="streams-and-persistence"></a>資料流和保存
[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件[儲存](../../../ado/reference/ado-api/save-method.md)方法存放區，或*持續發生*，則**資料錄集**在檔案中，而[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法還原**資料錄集**從該檔案。  
  
 搭配 ADO 2.7 或更新版本，**儲存**並**開啟**方法可以保存**資料錄集**至[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件以及。 使用遠端資料服務 (RDS) 與 Active Server Pages (ASP) 時，這項功能是特別有用。  
  
 如需如何持續可供本身在 ASP 網頁上的詳細資訊，請參閱新的 ASP 文件。  
  
 以下是幾個案例，示範如何**Stream**可以使用物件和持續性。  
  
## <a name="scenario-1"></a>實例 1  
 這種情況下只會儲存**Recordset**檔案，然後**Stream**。 接著它會開啟永續性資料流到另一個**資料錄集**。  
  
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
 這種情況下仍然存在**Recordset**到**Stream**以 XML 格式。 它接著會讀取**Stream**轉換為字串，您可以檢查、 操作或顯示。  
  
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
 此程式碼範例顯示 ASP 程式碼保存**Recordset**為以 XML 直接**回應**物件：  
  
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
 在此案例中，ASP 程式碼的內容寫入**資料錄集**ADTG 格式，用戶端。 [OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)可以使用此資料來建立已中斷連接**資料錄集**。  
  
 在 RDS 上新的屬性[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)， [URL](../../../ado/reference/rds-api/url-property-rds.md)，指向 產生.asp 頁面**資料錄集**。 這表示**Recordset**可以取得物件而不需要 RDS 使用伺服器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件或使用者撰寫的商務物件。 這可大幅簡化 RDS 程式設計模型。  
  
 伺服器端程式碼中，名為 https://server/directory/recordset.asp:  
  
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
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
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
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
