---
title: Refresh 方法範例 (VBScript) |Microsoft Docs
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
- Refresh method [ADO], VBScript example
ms.assetid: f2926578-bc60-464b-916e-ddfdb8014253
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcb4ccd685a5f28377972db03d32496017bda8cd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731217"
---
# <a name="refresh-method-example-vbscript"></a>Refresh 方法範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列範例示範如何設定必要的參數的[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)在執行階段。 方法[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)會使用擷取[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法取決於設定[ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md)和[FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md)屬性。 若要測試此範例中，剪下並貼入正常的 ASP 文件中的下列程式碼並將它命名**RefreshVBS.asp**。 使用 **尋找**找出檔案 Adovbs.inc，並將它放在您打算使用的目錄。 ASP 指令碼會識別您的伺服器。  
  
```  
<!-- BeginRefreshVBS -->  
<%@ Language=VBScript %>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Refresh Method Example (VBScript)</title>  
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
<h1>Refresh Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples </H2>  
<HR>  
<TABLE DATASRC=#RDC>  
   <TR>  
      <TD> <INPUT DATAFLD="FirstName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="LastName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="Title" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="HireDate" SIZE=15> </TD>  
   </TR>  
</TABLE>  
  
<!-- RDS.DataControl with no parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDC HEIGHT=1 WIDTH=1>  
</OBJECT>  
<HR>  
Server: <Input Size=70 Name="txtServer" Value="http://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
Connect: <Input Size=70 Name="txtConnect" Value="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'"><BR>  
SQL: <Input Size=70 Name="txtSQL" Value="Select * from Employees">  
<HR>  
<TABLE BORDER=1 WIDTH="60%">  
<TR>  
   <TD COLSPAN=3 BGCOLOR=silver>  
   Choose if you want the Recordset brought back Synchronously on the   
   current calling thread or Asynchronously on another thread.   
   </TD>  
</TR>  
<TR>  
   <TD>Synchronously: <BR>  
      <Input Type="Radio" Name="optExecuteOptions" Checked OnClick="SetExO('adcExecSync')">  
   </TD>  
   <TD>Asynchronously: <BR>  
      <Input Type="Radio" Name="optExecuteOptions"  OnClick="SetExO('adcExecAsync')">  
   </TD>  
   <TD> </TD>  
</TR>  
<TR>  
   <TD COLSPAN=3 BGCOLOR=silver>  
   Fetch Up Front, Background Fetch with Blocking or Background Fetch   
   without Blocking   
   </TD>  
<TR>  
   <TD>Up Front:<BR>  
       <Input Type="Radio" Name="optFetchOptions"  OnClick="SetFO('adcFetchUpFront')">  
   </TD>  
   <TD>Background w/ Blocking:<BR>  
       <Input Type="Radio" Name="optFetchOptions" Checked OnClick="SetFO('adcFetchBackground')">  
   </TD>  
   <TD>Background w/o Blocking:<BR>  
      <Input Type="Radio" Name="optFetchOptions"  OnClick="SetFO('adcFetchAsync')">  
   </TD>  
</TR>  
</TABLE>  
  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run"><BR>  
  
<Script Language="VBScript">  
<!--  
Dim EO         'ExecuteOptions  
Dim FO         'FetchOptions  
EO = "adcExecSync"   'Default value  
FO = "adcFetchBackground"   'Default value  
  
Sub SetExO(NewEO)  
   EO = NewEO  
End Sub  
  
Sub SetFO(NewFO)  
   FO = NewFO  
End Sub  
  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
   RDC.Server = txtServer.Value  
   RDC.SQL = txtSQL.Value  
   RDC.Connect = txtConnect.Value  
   If EO = "adcExecSync" Then   'Determine which ExecuteOption chosen  
      RDC.ExecuteOptions = adcExecSync  
      MsgBox "Recordset brought in on current calling thread Syncronously"  
   Else  
      RDC.ExecuteOptions = adcExecAsync  
      MsgBox "Recordset brought in on another thread Asyncronously"  
   End If  
  
   If FO = "adcFetchBackground" Then      'Determine                 which FetchOption chosen  
      RDC.FetchOptions = adcFetchBackground  
      MsgBox "Control goes back to user after first batch of records returned"  
   ElseIf FO = " adcFetchUpFront" Then  
      RDC.FetchOptions = adcFetchUpFront  
      MsgBox "All records returned before control goes back to user"  
   Else  
      RDC.FetchOptions = adcFetchAsync  
      MsgBox "Control goes back to user immediately"  
   End If  
  
   RDC.Refresh  
End Sub  
-->  
</Script>  
  
</body>  
</html>  
<!-- EndRefreshVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [ExecuteOptions 屬性 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)   
 [FetchOptions 屬性 (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)


