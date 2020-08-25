---
description: Refresh 方法範例 (VBScript)
title: " (VBScript) 的 Refresh 方法範例 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9d1a01aa5ef2049012cb296a2dc56684b8577c15
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767607"
---
# <a name="refresh-method-example-vbscript"></a>Refresh 方法範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列範例顯示如何設定 RDS 的必要參數 [。](./datacontrol-object-rds.md) 在執行時間 DataControl。 使用[Refresh](../ado-api/refresh-method-ado.md)方法抓取[記錄集](../ado-api/recordset-object-ado.md)的方式是由[ExecuteOptions](./executeoptions-property-rds.md)和[FetchOptions](./fetchoptions-property-rds.md)屬性的設定所決定。 若要測試此範例，請將下列程式碼剪下並貼入一般 ASP 檔中，並將它命名為**RefreshVBS。** 使用 [ **尋找** ] 找出檔案 Adovbs，並將它放在您打算使用的目錄中。 ASP 腳本會識別您的伺服器。  
  
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
Server: <Input Size=70 Name="txtServer" Value="https://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
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
   <TD> </TD>  
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
 [DataControl 物件 (RDS) ](./datacontrol-object-rds.md)   
 [ExecuteOptions 屬性 (RDS) ](./executeoptions-property-rds.md)   
 [FetchOptions 屬性 (RDS) ](./fetchoptions-property-rds.md)   
 [ (ADO) 的記錄集物件 ](../ado-api/recordset-object-ado.md)   
 [Refresh 方法 (ADO)](../ado-api/refresh-method-ado.md)