---
title: exist() 方法 (xml 資料類型) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5f17e8237939d2d2b5a5c7f92d3878b348ed65e1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970828"
---
# <a name="exist-method-xml-data-type"></a>exist() 方法 (xml 資料類型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回代表下列其中一個條件的**位元**：  
  
-   1 代表 True，即查詢中的 XQuery 運算式傳回非空的結果。 也就是，它至少會傳回一個 XML 節點。  
  
-   0 代表 False，即查詢傳回空的結果。  
  
-   如果查詢所執行的 **xml** 資料類型執行個體包含 NULL，則會傳回 NULL。  
  
## <a name="syntax"></a>語法  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>引數  
 XQuery  
 是一個 XQuery 運算式，為字串常值。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]  
>  **exist()** 方法會針對傳回非空白結果的 XQuery 運算式傳回 1。 若您在 **exist()** 方法內指定 **true()** 或 **false()** 函數，則 **exist()** 方法會傳回 1，因為函數 **true()** 及 **false()** 分別會傳回布林值 True 及 False。 也就是說，它們會傳回非空白的結果。 因此，**exist()** 會傳回 1 (True)，如下列範例所示：  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>範例  
 下列範例會示範如何指定 **exist()** 方法。  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>範例：針對 xml 類型變數指定 exist() 方法  
 在下列範例中，@x 是 **xml** 類型變數 (不具類型的 xml)，而 @f 則是整數類型變數，用以儲存 **exist()** 方法所傳回的值。 如果儲存在 XML 執行個體中的日期值是 `2002-01-01`，**exist()** 方法會傳回 True (1)。  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 在比較 **exist()** 方法中的日期時，請注意下列要點：  
  
-   程式碼 `cast as xs:date?` 是用以將值轉換成 **xs:date** 類型以利進行比較。  
  
-   **@Somedate** 屬性的值是不具類型的。 在比較此值時，會隱含地將它轉換成比較右邊的類型，即 **xs:date** 類型。  
  
-   不是使用 **cast as xs:date()**，而是改用 **xs:date()** 建構函式。 如需詳細資訊，請參閱[建構函式 &#40;XQuery&#41;](../../xquery/constructor-functions-xquery.md)。  
  
 下列範例與上例相似，除了它有 <`Somedate`> 元素以外。  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **text()** 方法會傳回一個文字節點，其中包含不具類型的值 `2002-01-01`。 (XQuery 類型是 **xdt:untypedAtomic**。)您必須明確地將此具類型的值從 **x** 轉換成 **xsd:date**，因為在此例中不支援隱含轉換。  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>範例：針對具有類型的 xml 變數指定 exist() 方法  
 下列範例說明針對 **xml** 類型變數使用 **exist()** 方法。 它是 XML 類型變數，因為它指定結構描述命名空間的集合名稱 `ManuInstructionsSchemaCollection`。  
  
 在本範例中，會先指派製造指示文件給此變數，然後使用 **exist()** 方法尋找文件中是否包含 **LocationID** 屬性值為 50 的 <`Location`> 元素。  
  
 如果製造指示文件包含具有 `LocationID=50` 的 <`Location`> 元素，針對 @x 變數所指定的 **exist()** 方法將會傳回 1 (True)。 否則，該方法會傳回 0 (False)。  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>範例：針對 xml 類型資料行指定 exist() 方法  
 下列查詢將擷取目錄描述不包含 <`Specifications`> 元素規格的產品型號識別碼。  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   WHERE 子句只會選取那些符合針對 **CatalogDescription xml** 類型資料行所指定的條件之 **ProductDescription** 資料表的資料列。  
  
-   如果 XML 不包含任何 <`Specifications`> 元素，在 WHERE 子句中的 **exist()** 方法將會傳回 1 (True)。 請注意 [not() function (XQuery)](../../xquery/functions-on-boolean-values-not-function.md) 的用法。  
  
-   [sql:column() function (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) 函數是用來帶入非 XML 資料行中的值。  
  
-   此查詢會傳回空的資料列集。  
  
 查詢會指定 xml 資料類型的 **query()** 與 **exist()** 方法，這兩種方法都會在查詢初構中宣告相同的命名空間。 在此例中，您可能會想要使用 WITH XMLNAMESPACES 來宣告前置詞並在查詢中使用它。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 資料修改語言 &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
