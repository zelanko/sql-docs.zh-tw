---
title: "XML 資料類型的 FOR XML 支援 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined functions [SQL Server], XML
- xml data type [SQL Server], FOR XML clause
ms.assetid: 365de07d-694c-4c8b-b671-8825be27f87c
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9fcd42a40be7da666ed66dc7eb05600b081457ea
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="for-xml-support-for-the-xml-data-type"></a>xml 資料類型的 FOR XML 支援
  如果 FOR XML 查詢在 SELECT 子句中指定 **xml** 類型的資料行，無論您是否指定 ELEMENTS 指示詞，資料行值都會對應為傳回的 XML 中之元素。 **xml** 類型資料行中的任何 XML 宣告都沒有序列化。  
  
 例如，下列查詢會從 `BusinessEntityID`XML `FirstName`類型的 `LastName` 資料行擷取客戶連絡資訊，例如 `AdditionalContactInfo` 、 **和** 資料行，以及電話號碼。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 因為查詢並未指定 ELEMENTS 指示詞，除了從 **xml** 類型資料行擷取的其他連絡資訊值以外，資料行值都是以屬性傳回。 這些是以元素傳回。  
  
 以下是部份結果：  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</PhoneNumber>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<PhoneNumber>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</PhoneNumber>`  
  
```  
</Person.Person>  
...  
```  
  
 如果您為 XQuery 產生的 XML 資料行指定資料行別名，該別名會用來在 XQuery 產生的 XML 周圍加入包裝函數元素。 例如，下列查詢會指定 `MorePhoneNumbers` 做為資料行別名：  
  
```  
SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumber  
FROM Person.Person  
WHERE AdditionalContactInfo.query('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
')IS NOT NULL  
FOR XML AUTO, TYPE;  
```  
  
 XQuery 傳回的 XML 會包裝在 <`MorePhoneNumbers`> 元素內，如以下的部分結果所示：  
  
 `<Person.Person BusinessEntityID="291" FirstName="Gustavo" LastName="Achong">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1112</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">425-555-1111</act:number>`  
  
 `</MorePhoneNumbers>`  
  
 `</Person.Person>`  
  
 `<Person.Person BusinessEntityID="293" FirstName="Catherine" LastName="Abel">`  
  
 `<MorePhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-2222</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">206-555-1234</act:number>`  
  
 `</MorePhoneNumbers>`  
  
```  
</Person.Person>  
...  
```  
  
 如果您在查詢中指定 ELEMENTS 指示詞，則產生的 XML 中會將 BusinessEntityID、LastName 和 FirstName 以元素傳回。  
  
 下列範例說明 FOR XML 處理邏輯並不會從 **xml** 類型資料行，序列化 XML 資料中的任何 XML 宣告：  
  
```  
create table t(i int, x xml)  
go  
insert into t values(1, '<?xml version="1.0" encoding="UTF-8" ?>  
                             <Root SomeID="10" />')  
select i, x  
from   t  
for xml auto;  
```  
  
 以下是結果。 在結果中，XML 宣告 <`?xml version="1.0" encoding="UTF-8" ?`> 沒有序列化。  
  
```  
<root>  
  <t i="1">  
    <x>  
      <Root SomeID="10" />  
    </x>  
  </t>  
</root>  
```  
  
## <a name="returning-xml-from-a-user-defined-function"></a>從使用者自訂函數傳回 XML  
 可利用 FOR XML 查詢，從傳回下列項目之一的使用者自訂函數，傳回 XML：  
  
-   具有單一 **xml** 類型資料行的資料表  
  
-   **xml** 類型的執行個體  
  
 例如，下列使用者定義函數會傳回具有單一 **XML**類型資料行的資料表：  
  
```  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.MyUDF (@ProudctModelID int)  
RETURNS @T TABLE  
  (  
     ProductDescription xml  
  )  
AS  
BEGIN  
  INSERT @T  
     SELECT CatalogDescription.query('  
declare namespace PD="http://www.adventure-works.com/schemas/products/description";  
                    //PD:ProductDescription  ')  
     FROM Production.ProductModel  
     WHERE ProductModelID = @ProudctModelID  
  RETURN  
END;  
```  
  
 您可以執行使用者定義函數，並查詢它所傳回的資料表。 在此範例中，會將透過查詢資料表而傳回的 XML 指派給 **xml** 類型的變數。  
  
```  
declare @x xml;  
set @x = (SELECT * FROM MyUDF(19));  
select @x;  
```  
  
 以下是另一個使用者定義函數範例。 這個使用者定義函數會傳回 **XML** 類型的執行個體。 在此範例中，使用者定義函數會傳回 XML 類型的執行個體，因為有指定結構描述命名空間。  
  
```  
DROP FUNCTION dbo.MyUDF;  
GO  
CREATE FUNCTION MyUDF (@ProductModelID int)   
RETURNS xml ([Production].[ProductDescriptionSchemaCollection])  
AS  
BEGIN  
  declare @x xml  
  set @x =   ( SELECT CatalogDescription  
          FROM Production.ProductModel  
          WHERE ProductModelID = @ProductModelID )  
  return @x  
END;  
```  
  
 使用者定義函數傳回的 XML 可以指派到 **XML** 類型的變數，如下所示：  
  
```  
declare @x xml;  
SELECT @x= dbo.MyUDF4 (19) ;  
select @x;  
```  
  
## <a name="see-also"></a>另請參閱  
 [各個 SQL Server 資料類型的 FOR XML 支援](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  

