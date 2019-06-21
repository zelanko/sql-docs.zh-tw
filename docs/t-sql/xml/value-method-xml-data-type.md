---
title: value() 方法 (xml 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a208baaf237987c9f3e544da4d02dca72b191f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62857328"
---
# <a name="value-method-xml-data-type"></a>value() 方法 (xml 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  對 XML 執行 XQuery 並傳回 SQL 類型的值。 此方法會傳回純量值。  
  
 通常您會使用此方法，從儲存在 **xml** 類型資料行、參數或變數中的 XML 執行個體擷取值。 如此一來，您就可以指定 SELECT 查詢來結合或比較 XML 資料與非 XML 資料行的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>引數  
 *XQuery*  
 這是 *XQuery* 運算式，在 XML 執行個體內擷取資料的一個字串常值。 XQuery 最多只能傳回一個值。 否則，就會傳回錯誤。  
  
 *SQLType*  
 是慣用的 SQL 類型，要傳回的字串常值。 此方法的傳回類型符合 *SQLType* 參數。 *SQLType* 不可為 **xml** 資料類型、通用語言執行平台 (CLR) 使用者定義型別、**image**、**text**、**ntext** 或 **sql_variant** 資料類型。 *SQLType* 可以是 SQL、使用者定義資料類型。  
  
 **value()** 方法會隱含使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 運算子，並試著將 XQuery 運算式的結果 (序列化字串表示法)，從 XSD 類型轉換成 [!INCLUDE[tsql](../../includes/tsql-md.md)] 轉換所指定的對應 SQL 類型。 如需 CONVERT 之類型轉換規則的詳細資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)。  
  
> [!NOTE]  
>  基於效能的考量，不要在述詞中使用 **value()** 方法來與關聯式值做比較，而是使用 **exist()** 搭配 **sql:column()** 進行比較。 如下列範例 D 所示。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. 對 xml 類型變數使用 value() 方法  
 在下列範例中，XML 執行個體是儲存在 `xml` 類型的變數中。 `value()` 方法會從 XML 擷取 `ProductID` 屬性值， 然後此值會指派給 `int` 變數。  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 傳回的結果為值 1。  
  
 雖然 XML 執行個體中只有一個 `ProductID` 屬性，靜態類型規則仍要求您明確指定路徑運算式傳回單一值。 因此，會在路徑運算式結尾另外指定 `[1]`。 如需靜態類型的詳細資訊，請參閱 [XQuery 與靜態類型](../../xquery/xquery-and-static-typing.md)。  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. 使用 value() 方法來擷取 xml 類型資料行中的值  
 下列查詢是針對 `AdventureWorks` 資料庫中的 **xml** 類型資料行 (`CatalogDescription`) 所指定。 此查詢會從儲存在資料行中的每一個 XML 執行個體擷取 `ProductModelID` 屬性值。  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `namespace` 關鍵字是用來定義命名空間前置詞。  
  
-   根據靜態類型需求，會在 `[1]` 方法的路徑運算式結尾加入 `value()`，以明確指出路徑運算式會傳回單一值。  
  
 以下是部份結果：  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. 使用 value() 和 exist() 方法來擷取 xml 類型資料行中的值  
 下列範例顯示如何使用 **xml** 資料類型的 `value()` 方法和 [exist()](../../t-sql/xml/exist-method-xml-data-type.md) 方法。 `value()` 方法是用於擷取 XML 中的 `ProductModelID` 屬性值。 `exist()` 子句中的 `WHERE` 方法則是用於篩選資料表中的資料列。  
  
 此查詢會從將保固資訊 (<`Warranty`> 元素) 作為功能之一的 XML 執行個體中，擷取產品型號識別碼。 `WHERE` 子句中的條件會使用 `exist()` 方法，只擷取滿足此條件的資料列。  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   `CatalogDescription` 資料行是具類型的 XML 資料行。 這表示它有相關聯的結構描述集合。 在 [XQuery 初構](../../xquery/modules-and-prologs-xquery-prolog.md)中，命名空間宣告是用來定義稍後要在查詢主體中使用的前置詞。  
  
-   如果 `exist()` 方法傳回 `1` (True)，表示 XML 執行個體包括 <`Warranty`> 子元素作為功能之一。  
  
-   `value()` 子句中的 `SELECT` 方法就會擷取 `ProductModelID` 屬性值做為整數。  
  
 以下是部份結果：  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. 使用 exist() 方法而非 value() 方法  
 基於效能的考量，不要在述詞中使用 `value()` 方法來與關聯式值做比較，而是使用 `exist()` 搭配 `sql:column()` 進行比較。 例如：  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 這可由下列方式來撰寫：  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
