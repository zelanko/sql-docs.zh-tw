---
title: 在路徑運算式步驟中指定軸 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
author: rothja
ms.author: jroth
ms.openlocfilehash: 07058816406ef6ac0d5a3356423e231a10ce6165
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946486"
---
# <a name="path-expressions---specifying-axis"></a>路徑運算式 - 指定軸
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  路徑運算式中的軸步包含下列部份：  
  
-   軸  
  
-   [節點測試](../xquery/path-expressions-specifying-node-test.md)  
  
-   [零或多個步驟限定詞 (選擇性)](../xquery/path-expressions-specifying-predicates.md)  
  
 如需詳細資訊，請參閱[&#40;XQuery&#41;的路徑運算式](../xquery/path-expressions-xquery.md)。  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XQuery 實作支援下列軸步。  
  
|軸|描述|  
|----------|-----------------|  
|**child**|傳回內容節點的子系。|  
|**descendant**|傳回內容節點的所有下階。|  
|**父**|傳回內容節點的父系。|  
|**特性**|傳回內容節點的屬性。|  
|**供電**|傳回內容節點本身。|  
|**descendant-or-self**|傳回內容節點及內容節點的所有下階。|  
  
 除了**父**軸以外，所有這些軸都是順向軸。 **父**軸是反向軸，因為它會在檔階層中向後搜尋。 例如，相對路徑運算式 `child::ProductDescription/child::Summary` 有兩個步驟，而且每個步驟都指定 `child` 軸。 第一個步驟會抓取\<內容節點的 ProductDescription> 元素子系。 針對每\<個 ProductDescription> 元素節點，第二個步驟\<會抓取摘要> 元素節點子系。  
  
 相對路徑運算式 `child::root/child::Location/attribute::LocationID` 有三步。 前兩步每個都會指定 `child` 軸，第三步會指定 `attribute` 軸。 針對**ProductModel**資料表中的製造指示 XML 檔執行時，運算式會傳回`LocationID` \< \<根> 元素> 專案節點子系的位置屬性。  
  
## <a name="examples"></a>範例  
 本主題中的查詢範例是針對**AdventureWorks**資料庫中的**xml**類型資料行所指定。  
  
### <a name="a-specifying-a-child-axis"></a>A. 指定子軸  
 針對特定的產品型號，下列查詢會從儲存\<在`Production.ProductModel`資料表中的產品目錄描述\<，抓取 ProductDescription> 元素節點的功能> 元素節點子系。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   Xml `query()`資料類型的**xml**方法會指定路徑運算式。  
  
-   在路徑運算式中的步驟可指定 `child` 軸和節點名稱、`ProductDescription` 與 `Features` 做為節點測試。 如需節點測試的詳細資訊，請參閱[在路徑運算式步驟中指定節點測試](../xquery/path-expressions-specifying-node-test.md)。  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. 指定 descendant 與 descendant-or-self 軸  
 下列使用 descendant 與 descendant-or-self 軸 這個範例中的查詢是針對**xml**類型變數所指定。 XML 執行個體已加以簡化，以便於能輕易地說明產生結果中的差異。  
  
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
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 在下列結果中，運算式會傳回 `<b>` 元素節點的 `<a>` 元素節點子系：  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 在此運算式中，如果您為下列路徑運算式指定 descendant 軸：  
  
 `/child::a/child::b/descendant::*`，您會要求 <`b`> 元素節點的所有下階。  
  
 在節點測試中的星號 (*) 代表做為節點測試的節點名稱。 因此，descendant 軸、元素節點的主要節點類型將決定要傳回的節點類型。 也就是，運算式會傳回所有的元素節點。 但不會傳回文字節點。 如需主要節點類型及其與節點測試之關聯性的詳細資訊，請參閱[在路徑運算式步驟主題中指定節點測試](../xquery/path-expressions-specifying-node-test.md)。  
  
 會傳回 <`c`> 和 <`d`> 的元素節點，如下列結果所示：  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 如果您指定子系或本身軸，而不是下階軸， `/child::a/child::b/descendant-or-self::*`則會傳回內容節點、元素`b` <> 和其子系。  
  
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
  
 下列針對**AdventureWorks**資料庫的範例查詢會抓取 <`Features` `ProductDescription`> 專案之 <> 專案子系的所有子代元素節點：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. 指定父軸  
 下列查詢會傳回`Summary` `ProductDescription` `Production.ProductModel`資料表中儲存的產品目錄 XML 檔中，<> 專案的 <> 元素子系。  
  
 這個範例會使用父軸傳回 <`Feature`> 專案的父系，並抓取 <`Summary` `ProductDescription`> 元素的 <> 專案子系。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 在此查詢範例中，路徑運算式使用 `parent` 軸。 您可以重寫沒有父軸的運算式，如下列所示：  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 在下列範例中提供了更有用的父軸範例。  
  
 儲存在**ProductModel**資料表之**CatalogDescription**資料行中的每個產品型號目錄描述`<ProductDescription>`都具有具有`ProductModelID`屬性和`<Features>`子項目的元素，如下列片段所示：  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 此查詢在 FLWOR 陳述式中設定了 iterator 變數、`$f`，以傳回 `<Features>` 元素的元素子系。 如需詳細資訊，請參閱[FLWOR 語句和反復專案 &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)。 對於每個功能，`return` 子句會以下列形式建構 XML：  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 若要為`ProductModelID`每個`<Feature`> 專案加入， `parent`請指定軸：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部份結果：  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 請注意在路徑運算式中加入了述詞 `[1]`，以確保會傳回單一值。  
  
  
