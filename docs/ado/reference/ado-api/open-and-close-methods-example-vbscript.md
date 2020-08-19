---
description: Open 和 Close 方法範例 (VBScript)
title: " (VBScript) 的開啟和關閉方法範例 |Microsoft Docs"
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
- Close method [ADO], VBScript example
- Open method [ADO], VBScript example
ms.assetid: 66eca011-e258-4d8f-bd67-e017bcf0871b
author: rothja
ms.author: jroth
ms.openlocfilehash: bb26a778e3d484ba024a5a38564d9e3abc0a3ef0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443000"
---
# <a name="open-and-close-methods-example-vbscript"></a>Open 和 Close 方法範例 (VBScript)
此範例會在已開啟的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)和[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件上使用[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Close](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
 使用 Active Server Page (ASP) 中的下列範例。 使用 [ **尋找** ] 找出檔案 Adovbs，並將它放在您打算使用的目錄中。 將下列程式碼剪下並貼到 [記事本] 或其他文字編輯器中，然後將它儲存為**OpenVBS。** 您可以在任何瀏覽器中查看結果。  
  
```  
<!-- BeginOpenVBS -->  
<%@ Language=VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>ADO Open Method</title>  
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
<H3>ADO Open Method</H3>  
  
<TABLE WIDTH=600 BORDER=0>  
<TR>  
<TD VALIGN=TOP COLSPAN=3>  
<FONT SIZE=2>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim rsProducts, strSQLProducts  
  
    ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
  
    Cnxn.Open strCnxn  
  
    ' create and open first Recordset using Connection - execute  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "SELECT CompanyName, ContactName, City FROM Customers"  
    Set rsCustomers = Cnxn.Execute(strSQLCustomers)   
  
    ' create and open second Recordset using recordset - open  
    Set rsProducts = Server.CreateObject("ADODB.Recordset")  
    strSQLProducts = "SELECT ProductName, UnitPrice FROM Products"  
    rsProducts.Open strSQLProducts, Cnxn, adOpenDynamic, adLockPessimistic, adCmdText  
    %>  
  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
    <!-- BEGIN column header row for Customer Table-->  
    <TR CLASS=thead>  
       <TD>Company Name</TD>  
       <TD>Contact Name</TD>  
       <TD>City</TD>  
    </TR>  
  
    <!--Display ADO Data from Customer Table-->  
    <% Do Until rsCustomers.EOF %>  
    <TR CLASS=tbody>  
      <TD> <%=rsCustomers("CompanyName")%> </TD>  
      <TD> <%=rsCustomers("ContactName")%></TD>  
      <TD> <%=rsCustomers("City")%> </TD>  
    </TR>   
    <%rsCustomers.MoveNext   
    Loop   
    %>  
    </TABLE>  
  
    <HR>  
  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
    <!-- BEGIN column header row for Product List Table-->  
  
    <TR CLASS=thead2>  
       <TD>Product Name</TD>  
       <TD>Unit Price</TD>  
    </TR>  
    <!-- Display ADO Data Product List-->  
    <% Do Until rsProducts.EOF %>  
      <TR CLASS=tbody>    
      <TD> <%=rsProducts("ProductName")%> </TD>  
      <TD> <%=rsProducts("UnitPrice")%> </TD>  
      </TR>  
      <!--  Next Row = Record -->  
    <%rsProducts.MoveNext   
    Loop   
  
    ' clean up  
    If rsProducts.State = adStateOpen then  
        rsProducts.Close  
    End If  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
    Set rsProducts = Nothing  
    Set rsCustomers = Nothing  
    Set Cnxn = Nothing  
  
    %>  
    </TABLE>  
  
</BODY>  
</HTML>  
<!-- EndOpenVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 Close 方法 ](../../../ado/reference/ado-api/close-method-ado.md)   
 [ (ADO) 的 Connection 物件 ](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ (ADO Connection) 的 Open 方法 ](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [ (ADO 記錄集的 Open 方法) ](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
