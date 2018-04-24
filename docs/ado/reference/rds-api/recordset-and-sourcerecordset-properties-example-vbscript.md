---
title: 資料錄集和 SourceRecordset 屬性範例 (VBScript) |Microsoft 文件
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Source property [ADO], VBScript example
- Recordset property [ADO], VBScript example
ms.assetid: 95175316-cd10-4cf7-96ba-2a226fd97701
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 23748908966cc2aaae3b747844308e7021392b5a
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="recordset-and-sourcerecordset-properties-example-vbscript"></a>資料錄集和 SourceRecordset 屬性範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列範例示範如何設定必要的參數[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)預設商務物件，在執行階段。  
  
 若要測試此範例中，剪下並貼上這段程式碼之間\<主體 > 和\</b > 標記以標準 HTML 文件並將其命名**RecordsetVBS.asp**。 ASP 指令碼會找出您的伺服器。  
  
```  
<!-- BeginRecordSetVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Recordset and SourceRecordset Properties Example (VBScript)</title>  
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
  
<body>  
<h1>Recordset and SourceRecordset Properties Example (VBScript)</h1>  
  
<Center>  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using SourceRecordset and Recordset with RDSServer.DataFactory</H3>  
<!-- RDS.DataSpace ID RDS1 -->  
<OBJECT ID="RDS1" WIDTH=1 HEIGHT=1   
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters set at Run Time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDC WIDTH=1 HEIGHT=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDC>  
   <TR>  
      <TD> <INPUT DATAFLD="FirstName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="LastName" SIZE=15></TD>  
   </TR>  
</TABLE>  
<HR>  
<Input Size=70 Name="txtServer" Value="http://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
<Input Size=70 Name="txtConnect" Value="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'"><BR>  
<Input Size=70 Name="txtSQL" Value="SELECT FirstName, LastName FROM Employees">  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run"><BR>  
  
</Center>  
<Script Language="VBScript">  
  
   Dim rdsDF  
   Dim strServer  
   strServer = "http://<%=Request.ServerVariables("SERVER_NAME")%>"  
  
   Sub Run_OnClick()  
  
      Dim rs           
      ' Create RDSServer.DataFactory Object  
      Set rdsDF = RDS1.CreateObject("RDSServer.DataFactory", strServer)                 
      ' Get Recordset  
      Set rs = rdsDF.Query(txtConnect.Value,txtSQL.Value)  
  
      ' Set parameters of RDS.DataControl at run time  
      RDC.Server = txtServer.Value  
      RDC.SQL = txtSQL.Value  
      RDC.Connect = txtConnect.Value  
      RDC.Refresh  
  
   End Sub  
  
</Script>  
  
</body>  
</html>  
<!-- EndRecordsetVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Recordset、SourceRecordset 屬性 (RDS)](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md)



