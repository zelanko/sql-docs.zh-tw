---
title: sql:可變() 函數 (XQuery) |微軟文件
description: 瞭解如何使用 XQuery 延伸函數 sql:variable() 公開包含 XQuery 運算式中的 SQL 關係值的變數。
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
ms.openlocfilehash: 8241e15643eb4aa25912451ddfed94699954797f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388608"
---
# <a name="xquery-extension-functions---sqlvariable"></a>XQuery 擴充函式 - sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 XQuery 運算式內公開含有 SQL 關聯值的變數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>備註  
 如在主題[綁定關係數據在XML中](../t-sql/xml/binding-relational-data-inside-xml-data.md)所述,當使用[XML數據類型方法](../t-sql/xml/xml-data-type-methods.md)在XQuery中公開關係值時,可以使用此功能。  
  
 例如[,query() 方法](../t-sql/xml/query-method-xml-data-type.md)用於指定針對儲存在**xml**資料類型變數或列中的 XML 實例的查詢。 有時候，您也會想要讓您的查詢作業使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 變數或參數中的值，以合併關聯式資料及 XML 資料。 為此,請使用**sql:變數**函數。  
  
 SQL 值將映射到相應的 XQuery 值,其類型將是等效於相應 SQL 類型的 XQuery 基類型。  
  
 只能在 XML-DML 插入文句的源運算式上下文中引用**xml**實例;否則,您不能引用類型**為 xml**或通用語言運行時 (CLR) 使用者定義的類型的值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. 使用 sql:variable() 函數，將 Transact-SQL 變數值導入 XML  
 此範例會建構一個 XML 執行個體，由下列項目組成：  
  
-   取自非 XML 資料行的值 (`ProductID`)。 [sql:列()函數](../xquery/xquery-extension-functions-sql-column.md)用於在 XML 中綁定此值。  
  
-   取自其他資料表之非 XML 資料行的值 (`ListPrice`)。 同樣地，使用 `sql:column()` 在 XML 中繫結此值。  
  
-   取自 [!INCLUDE[tsql](../includes/tsql-md.md)] 變數的值 (`DiscountPrice`)。 會使用 `sql:variable()` 方法在 XML 中繫結此值。  
  
-   xml`ProductModelName`類型 列**xml**中的值 ( ), 以使查詢更有趣。  
  
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
  
-   該`namespace`關鍵字用於在[XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)中定義命名空間首碼。 因為 `ProductModelName` 類型資料行具有相關聯的結構描述，可從中擷取 `CatalogDescription xml` 屬性值，所以可以完成此設定。  
  
 以下是結果：  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器 XQuery 延伸函式](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [將鍵入的 XML 與未鍵入的 XML 進行比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML 資料&#40;SQL 伺服器&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [建立 XML 資料的實體](../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料型態方法](../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
