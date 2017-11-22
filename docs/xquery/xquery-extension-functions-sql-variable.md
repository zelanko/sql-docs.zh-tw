---
title: ": variable （) 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: cb9b3234241f534cf5d91d7f06b40dde6912ebcc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 擴充函數-: variable （）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 XQuery 運算式內公開含有 SQL 關聯值的變數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>備註  
 本主題中所述[繫結關聯式資料在 XML](../t-sql/xml/binding-relational-data-inside-xml-data.md)，您可以使用此函式，當您使用[XML 資料類型方法](../t-sql/xml/xml-data-type-methods.md)來公開 XQuery 內的關聯式值。  
  
 例如， [query （） 方法](../t-sql/xml/query-method-xml-data-type.md)用來指定針對 XML 執行個體中所儲存的查詢**xml**資料類型變數或資料行。 有時候，您也會想要讓您的查詢作業使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 變數或參數中的值，以合併關聯式資料及 XML 資料。 若要這樣做，您使用**sql: variable**函式。  
  
 SQL 值將會對應至相對應的 XQuery 值，而其類型為相當於對應的 SQL 類型的 XQuery 基底類型。  
  
 您只能參考**xml**內容中執行個體的來源運算式的 XML DML 插入陳述式，否則您不能參考類型的值**xml**或 common language runtime (CLR)使用者定義型別。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. 使用 sql:variable() 函數，將 Transact-SQL 變數值導入 XML  
 此範例會建構一個 XML 執行個體，由下列項目組成：  
  
-   取自非 XML 資料行的值 (`ProductID`)。 [: Column （） 函式](../xquery/xquery-extension-functions-sql-column.md)用來在 XML 中繫結此值。  
  
-   取自其他資料表之非 XML 資料行的值 (`ListPrice`)。 同樣地，使用 `sql:column()` 在 XML 中繫結此值。  
  
-   取自 [!INCLUDE[tsql](../includes/tsql-md.md)] 變數的值 (`DiscountPrice`)。 會使用 `sql:variable()` 方法在 XML 中繫結此值。  
  
-   值 (`ProductModelName`) 從**xml**類型資料行，使查詢更有趣。  
  
 此查詢如下：  
  
```  
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
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
  
-   `namespace`關鍵字用來定義中的命名空間前置詞[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)。 因為 `ProductModelName` 類型資料行具有相關聯的結構描述，可從中擷取 `CatalogDescription xml` 屬性值，所以可以完成此設定。  
  
 以下是結果：  
  
```  
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>請參閱＜  
 [SQL Server XQuery 擴充函數](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [比較具類型的 XML 與不具類型的 XML](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 資料 &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [建立 XML 資料的執行個體](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
