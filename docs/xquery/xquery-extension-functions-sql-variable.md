---
title: 'sql：變數 ( # A1 函數 (XQuery) |Microsoft Docs'
description: '瞭解如何使用 XQuery 擴充功能 sql： variable ( # A1 來公開一個變數，該變數包含 XQuery 運算式內的 SQL 關聯式值。'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ed7dd109906b4cace6ed185b1842f9e9e7dedde
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037031"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 擴充函式 - sql:variable()
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  在 XQuery 運算式內公開含有 SQL 關聯值的變數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>備註  
 如在 [XML 內系結關聯式資料](../t-sql/xml/binding-relational-data-inside-xml-data.md)主題中所述，當您使用 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md) 來公開 XQuery 內的關聯式值時，可以使用此函數。  
  
 例如， [查詢 ( # A1 方法](../t-sql/xml/query-method-xml-data-type.md) 是用來針對 **xml 資料類型** 變數或資料行中儲存的 xml 實例指定查詢。 有時候，您也會想要讓您的查詢作業使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 變數或參數中的值，以合併關聯式資料及 XML 資料。 若要這樣做，請使用 **sql： variable** 函數。  
  
 SQL 值會對應到對應的 XQuery 值，且其類型將會是與對應的 SQL 類型相等的 XQuery 基底類型。  
  
 您只能參考 XML-DML insert 語句之來源運算式內容中的 **xml** 實例。否則，您無法參考 **xml** 類型或 common language RUNTIME (CLR) 使用者定義型別的值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. 使用 sql:variable() 函數，將 Transact-SQL 變數值導入 XML  
 此範例會建構一個 XML 執行個體，由下列項目組成：  
  
-   取自非 XML 資料行的值 (`ProductID`)。 [Sql： column ( # A1 函數](../xquery/xquery-extension-functions-sql-column.md)用來在 XML 中系結此值。  
  
-   取自其他資料表之非 XML 資料行的值 (`ListPrice`)。 同樣地，使用 `sql:column()` 在 XML 中繫結此值。  
  
-   取自 [!INCLUDE[tsql](../includes/tsql-md.md)] 變數的值 (`DiscountPrice`)。 會使用 `sql:variable()` 方法在 XML 中繫結此值。  
  
-   `ProductModelName`從**xml**類型資料行)  (值，讓查詢更有趣。  
  
 此查詢如下：  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `query()` 方法中的 XQuery 會建構 XML。  
  
-   `namespace`關鍵字是用來定義[XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中的命名空間前置詞。 因為 `ProductModelName` 類型資料行具有相關聯的結構描述，可從中擷取 `CatalogDescription xml` 屬性值，所以可以完成此設定。  
  
 以下是結果：  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server XQuery 擴充功能函式](./xquery-extension-functions-sql-column.md)   
 [比較具類型的 XML 與不具類型的 XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [建立 XML 資料的執行個體](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
