---
title: URL 屬性範例 (VBScript) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- URL property [ADO], VBScript example
ms.assetid: 6ae5ac50-c88c-4262-b7ab-f2b3de382a0b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 663cac5f83608b5a0a100a3f5bc33dc94e3023db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697235"
---
# <a name="url-property-example-vbscript"></a>URL 屬性範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列程式碼示範如何設定**URL**指定.asp 檔案會接著處理變更提交至資料來源的用戶端上的屬性。  
  
```  
<!-- BeginURLClientVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>URL Property Example (VBScript)</title>  
<style>  
<!--  
body {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</style>  
</head>  
  
<body onload=Getdata()>  
<h1>URL Property Example (VBScript)</h1>  
<OBJECT classid=clsid:BD96C556-65A3-11D0-983A-00C04FC29E33 height=1 id=ADC width=1>  
</OBJECT>  
  
<table datasrc="#ADC" align="center">  
<thead>  
<tr id="ColHeaders" class="thead2">  
   <th>FirstName</th>  
   <th>LastName</th>  
   <th>Extension</th>  
</tr>  
</thead>  
<tbody class="tbody">  
<tr>  
   <td><input datafld="FirstName" size=15> </td>  
   <td><input datafld="LastName" size=25> </td>  
   <td><input datafld="Extension" size=15> </td>  
</tr>  
</tbody>  
</table>  
  
<script Language="VBScript">  
Sub Getdata()  
  
      ADC.URL = "https://MyServer/URLServerVBS.asp"  
      ADC.Refresh  
End Sub  
  
</script>  
  
</body>  
</html>  
<!-- EndURLClientVBS -->  
```  
  
 伺服器端程式碼存在於**URLServerVBS.asp**提交更新**資料錄集**到資料來源。  
  
```  
<!-- BeginURLServerVBS -->  
<%@ Language=VBScript %>  
<%  
  
        ' XML output req's  
    Response.ContentType = "text/xml"  
    const adPersistXML  = 1  
  
        ' recordset vars  
    Dim strSQL, rsEmployees   
    Dim strCnxn, Cnxn  
  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    Set rsEmployees = Server.CreateObject("ADODB.Recordset")  
  
    strSQL = "SELECT FirstName, LastName, Extension FROM Employees"  
  
    Cnxn.Open strCnxn  
    rsEmployees.Open strSQL, Cnxn  
  
        ' output as XML  
    rsEmployees.Save Response, adPersistXML  
  
        ' Clean up  
    rsEmployees.Close  
    Cnxn.Close  
    Set rsEmployees = Nothing  
    Set Cnxn = Nothing  
%>  
<!-- EndURLServerVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [URL 屬性 (RDS)](../../../ado/reference/rds-api/url-property-rds.md)


