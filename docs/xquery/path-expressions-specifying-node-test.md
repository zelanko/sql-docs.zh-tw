---
title: "在路徑運算式步驟中指定節點測試 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- axis step [XQuery]
- node test [XQuery]
ms.assetid: ffe27a4c-fdf3-4c66-94f1-7e955a36cadd
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f9fece26e607005cca982be1963a9ca8a53a632
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="path-expressions---specifying-node-test"></a>路徑運算式的指定節點測試
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  路徑運算式中的軸步包含下列部份：  
  
-   [軸](../xquery/path-expressions-specifying-axis.md)  
  
-   節點測試  
  
-   [零或多個步驟限定詞 （選擇性）](../xquery/path-expressions-specifying-predicates.md)  
  
 如需詳細資訊，請參閱[路徑運算式 &#40;XQuery &#41;](../xquery/path-expressions-xquery.md).  
  
 節點測試是一種條件，而且是路徑運算式中軸步的第二個部份。 步驟所選取的所有節點必須符合此條件。 對於路徑運算式 `/child::ProductDescription`，節點測試是 `ProductDescription`。 此步驟只會擷取名稱是 ProductDescription 的元素節點子系。  
  
 節點測試條件可包含下列項目：  
  
-   節點名稱。 只會傳回主體節點種類具有指定名稱的節點。  
  
-   節點類型。 只會傳回指定類型的節點。  
  
> [!NOTE]  
>  在 XQuery 路徑運算式中指定的節點名稱，並不受限於與永遠區分大小寫的 Transact-SQL 查詢相同的區分定序規則。  
  
## <a name="node-name-as-node-test"></a>做為節點測試的節點名稱  
 當在路徑運算式步驟中指定節點名稱做為節點測試時，您必須了解主體節點種類的概念。 每個軸、子系、父系或屬性都有主要節點類型。 例如：  
  
-   屬性軸只能包含屬性。 因此，屬性節點是屬性軸的主要節點種類。  
  
-   對於其他的軸，如果軸所選取的節點可包含元素節點，元素是該軸的主要節點種類。  
  
 當您指定節點名稱做為節點測試時，該步驟會傳回下列類型的節點：  
  
-   軸的主要節點種類的節點。  
  
-   在節點測試中指定相同名稱的節點。  
  
 例如，請考慮下列路徑運算式：  
  
```  
child::ProductDescription   
```  
  
 此一步運算式指定了 `child` 軸以及節點名稱 `ProductDescription` 做為節點測試。 運算式只會傳回那些是子軸、元素節點的主要節點種類而且擁有 ProductDescription 做為其名稱之節點。  
  
 路徑運算式 `/child::PD:ProductDescription/child::PD:Features/descendant::*,` 有三步。 這些步可以指定元素和下階軸。 在每一步中，會將節點名稱指定成節點測試。 在第三步中的萬用字元 (`*`) 代表下階軸主要節點種類的所有節點。 軸的主要節點種類可決定所選取的節點類型，而節點名稱可篩選所選取的節點。  
  
 如此一來，當此運算式會針對執行中的產品目錄 XML 文件**ProductModel**資料表，它會擷取的所有元素節點子系\<功能 > 元素節點子系\<P > 項目。  
  
 路徑運算式`/child::PD:ProductDescription/attribute::ProductModelID`，所組成的兩個步驟。 這兩步均指定節點名稱做為節點測試。 另外，第二步會使用屬性軸。 因此，每一步所選取的軸之主要節點種類的節點，其所指定的名稱均與節點測試相同。 因此，運算式會傳回**ProductModelID**屬性節點\<p > 項目節點。  
  
 當為節點測試指定節點名稱時，您可以使用萬用字元 (*) 指定節點的本機名稱或用於節點的命名空間前置詞，如下列範例所示：  
  
```  
declare @x xml  
set @x = '  
<greeting xmlns="ns1">  
   <salutation>hello</salutation>  
</greeting>  
<greeting xmlns="ns2">  
   <salutation>welcome</salutation>  
</greeting>  
<farewell xmlns="ns1" />'  
select @x.query('//*:greeting')  
select @x.query('declare namespace ns="ns1"; /ns:*')  
```  
  
## <a name="node-type-as-node-test"></a>做為節點測試的節點類型  
 若要查詢非元素節點以外的節點類型，請使用節點類型測試。 如下表所示，有四種節點類型測試可供使用。  
  
|節點類型|傳回值|範例|  
|---------------|-------------|-------------|  
|`comment()`|註解節點會傳回 True。|`following::comment()` 會選取所有出現在內容節點後面的註解節點。|  
|`node()`|任何種類的節點均會傳回 True。|`preceding::node()` 會選取所有出現在內容節點前面的節點。|  
|`processing-instruction()`|處理指示節點會傳回 True。|`self::processing instruction()` 會選取所有在內容節點內的處理指示節點。|  
|`text()`|文字節點會傳回 True。|`child::text()` 會選取內容節點子系的文字節點。|  
  
 如果節點類型 (例如 text() 或 comment()) 是指定為節點測試，該步只會傳回指定種類的節點，不論軸的主要節點種類為何。 例如，下列路徑運算式只會傳回內容節點的註解節點子系：  
  
```  
child::comment()  
```  
  
 同樣地，`/child::ProductDescription/child::Features/child::comment()`擷取其註解節點子系\<功能 > 元素節點子系\<p > 項目節點。  
  
## <a name="examples"></a>範例  
 下列範例會比較節點名稱與節點種類。  
  
### <a name="a-results-of-specifying-the-node-name-and-the-node-type-as-node-tests-in-a-path-expression"></a>A. 將節點名稱與節點類型指定為路徑運算式中的節點測試之結果  
 在下列範例中，簡單的 XML 文件指派給**xml**類型變數。 使用不同的路徑運算式來查詢文件。 接著會比較結果。  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
select @x.query('  
/child::a/child::b/descendant::*  
')  
```  
  
 此運算式會詢問 `<b>` 元素節點的下階元素節點。  
  
 在節點測試中的星號 (`*`) 代表節點名稱的萬用字元。 下階軸具有做為其主要節點種類的元素節點。 因此，運算式會傳回 `<b>` 元素節點的所有下階元素節點。 也就是，將會傳回 `<c>` 與 `<d>` 元素節點，如下列結果所示：  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 如果您指定 descendant-or-self 軸而不是 descendant 軸， 就會傳回內容節點以及其下階：  
  
```  
/child::a/child::b/descendant-or-self::*  
```  
  
 此運算式會傳回 `<b>` 元素節點以及其下階元素節點。 在傳回下階節點時，descendant-or-self 軸的主要節點種類、元素節點類型將決定要傳回哪些節點種類。  
  
 以下是結果：  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 上一個運算式使用萬用字元做為節點名稱。 您可以改用 `node()` 函數，如此運算式所顯示：  
  
```  
/child::a/child::b/descendant::node()  
```  
  
 因為`node()`是節點類型，您會收到下階軸的所有節點。 以下是結果：  
  
```  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
 另外，如果您指定 descendant-or-self 軸與 `node()` 做為節點測試，您將會收到所有的下階、元素與文字節點，以及內容節點，即 `<b>` 元素。  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
text1  
<c>text2  
     <d>text3</d>  
</c>  
text2  
<d>text3</d>  
text3  
```  
  
### <a name="b-specifying-a-node-name-in-the-node-test"></a>B. 指定節點測試中的節點名稱  
 下列範例在所有的路徑運算式中指定節點名稱做為節點測試。 結果，所有的運算式都會傳回在節點測試中有指定節點名稱的軸中主要節點種類的節點。  
  
 下列查詢運算式會從儲存在 `Production.ProductModel` 資料表中的產品目錄 XML 文件，傳回  <`Warranty`> 元素：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:Warranty  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   在 XQuery 初構中的 `namespace` 關鍵字定義了可用於查詢主體中的前置詞。 如需 XQuery 初構的詳細資訊，請參閱[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)。  
  
-   在路徑運算式中的三步全部都可指定子軸和節點名稱做為節點測試。  
  
-   在運算式的任一步中均無法指定軸步的選擇性步驟限定詞部份。  
  
 查詢會傳回 <`ProductDescription`> 元素中 <`Features`> 元素子系的所有 <`Warranty`> 元素子系。  
  
 以下是結果：  
  
```  
<wm:Warranty xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
  <wm:Description>parts and labor</wm:Description>  
</wm:Warranty>     
```  
  
 在下列查詢查詢中，路徑運算式在節點測試中指定了萬用字元 (`*`)。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 萬用字元是針對節點名稱所指定。 因此，查詢會傳回 <`ProductDescription`> 元素節點中 <`Features`> 元素節點子系的所有元素子系。  
  
 除了與萬用字元搭配使用以外，下列查詢與上一個查詢相似，都指定了命名空間。 結果，會傳回在該命名空間的所有元素節點子系。 請注意 <`Features`> 元素可包含不同命名空間的元素。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::wm:*  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 您可以使用萬用字元做為命名空間前置詞，如此查詢所示：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::*:Maintenance  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 此查詢會從產品目錄 XML文件傳回所有命名空間的 <`Maintenance`> 元素節點子系。  
  
### <a name="c-specifying-node-kind-in-the-node-test"></a>C. 指定節點測試中的節點種類  
 下列範例在所有的路徑運算式中指定節點種類做為節點測試。 結果，所有的運算式都會傳回在節點測試中所指定的節點種類。  
  
 在下列查詢中，路徑運算式在第三步中指定節點種類：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::PD:Features/child::text()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 在下一個查詢中，請指定下列項目：  
  
-   路徑運算式包含以斜線分隔的三步 (`/`)。  
  
-   每一步都指定子軸。  
  
-   前兩步指定節點名稱做為節點測試，而第三步指定節點種類做為節點測試。  
  
-   該運算式會傳回 <`ProductDescription`> 元素節點中 <`Features`> 元素子系的文字節點子系。  
  
 只會傳回一個文字節點。 以下是結果：  
  
```  
These are the product highlights.   
```  
  
 下列查詢會傳回 <`ProductDescription`> 元素的註解節點子系。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::PD:ProductDescription/child::comment()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   第二步指定節點種類做為節點測試  
  
-   結果，運算式會傳回 <`ProductDescription`> 元素節點的註解節點子系。  
  
 以下是結果：  
  
```  
<!-- add one or more of these elements... one for each specific product in this product model -->  
<!-- add any tags in <specifications> -->      
```  
  
 下列查詢會擷取最上層的處理指示節點：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction()  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是結果：  
  
```  
<?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>   
```  
  
 您可以將字串常值參數傳遞至 `processing-instruction()` 節點測試。 在此情況下，查詢會傳回處理指示，它的名稱屬性值是在引數中指定的字串常值。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
 /child::processing-instruction("xml-stylesheet")  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
## <a name="implementation-limitations"></a>實作限制  
 下列是特定限制  
  
-   不支援擴充的 SequenceType 節點測試。  
  
-   不支援 processing-instruction(name)。 請改將名稱放置在引號內。  
  
  
