---
title: "position 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 287e178fb6b8c0a30ee8af9c014a46a7fa46883f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="context-functions---position-xquery"></a>內容函數的位置 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回整數值，以指出目前所處理的項目序列中內容項目的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>備註  
 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]， **fn:position()**只能用於內容相依述詞的內容。 具體而言，它只能用於括號 ([ ]) 內。針對此函數所做的比較不會在靜態類型推斷期間減少基數。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫。  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. 使用 position() XQuery 函數以擷取前兩個產品功能  
 下列查詢會從產品型號目錄描述擷取前兩個功能、<`Features`> 元素的前兩個子元素。 如果有更多的功能，它會將 <`there-is-more/`> 元素加入結果中。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **命名空間**關鍵字[XQuery 初構](../xquery/modules-and-prologs-xquery-prolog.md)查詢主體中定義命名空間前置詞使用。  
  
-   查詢主體建構的 XML\<產品 > 項目**ProductModelID**和**ProductModelName**屬性，且具有以子元素傳回的產品功能。  
  
-   **Position （)**函式用於述詞中決定的位置\<功能 > 子元素內容中的。 如果它是第一個或第二個功能，就會傳回它。  
  
-   如果陳述式加入\<該處是更 / > 元素加入結果中，如果產品目錄中有兩個以上的功能。  
  
-   因為並非所有的產品型號都在資料表中儲存目錄描述，所以將使用 WHERE 子句來捨棄 CatalogDescriptions 為 NULL 的 WHERE 子句。  
  
 以下是部份結果：  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
…  
```  
  
## <a name="see-also"></a>請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
