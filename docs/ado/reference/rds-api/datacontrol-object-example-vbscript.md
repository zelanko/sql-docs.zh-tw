---
description: DataControl 物件範例 (VBScript)
title: " (VBScript) 的 DataControl 物件範例 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- DataControl object [ADO], VBScript example
ms.assetid: 4f306a51-d5a4-4785-b426-487639cda164
author: rothja
ms.author: jroth
ms.openlocfilehash: c237a4259838beca54f0016b8a34f191e169d0ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439160"
---
# <a name="datacontrol-object-example-vbscript"></a>DataControl 物件範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列程式碼顯示如何設定 [RDS。](../../../ado/reference/rds-api/datacontrol-object-rds.md) 在設計階段 DataControl 參數，並將其系結至資料感知控制項。 將此程式碼剪下並貼到 \<Body> 一般 HTML 檔案中的和標記之間，然後將 \</Body> 它命名為 **DataControlDesignVBS asp**。 ASP 腳本會識別您的伺服器。  
  
```  
<!-- BeginDataControlDesignVBS -->  
<%@ Language=VBScript %>  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>RDS DataControl</title>  
  
    <%' local style sheet used for display%>  
<STYLE>  
<!--  
BODY {  
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
</STYLE>  
</HEAD>  
  
<BODY>  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Remote Data Service</H3>  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR>  
      <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
      <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
<!-- Remote Data Service with Parameters set at Design Time -->  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS>  
   <PARAM NAME="SQL" VALUE="Select * from Employees for browse">  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
</OBJECT>  
  
</BODY>  
</HTML>  
<!-- EndDataControlDesignVBS -->  
```  
  
 下列範例顯示如何設定 RDS 的必要參數 **。** 在執行時間 DataControl。 若要測試此範例，請將此程式碼剪下並貼到 \<Body> 一般 HTML 檔案中的和標記之間，然後將 \</Body> 它命名為 **DataControlRuntimeVBS .asp**。 ASP 腳本會識別您的伺服器。  
  
```  
<!-- BeginDataControlRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Data Control Object Example (VBScript)</title>  
  
    <%' local style sheet used for display%>  
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
<h1>Data Control Object Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Remote Data Service Run Time</H3>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
    <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
<% ' RDS.DataControl with no parameters set at design time %>  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS HEIGHT=1 WIDTH=1></OBJECT>  
  
<FORM name="frmInput">  
<HR>  
<Input Size="70" Name="txtServer" Value="https://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
<Input Size="100" Name="txtConnect" Value="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Initial Catalog='Pubs';Integrated Security='SSPI';">  
<BR>  
<Input Size="70" Name="txtSQL" Value="Select * from Authors">  
<HR>  
<INPUT TYPE="BUTTON" NAME="Run" VALUE="Run"><BR>  
<H4>Show grid with these values or change them to see data from another ODBC data source on your server</H4>  
</FORM>  
  
<Script Language="VBScript">  
  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
  
   RDS.Server = document.frmInput.txtServer.Value  
   RDS.Connect = document.frmInput.txtConnect.Value  
   RDS.SQL = document.frmInput.txtSQL.Value  
  
   RDS.Refresh  
  
End Sub  
  
</Script>  
  
</body>  
</html>  
<!-- EndDataControlRuntimeVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


