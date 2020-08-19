---
description: Find 方法範例 (JScript)
title: " (JScript 的 Find 方法範例) |Microsoft Docs"
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
- Find method [ADO], JScript example
ms.assetid: adb5c37e-7874-41db-b4ee-572c1323deff
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c328a3efe858c7abd9872eef0fcd28dfa1ccb36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443630"
---
# <a name="find-method-example-jscript"></a>Find 方法範例 (JScript)
此範例會使用[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[Find](../../../ado/reference/ado-api/find-method-ado.md)方法，找出並顯示***Northwind***資料庫中名稱以字母 G 開頭的公司。剪下並貼上下列程式碼至記事本或其他文字編輯器，然後將它儲存為**FindJS。**  
  
```  
<!-- BeginFindJS -->  
<%@  Language=JavaScript %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
<title>ADO Recordset.Find Example</title>  
<style>  
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
</style>  
</head>  
  
<body bgcolor="white">  
  
<h1>ADO Recordset.Find Example</h1>  
<%  
    // connection and recordset variables  
    var Cnxn = Server.CreateObject("ADODB.Connection");  
    var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
    var rsCustomers = Server.CreateObject("ADODB.Recordset");  
        // display string  
    var strMessage;      
    var strFind;  
  
    try  
    {  
            // open connection  
        Cnxn.Open(strCnxn);  
  
            //create recordset using object refs  
        SQLCustomers = "select * from Customers;";  
  
        rsCustomers.ActiveConnection = Cnxn;  
        rsCustomers.CursorLocation = adUseClient;  
        rsCustomers.CursorType = adOpenKeyset;  
        rsCustomers.LockType = adLockOptimistic;  
        rsCustomers.Source = SQLCustomers;  
  
        rsCustomers.Open();  
        rsCustomers.MoveFirst();  
  
            //find criteria  
        strFind = "CompanyName like 'g%'"  
        rsCustomers.Find(strFind);  
  
        if (rsCustomers.EOF) {  
            Response.Write("No records matched ");  
            Response.Write(SQLCustomers & "So cannot make table...");  
            Cnxn.Close();  
            Response.End();  
        }   
        else {  
            Response.Write('<table width="100%" border="2">');  
            Response.Write('<tr class="thead2">');  
            // Put Headings On The Table for each Field Name  
            for (thisField = 0; thisField < rsCustomers.Fields.Count; thisField++) {  
                fieldObject = rsCustomers.Fields(thisField);  
                Response.Write('<th width="' + Math.floor(100 / rsCustomers.Fields.Count) + '%">' + fieldObject.Name + "</th>");  
            }  
            Response.Write("</tr>");  
  
            while (!rsCustomers.EOF) {  
                Response.Write('<tr class="tbody">');  
                for(thisField=0; thisField<rsCustomers.Fields.Count; thisField++) {  
                    fieldObject = rsCustomers.Fields(thisField);  
                    strField = fieldObject.Value;  
                    if (strField == null)  
                        strField = "-Null-";  
                    if (strField == "")  
                        strField = "";  
                    Response.Write("<td>" + strField + "</td>");  
                }  
                rsCustomers.Find(strFind, 1, adSearchForward)  
                Response.Write("</tr>");  
            }  
            Response.Write("</table>");  
        }  
    }  
    catch (e)  
    {  
        Response.Write(e.message);  
    }  
    finally  
    {  
        // clean up  
        if (rsCustomers.State == adStateOpen)  
            rsCustomers.Close;  
        if (Cnxn.State == adStateOpen)  
            Cnxn.Close;  
        rsCustomers = null;  
        Cnxn = null;  
    }  
%>  
  
</body>  
  
</html>  
<!-- EndFindJS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Find 方法 ](../../../ado/reference/ado-api/find-method-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
