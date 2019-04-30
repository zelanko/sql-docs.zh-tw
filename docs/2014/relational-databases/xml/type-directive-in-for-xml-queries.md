---
title: FOR XML 查詢中的 TYPE 指示詞 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21ff73c95bb85167dfba64d434ed7b6c42051c07
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63193281"
---
# <a name="type-directive-in-for-xml-queries"></a>在 FOR XML 查詢中的 TYPE 指示詞
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援[xml &#40;TRANSACT-SQL&#41; ](/sql/t-sql/xml/xml-transact-sql)可讓您選擇性地要求的 FOR XML 查詢結果傳回為`xml`藉由指定 TYPE 指示詞的資料類型。 這將允許您處理伺服器上 FOR XML 查詢的結果。 例如，您可以針對它指定 XQuery、 將結果指派給`xml`類型變數或撰寫[巢狀 FOR XML 查詢](use-nested-for-xml-queries.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 XML 資料類型的執行個體資料至用戶端，做為不同伺服器建構的結果，例如使用 TYPE 指示詞的 FOR XML 查詢，或使用 `xml` 資料類型從 SQL 資料表資料行和輸出參數傳回 XML 執行個體資料。 在用戶端應用程式中，ADO.NET 提供者要求以二進位編碼從伺服器傳送此 XML 資料類型資訊。 然而，如果您使用沒有 TYPE 指示詞的 FOR XML，XML 資料會以字串類型傳回。 在任一情況下，用戶端提供者將永遠可以處理任一 XML 形式。 請注意，不含 TYPE 指示詞的最上層 FOR XML 無法與資料指標一起使用。  
  
## <a name="examples"></a>範例  
 下列範例說明搭配 FOR XML 查詢使用 TYPE 指示詞。  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>以 xml 類型擷取 FOR XML 查詢結果  
 下列查詢將擷取 `Contacts` 資料表中客戶的連絡資訊。 由於 `TYPE` 指示詞是在 `FOR XML` 中指定，因此結果會以 `xml` 類型傳回。  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 以下是部份結果：  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>將 FOR XML 查詢結果指派給 xml 類型變數  
 在以下範例中，FOR XML 結果會指派給一個 `xml` 類型變數 `@x`。 此查詢會擷取連絡資訊，例如`BusinessEntityID`， `FirstName`， `LastName`，以及其他電話號碼從`AdditionalContactInfo`資料行`xml``TYPE`。 由於 `FOR XML` 子句會指定 `TYPE` 指示詞，因此 XML 將以 `xml` 類型傳回並將其指派給變數。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>查詢 FOR XML 查詢的結果  
 FOR XML 查詢會傳回 XML。 因此，您可以將 `xml` 類型方法 (例如 `query()` 與 `value()`) 套用至 FOR XML 查詢所傳回的 XML 結果。  
  
 在下列查詢中，`xml` 資料類型的 `query()` 方法是用以查詢 `FOR XML` 查詢的結果。 如需詳細資訊，請參閱 [query&#40;&#41; 方法 &#40;xml 資料類型&#41;](/sql/t-sql/xml/query-method-xml-data-type)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 內部 `SELECT ... FOR XML` 查詢會傳回 `xml` 類型結果，以利外部 `SELECT` 將 `query()` 方法套用至 `xml` 類型。 請注意已指定 `TYPE` 指示詞。  
  
 以下是結果：  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="S??nchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 在下列查詢中，`xml` 資料類型的 `value()` 方法是用以擷取 `SELECT...FOR XML` 查詢所傳回的 XML 結果。 如需詳細資訊，請參閱 [value&#40;&#41; 方法 &#40;xml 資料類型&#41;](/sql/t-sql/xml/value-method-xml-data-type)。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 在 `value()` 方法中的 XQuery 路徑運算式會擷取客戶連絡人之 `BusinessEntityID` 為 `1`的第一個客戶電話號碼。  
  
> [!NOTE]  
>  如果未指定 TYPE 指示詞，FOR XML 查詢結果會以 `nvarchar(max)` 類型傳回。  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>使用 INSERT、UPDATE 及 DELETE 中的 FOR XML 查詢結果 (Transact-SQL DML)  
 下列範例示範如何在「資料管理語言」(DML) 陳述式中使用 FOR XML 查詢。 在下列範例中，`FOR XML` 會傳回 `xml` 類型的執行個體。 `INSERT` 陳述式會將此 XML 插入資料表中。  
  
```  
CREATE TABLE T1(intCol int, XmlCol xml);  
GO  
INSERT INTO T1   
VALUES(1, '<Root><ProductDescription ProductModelID="1" /></Root>');  
GO  
  
CREATE TABLE T2(XmlCol xml)  
GO  
INSERT INTO T2(XmlCol)   
SELECT (SELECT XmlCol.query('/Root')   
        FROM T1   
        FOR XML AUTO,TYPE);   
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
