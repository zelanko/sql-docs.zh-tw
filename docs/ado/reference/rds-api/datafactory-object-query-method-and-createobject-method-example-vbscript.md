---
title: 建立 RDSServer.DataFactory 物件使用 CreateObject (VBScript) |Microsoft Docs
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
- DataFactory object [ADO], VBScript example
- CreateObject method [ADO], VBScript example
- Query method [ADO], VBScript example
ms.assetid: b4e2844a-120a-4513-860b-f1b6e4b5dda4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d9a3984e956cd9e742bcc8a29accb7fe012b9e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043383"
---
# <a name="datafactory-object-query-method-and-createobject-method-example-vbscript"></a>DataFactory 物件、Query 方法和 CreateObject 方法範例 (VBScript)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 這個範例會建立[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件使用[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)物件。 若要測試此範例中，剪下並貼上此程式碼之間\<主體 > 並\</b > 標記以正常的 HTML 文件並將它命名**DataFactoryVBS.asp**。 ASP 指令碼會識別您的伺服器。  
  
```  
<!-- BeginDataFactoryVBS -->  
<HTML>  
<HEAD>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<META name="VI60_DefaultClientScript" Content="VBScript">  
  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE>DataFactory Object, Query Method, and   
CreateObject Method Example (VBScript)</TITLE>  
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
</HEAD>  
<BODY>  
<h1>DataFactory Object, Query Method, and   
CreateObject Method Example (VBScript)</h1>  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using Query Method of RDSServer.DataFactory</H3>  
  
<!-- RDS.DataSpace  ID RDS1-->  
<OBJECT ID="RDS1" WIDTH=1 HEIGHT=1  
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters   
set at run time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS WIDTH=1 HEIGHT=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>      
</TABLE>  
  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
<BR>  
<H4>Click Run -    
The <i>CreateObject</i> Method of the RDS.DataSpace Object Creates   
an instance of the RDSServer.DataFactory;   
The <i>Query</i> Method of the RDSServer.DataFactory is used  
to bring back a Recordset. </H4>  
  
<Script Language="VBScript">  
  
    Dim rdsDF  
    Dim strServer  
    Dim strCnxn  
    Dim strSQL  
  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    strCnxn = "Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';"  
    strSQL = "Select FirstName, LastName from Employees"  
  
    Sub Run_OnClick()  
  
        ' Create RDSServer.DataFactory Object  
        Dim rs  
        ' Get Recordset  
        Set DF = RDS1.CreateObject("RDSServer.DataFactory", strServer)  
        Set rs = DF.Query(strCnxn, strSQL)  
        ' Set parameters of RDS.DataControl at Run Time  
        RDS.Server = strServer  
        RDS.SQL = strSQL  
        RDS.Connect = strCnxn  
        RDS.Refresh  
  
    End Sub  
</Script>  
  
</BODY>  
</HTML>  
<!-- EndDataFactoryVBS -->  
```  
  
## <a name="see-also"></a>另請參閱  
 [CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)   
 [DataFactory 物件 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace Object (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Query 方法 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


