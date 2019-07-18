---
title: 在範例 ASP 應用程式 (SQLXML 4.0) 中使用 Updategram |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- ASP applications [SQLXML]
- Active Server Pages
- updategrams [SQLXML], ASP applications
ms.assetid: 10eff799-4c39-4b52-8b38-7ea6f68454a8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e209a4f6118ae9581889299c09653ebaf1cfe2cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014625"
---
# <a name="using-an-updategram-in-a-sample-asp-application-sqlxml-40"></a>在範例 ASP 應用程式中使用 Updategram (SQLXML 4.0)
  這個 Active Server Pages (ASP) 應用程式可讓您在 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之 AdventureWorks 範例資料庫的 Person.Contact 資料表中更新客戶資訊。 此應用程式會進行下列作業：  
  
-   要求使用者輸入連絡識別碼。  
  
-   使用這個客戶識別碼值來執行範本，以便從 Person.Contact 資料表中擷取連絡資訊。  
  
-   使用 HTML 表單來顯示這項資訊。  
  
 然後，使用者就可以更新連絡資訊，但無法更新連絡識別碼 (因為 ContactID 是主索引鍵)。 在使用者提交資訊之後，系統就會執行 Updategram 並且將所有表單參數傳遞給 Updategram。  
  
 下列範本是第一個範本 (GetContact.xml)。 請將這個範本儲存在與 `template` 類型之虛擬名稱相關聯的目錄中。  
  
```  
<root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <sql:header>  
      <sql:param name="cid"></sql:param>  
   </sql:header>  
   <sql:query>  
      SELECT  *   
      FROM    Person.Contact  
      WHERE   ContactID=@cid   
      FOR XML AUTO  
   </sql:query>  
</root>  
```  
  
 下列範本是第二個範本 (UpdateContact.xml)。 請將這個範本儲存在與 `template` 類型之虛擬名稱相關聯的目錄中。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
   <updg:param name="cid"/>  
   <updg:param name="title" />  
   <updg:param name="firstname" />  
   <updg:param name="lastname" />  
   <updg:param name="emailaddress" />  
   <updg:param name="phone" />  
</updg:header>  
<updg:sync >  
   <updg:before>  
      <Person.Contact ContactID="$cid" />   
   </updg:before>  
   <updg:after>  
      <Person.Contact ContactID="$cid"   
       Title="$title"  
       FirstName="$firstname"  
       LastName="$lastname"  
       EmailAddress="$emailaddress"  
       Phone="$phone"/>  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 下列程式碼是 ASP 應用程式 (SampleASP.asp)。 請將它儲存在與您使用網際網路服務管理員公用程式所建立之虛擬根目錄相關聯的目錄中 (這個虛擬根目錄並非使用 IIS Virtual Directory Management for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 公用程式所建立，因為 IIS Virtual Directory Management for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 無法存取或識別 ASP 應用程式)。  
  
> [!NOTE]  
>  在此程式碼中，您必須將 "ServerName" 取代成執行 Microsoft Internet Information Services (IIS) 之伺服器的名稱。  
  
```  
<% LANGUAGE=VBSCRIPT %>  
<%  
  Dim ContactID  
  ContactID=Request.Form("cid")  
%>  
<html>  
<body>  
<%  
  'If a ContactID value is not yet provided, display this form.  
  if ContactID="" then  
%>  
<!-- If the ContactID has not been specified, display the form that allows users to enter an ID. -->  
<form action="AdventureWorksContacts.asp" method="POST">  
<br>  
Enter ContactID: <input type=text name="cid"><br>  
<input type=submit value="Submit this ID" ><br><br>  
<-- Otherwise, if a ContactID is entered, display the second part of the form where the user can change customer information. -->  
<%  
  else  
%>  
<form name="Contacts" action="http://localhost/AdventureWorks/Template/UpdateContact.xml" method="POST">  
You may update customer information below.<br><br>  
<!-- A comment goes here to separate the parts of the application or page. -->  
<br>  
<%  
  ' Load the document in the parser and extract the values to populate the form.  
    Set objXML=Server.CreateObject("MSXML2.DomDocument")  
    ObjXML.setProperty "ServerHTTPRequest", TRUE  
  
    objXML.async=False  
    objXML.Load("http://localhost/AdventureWorks/Template/GetContact.xml?cid=" & ContactID)  
    set objCustomer=objXML.documentElement.childNodes.Item(0)  
  
  ' In retrieving data from the database, if a value in the column is NULL there  
  '  is no attribute for the corresponding element. In this case,  
  ' skip the error generation and go to the next attribute.  
  
  On Error Resume Next  
  
  Response.Write "Contact ID: <input type=text readonly=true style='background-color:silver' name=cid value="""  
  Response.Write objCustomer.attributes(0).value  
  Response.Write """><br><br>"  
  
  Response.Write "Title: <input type=text name=title value="""  
  Response.Write objCustomer.attributes(1).value  
  Response.Write """><br><br>"  
  
  Response.Write "First Name: <input type=text name=firstname value="""  
  Response.Write objCustomer.attributes(2).value  
  Response.Write """><br>"  
  
  Response.Write "Last Name: <input type=text name=lastname value="""  
  Response.Write objCustomer.attributes(3).value  
  Response.Write """><br><br>"  
  
  Response.Write "Email Address: <input type=text name=emailaddress value="""  
  Response.Write objCustomer.attributes(4).value  
  Response.Write """><br><br>"  
  
  Response.Write "Phone: <input type=text name=phone value="""  
  Response.Write objCustomer.attributes(9).value  
  Response.Write """><br><br>"  
  
  set objCustomer=Nothing  
  Set objXML=Nothing  
%>  
<input type="submit" value="Submit this change" ><br><br>  
<input type=hidden name="contenttype" value="text/xml">  
<input type=hidden name="eeid" value="<%=ContactID%>"><br><br>  
<% end if %>  
  
</form>  
</body>  
</html>  
```  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
