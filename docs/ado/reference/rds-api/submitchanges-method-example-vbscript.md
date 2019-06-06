---
title: SubmitChanges 方法範例 (VBScript) |Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- SubmitChanges method [ADO], VBScript example
ms.assetid: 619bc7fd-ad0a-44ea-9678-ad40a662c258
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ea04456e4ef3ae0b35ef983df026ca92097af1b5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697504"
---
# <a name="submitchanges-method-example-vbscript"></a>SubmitChanges 方法範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列程式碼片段示範如何使用[SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)物件。  
  
 若要測試此範例中，剪下並貼入正常的 ASP 文件中的這段程式碼並將它命名**SubmitChangesCtrlVBS.asp**。 ASP 指令碼會識別您的伺服器。  
  
```  
<!-- BeginCancelUpdateVBS -->  
<%@Language=VBScript%>  
  
<%'Option Explicit%>  
<% 'use the following META tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE></TITLE>  
</HEAD>  
<BODY>  
<CENTER>  
<H1>Remote Data Service</H1>  
<H2>SubmitChanges and CancelUpdate Methods</H2>  
  
<%  ' to integrate/test this code replace the Server property value and   
    ' the Data Source value in the Connect property with identical values%>  
  
<HR>  
<OBJECT id="RDS" classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" HEIGHT="1" WIDTH="1"></OBJECT>  
<SCRIPT Language="VBScript">  
  
     'set RDS properties for control just created  
    RDS.Server = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    RDS.Connect = "Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';"  
    RDS.SQL = "Select * from Employees"  
    RDS.Refresh  
</SCRIPT>  
  
<TABLE DATASRC="#RDS">  
<THEAD>  
<TR ID="ColHeaders">  
   <TH>ID</TH>  
   <TH>FName</TH>  
   <TH>LName</TH>  
   <TH>Title</TH>  
   <TH>Hire Date</TH>  
   <TH>Birth Date</TH>  
   <TH>Extension</TH>  
   <TH>Home Phone</TH>  
</TR>  
</THEAD>  
<TBODY>  
<TR>  
   <TD> <INPUT DATAFLD="EmployeeID" size=4 id=text1 name=text1> </TD>  
   <TD> <INPUT DATAFLD="FirstName" size=10 id=text2 name=text2> </TD>  
   <TD> <INPUT DATAFLD="LastName" size=10 id=text3 name=text3> </TD>  
   <TD> <INPUT DATAFLD="Title" size=10 id=text4 name=text4> </TD>  
   <TD> <INPUT DATAFLD="HireDate" size=10 id=text5 name=text5> </TD>  
   <TD> <INPUT DATAFLD="BirthDate" size=10 id=text6 name=text6> </TD>  
   <TD> <INPUT DATAFLD="Extension" size=10 id=text7 name=text7> </TD>  
   <TD> <INPUT DATAFLD="HomePhone" size=8 id=text8 name=text8> </TD>  
</TR>  
</TBODY>  
</TABLE>  
<HR>  
<INPUT TYPE=button NAME="SubmitChange" VALUE="Submit Changes">  
<INPUT TYPE=button NAME="CancelChange" VALUE="Cancel Update">  
<BR>  
<H4>Alter a current entry on the grid. Move off that Row. <BR>  
Submit the Changes to your DBMS or cancel the updates. </H4>  
</CENTER>  
<SCRIPT Language="VBScript">  
  
Sub SubmitChange_OnClick  
  
    msgbox "Changes will be made"  
    RDS.SubmitChanges     
    RDS.Refresh  
  
End Sub  
  
Sub CancelChange_OnClick  
  
    msgbox "Changes will be cancelled"  
    RDS.CancelUpdate  
    RDS.Refresh  
  
End Sub  
</SCRIPT>  
  
</BODY>  
</HTML>  
<!-- EndCancelUpdateVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


