---
description: ActiveCommand 屬性範例 (JScript)
title: ActiveCommand 屬性範例 (JScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- ActiveCommand property [ADO], JScript example
ms.assetid: be09e2af-ba31-4168-8ccd-2461bb24e49a
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d39a5cdfdf83f87f92a3b9087eda49a72a52f6b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451730"
---
# <a name="activecommand-property-example-jscript"></a>ActiveCommand 屬性範例 (JScript)
此範例示範 [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md) 屬性。 將下列程式碼剪下並貼到 [記事本] 或其他文字編輯器，然後將它儲存為**ActiveCommandJS。**  
  
```  
<!-- BeginActiveCommandJS -->  
<%@LANGUAGE="JScript" %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<%  
    // user input  
    strName = new String(Request.Form("ContactName"))  
%>  
  
<html>  
  
<head>  
<title>ActiveCommand Property Example (JScript)</title>  
<style>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
-->  
</style>  
</head>  
  
<body bgcolor="White">  
  
<h1>ActiveCommand Property Example (JScript)</h1>  
  
<%  
if (strName.length > 0)  
    {  
        // connection and recordset variables  
        var Cnxn = Server.CreateObject("ADODB.Connection")  
        var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
        var cmdContact = Server.CreateObject("ADODB.Command");  
        var rsContact = Server.CreateObject("ADODB.Recordset");  
        // display variables  
        var strMessage;  
  
        try  
        {  
            // open connection  
            Cnxn.Open(strCnxn);  
  
            // Open a recordset using a command object  
            cmdContact.CommandText = "SELECT ContactName FROM Customers WHERE City = ?";  
            cmdContact.ActiveConnection = Cnxn;  
            // create parameter and insert variable value  
            cmdContact.Parameters.Append(cmdContact.CreateParameter("ContactName", adChar, adParamInput, 30, strName));  
  
            rsContact = cmdContact.Execute();  
  
            while(!rsContact.EOF){  
                // start new line  
                strMessage = "<P>";  
  
                // get data  
                strMessage += rsContact("ContactName")  
  
                // end the line  
                strMessage += "</P>";  
  
                // show data  
                Response.Write(strMessage);  
  
                // get next record  
                rsContact.MoveNext;  
            }  
        }  
        catch (e)  
        {  
            Response.Write(e.message);  
        }  
        finally  
        {  
            // 'clean up  
            if (rsContact.State == adStateOpen)  
                rsContact.Close;  
            if (Cnxn.State == adStateOpen)  
                Cnxn.Close;  
            rsContact = null;  
            Cnxn = null;  
        }  
    }  
%>  
  
<hr>  
  
<form method="POST" action="ActiveCommandJS.asp">  
  <p align="left">Enter city of customer to find (e.g., Paris): <input type="text" name="ContactName" size="40" value=""></p>  
  <p align="left"><input type="submit" value="Submit" name="B1"><input type="reset" value="Reset" name="B2"></p>  
</form>  
</body>  
  
</html>  
<!-- EndActiveCommandJS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 ActiveCommand 屬性 ](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [ (ADO) 的命令物件 ](../../../ado/reference/ado-api/command-object-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
