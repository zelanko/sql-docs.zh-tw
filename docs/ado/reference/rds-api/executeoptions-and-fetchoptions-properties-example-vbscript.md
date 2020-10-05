---
description: ExecuteOptions 和 FetchOptions 屬性範例 (VBScript)
title: ExecuteOptions 和 FetchOptions 屬性範例 (VBScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- FetchOptions property [ADO], VBScript example
- ExecuteOptions property [ADO]
ms.assetid: 753a4a3d-0fba-40b8-86e7-50b34182ca69
author: rothja
ms.author: jroth
ms.openlocfilehash: 0bb4b99b268397ff34d6e4c1a022407379dc1409
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722343"
---
# <a name="executeoptions-and-fetchoptions-properties-example-vbscript"></a>ExecuteOptions 和 FetchOptions 屬性範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
 下列程式碼顯示如何在設計階段設定 [ExecuteOptions](./executeoptions-property-rds.md) 和 [FetchOptions](./fetchoptions-property-rds.md) 屬性。 如果保留未設定， **ExecuteOptions** 會預設為 **adcExecSync**。 此設定指出當 **RDS。** 會呼叫 Refresh 方法，它會在目前的呼叫執行緒上執行，也就是同步。 將下列程式碼剪下並貼到 [記事本] 或其他文字編輯器，然後將它儲存為**ExecuteOptionsDesignVBS。**  
  
```  
<!-- BeginExecuteOptionsDesignVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Design-time ExecuteOptions and FetchOptions Properties Example</title>  
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
<h2>Design-time <br> ExecuteOptions and FetchOptions Properties Example</h2>  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS height=1 width=1>  
<PARAM NAME="SQL" VALUE="SELECT FirstName, LastName FROM Employees ORDER BY LastName">  
<PARAM NAME="Connect" VALUE="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Integrated Security='SSPI';Initial Catalog='Northwind'">  
<PARAM NAME="Server" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
<PARAM NAME="ExecuteOptions" VALUE="1">  
<PARAM NAME="FetchOptions" VALUE="3">  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR class="thead2">  
      <TH>First Name</TH>  
      <TH>Last Name</TH>  
   </TR>  
   <TR class="tbody">  
     <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
     <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
  
</body>  
</html>  
<!-- EndExecuteOptionsDesignVBS -->  
```  
  
 下列範例示範如何在執行時間于 VBScript 程式碼中設定 **ExecuteOptions** 和 **FetchOptions** 屬性。 如需這些屬性的實用範例，請參閱重新[整理方法。](./refresh-method-rds.md) 將下列程式碼剪下並貼到 [記事本] 或其他文字編輯器，然後將它儲存為**ExecuteOptionsRuntimeVBS。**  
  
```  
<!-- BeginExecuteOptionsRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Run-time ExecuteOptions and FetchOptions Properties Example</title>  
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
<h2>Run-time <br> ExecuteOptions and FetchOptions Properties Example</h2>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS height=1 width=1>  
<PARAM NAME="SQL" VALUE="SELECT FirstName, LastName FROM Employees ORDER BY LastName">  
<PARAM NAME="Connect" VALUE="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Integrated Security='SSPI';Initial Catalog='Northwind'">  
<PARAM NAME="Server" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR class="thead2">  
      <TH>First Name</TH>  
      <TH>Last Name</TH>  
   </TR>  
   <TR class="tbody">  
     <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
     <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
<Script Language="VBScript">  
Const adcExecSync = 1  
Const adcFetchAsynch = 3  
  
Sub ExecuteHow  
  ' set RDS properties at run-time  
  RDS1.ExecuteOptions = adcExecSync  
  RDS1.FetchOptions = adcFetchAsynch  
  RDS.Refresh  
End Sub  
</Script>  
</body>  
</html>  
<!-- EndExecuteOptionsRuntimeVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteOptions 屬性 (RDS) ](./executeoptions-property-rds.md)   
 [FetchOptions 屬性 (RDS)](./fetchoptions-property-rds.md)