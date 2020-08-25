---
description: " (JScript) 的 Filter 和 RecordCount 屬性範例"
title: 篩選和 RecordCount 屬性範例 (JScript) |Microsoft Docs
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
- RecordCount property [ADO], JScript example
- Filter property [ADO], JScript example
ms.assetid: 677fa67e-9cb9-4d7d-a786-beeb5bee5236
author: rothja
ms.author: jroth
ms.openlocfilehash: e9de9c244d7faa115f03463a74a1dcaedb243b65
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775407"
---
# <a name="filter-and-recordcount-properties-example-jscript"></a> (JScript) 的 Filter 和 RecordCount 屬性範例
這個範例會在 Northwind 資料庫的 [公司] 資料表上開啟**記錄集**，然後使用 [[篩選](./filter-property.md)] 屬性來限制 [公司名稱] 欄位以字母 D 開頭的記錄。將下列程式碼剪下並貼到 [記事本] 或其他文字編輯器，然後將它儲存為**FilterJS。**  
  
```  
<!-- BeginFilterJS -->  
<%@  Language=JavaScript %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
<title>ADO Recordset.Filter Example</title>  
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
  
<body bgcolor="White">  
  
<h1>ADO Recordset.Filter Example</h1>  
<!-- Page text goes here -->  
<%  
    // connection and recordset variables  
    var Cnxn = Server.CreateObject("ADODB.Connection")  
    var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
    var rsCustomers = Server.CreateObject("ADODB.Recordset");  
    var SQLCustomers = "select * from Customers;";  
    // record variables  
    var fld, filter  
    var showBlank = " ";  
    var showNull = "-NULL-";  
  
    try  
    {  
        //open connection   
        Cnxn.Open(strCnxn);  
  
        // create recordset client-side using object refs  
        rsCustomers.ActiveConnection = Cnxn;  
        rsCustomers.CursorLocation = adUseClient;  
        rsCustomers.CursorType = adOpenKeyset;  
        rsCustomers.LockType = adLockOptimistic;  
        rsCustomers.Source = SQLCustomers;  
        rsCustomers.Open();  
  
        rsCustomers.MoveFirst();  
  
        //set filter  
        filter = "CompanyName LIKE 'b*'";  
        rsCustomers.Filter = filter  
  
        if (rsCustomers.RecordCount == 0) {  
            Response.Write("No records matched ");  
            Response.Write (SQLCustomers + "So cannot make table...");  
            Cnxn.Close();  
            Response.End  
        }  
        else {  
        // show the data  
            Response.Write('<table width="100%" border="2">');      
            while(!rsCustomers.EOF) {  
                Response.Write('<tr class="tbody">');  
                for (var thisField = 0; thisField < rsCustomers.Fields.Count; thisField++) {  
                    fld = rsCustomers(thisField);  
                    fldValue = fld.Value;  
                    if (fldValue == null)  
                        fldValue = showNull;  
                    if (fldValue == "")  
                        thisField=showBlank;  
                    Response.Write("<td>" + fldValue + "</td>")  
                }  
                rsCustomers.MoveNext();  
                Response.Write("</tr>");  
            }  
            // close the table  
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
<!-- EndFilterJS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [篩選屬性](./filter-property.md)   
 [ (ADO) 的 RecordCount 屬性 ](./recordcount-property-ado.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)