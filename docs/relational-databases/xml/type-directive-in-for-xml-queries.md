---
title: FOR XML 查詢中的 TYPE 指示詞 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, TYPE directive
- TYPE directive
ms.assetid: a3df6c30-1f25-45dc-b5a9-bd0e41921293
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2ec549950b912f4a2bd877163b60042c9820ae3c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="type-directive-in-for-xml-queries"></a>在 FOR XML 查詢中的 TYPE 指示詞
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對於 [xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md) 的支援，可讓您藉由指定 TYPE 指示詞，選擇性地要求以 **xml** 資料類型傳回 FOR XML 查詢的結果。 這將允許您處理伺服器上 FOR XML 查詢的結果。 例如，您可以針對它指定 XQuery、將結果指派至 **xml** 類型變數或撰寫 [巢狀 FOR XML 查詢](../../relational-databases/xml/use-nested-for-xml-queries.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 XML 資料類型的執行個體資料至用戶端，作為不同伺服器建構的結果，例如使用 TYPE 指示詞的 FOR XML 查詢，或使用 **xml** 資料類型從 SQL 資料表資料行和輸出參數傳回 XML 執行個體資料值。 在用戶端應用程式中，ADO.NET 提供者要求以二進位編碼從伺服器傳送此 XML 資料類型資訊。 然而，如果您使用沒有 TYPE 指示詞的 FOR XML，XML 資料會以字串類型傳回。 在任一情況下，用戶端提供者將永遠可以處理任一 XML 形式。 請注意，不含 TYPE 指示詞的最上層 FOR XML 無法與資料指標一起使用。  
  
## <a name="examples"></a>範例  
 下列範例說明搭配 FOR XML 查詢使用 TYPE 指示詞。  
  
### <a name="retrieving-for-xml-query-results-as-xml-type"></a>以 xml 類型擷取 FOR XML 查詢結果  
 下列查詢將擷取 `Contacts` 資料表中客戶的連絡資訊。 由於 `TYPE` 指示詞是在 `FOR XML`中指定，因此結果會以 **xml** 類型傳回。  
  
```  
USE AdventureWorks2012;  
Go  
SELECT BusinessEntityID, FirstName, LastName  
FROM Person.Person  
ORDER BY BusinessEntityID  
FOR XML AUTO, TYPE;  
```  
  
 以下是部份結果：  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez"/>`  
  
 `<Person.Person BusinessEntityID="2" FirstName="Terri" LastName="Duffy"/>`  
  
 `...`  
  
### <a name="assigning-for-xml-query-results-to-an-xml-type-variable"></a>將 FOR XML 查詢結果指派給 xml 類型變數  
 在以下範例中，FOR XML 結果會指派給一個 **xml** 類型變數 `@x`。 此查詢會從 `BusinessEntityID`xml `FirstName`的 `LastName`資料行擷取連絡資訊，例如 `AdditionalContactInfo` 、 **、**`TYPE`，以及其他電話號碼。 由於 `FOR XML` 子句會指定 `TYPE` 指示詞，因此 XML 將以 **xml** 類型傳回並將其指派給變數。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @x xml;  
SET @x = (  
   SELECT BusinessEntityID,   
          FirstName,   
          LastName,   
          AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
              //act:telephoneNumber/act:number') as MorePhoneNumbers  
   FROM Person.Person  
   FOR XML AUTO, TYPE);  
SELECT @x;  
GO  
```  
  
### <a name="querying-results-of-a-for-xml-query"></a>查詢 FOR XML 查詢的結果  
 FOR XML 查詢會傳回 XML。 因此您可以將 **xml** 類型方法 (例如 **query()** 與 **value()**) 套用至 FOR XML 查詢所傳回的 XML 結果。  
  
 在下列查詢中，**xml** 資料類型的 `query()` 方法是用以查詢 `FOR XML` 查詢的結果。 如需詳細資訊，請參閱 [query&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/query-method-xml-data-type.md)。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT (SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
DECLARE namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
DECLARE namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
 //act:telephoneNumber/act:number  
') AS PhoneNumbers  
FROM Person.Person  
FOR XML AUTO, TYPE).query('/Person.Person[1]');  
```  
  
 內部 `SELECT … FOR XML` 查詢會傳回 **xml** 類型結果，以利外部 `SELECT` 將 `query()` 方法套用至 **xml** 類型。 請注意已指定 `TYPE` 指示詞。  
  
 以下是結果：  
  
 `<Person.Person BusinessEntityID="1" FirstName="Ken" LastName="Sánchez">`  
  
 `<PhoneNumbers>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">111-111-1111</act:number>`  
  
 `<act:number xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">112-111-1111</act:number>`  
  
 `</PhoneNumbers>`  
  
 `</Person.Person>`  
  
 在下列查詢中，**xml** 資料類型的 `value()` 方法是用以擷取 `SELECT…FOR XML` 查詢所傳回的 XML 結果。 如需詳細資訊，請參閱 [value&#40;&#41; 方法 &#40;xml 資料類型&#41;](../../t-sql/xml/value-method-xml-data-type.md)。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @FirstPhoneFromAdditionalContactInfo varchar(40);  
SELECT @FirstPhoneFromAdditionalContactInfo =   
 ( SELECT BusinessEntityID, FirstName, LastName, AdditionalContactInfo.query('  
declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   //act:telephoneNumber/act:number  
   ') AS PhoneNumbers  
   FROM Person.Person Contact  
   FOR XML AUTO, TYPE).value('  
declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
  /Contact[@BusinessEntityID="1"][1]/PhoneNumbers[1]/act:number[1]', 'varchar(40)'  
 )  
SELECT @FirstPhoneFromAdditionalContactInfo;  
```  
  
 在 `value()` 方法中的 XQuery 路徑運算式會擷取客戶連絡人之 `BusinessEntityID` 為 `1` 的第一個客戶電話號碼。  
  
> [!NOTE]  
>  由於未指定 TYPE 指示詞，因此 FOR XML 查詢結果會以 **nvarchar(max)** 類型傳回。  
  
### <a name="using-for-xml-query-results-in-insert-update-and-delete-transact-sql-dml"></a>使用 INSERT、UPDATE 及 DELETE 中的 FOR XML 查詢結果 (Transact-SQL DML)  
 下列範例示範如何在「資料管理語言」(DML) 陳述式中使用 FOR XML 查詢。 在下列範例中， `FOR XML` 會傳回 **xml** 類型的執行個體。 `INSERT` 陳述式會將此 XML 插入資料表中。  
  
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
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
