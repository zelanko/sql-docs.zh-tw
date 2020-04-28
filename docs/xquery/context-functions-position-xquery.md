---
title: position 函數（XQuery） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
author: rothja
ms.author: jroth
ms.openlocfilehash: de9f30c3c63030aa956366c222b7cbda94e2becb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038977"
---
# <a name="context-functions---position-xquery"></a>內容函式 - position (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回整數值，以指出目前所處理的項目序列中內容項目的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>備註  
 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中， **fn： position （）** 只能用於內容相依述詞的內容中。 具體而言，它只能用於括號 ([ ]) 內。針對此函數所做的比較不會在靜態類型推斷期間減少基數。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存**xml**在資料庫的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]各種 XML 類型資料行中。  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. 使用 position() XQuery 函數以擷取前兩個產品功能  
 下列查詢會從產品型號目錄描述中，抓取前兩個功能，也`Features`就是 <> 元素的前兩個子項目。 如果有更多的功能，它會將`there-is-more/` <> 元素新增至結果。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
-   [XQuery](../xquery/modules-and-prologs-xquery-prolog.md)初構中的**namespace**關鍵字會定義在查詢主體中使用的命名空間前置詞。  
  
-   查詢主體會使用具有\< **ProductModelID**和**ProductModelName**屬性的產品> 專案來建立 XML，並將產品功能當做子項目傳回。  
  
-   **Position （）** 函式會在述詞中用來判斷\<功能> 子專案在內容中的位置。 如果它是第一個或第二個功能，就會傳回它。  
  
-   如果產品目錄中有\<兩個以上的功能，if 語句會 > 將此專案新增至結果。  
  
-   因為並非所有的產品型號都在資料表中儲存目錄描述，所以將使用 WHERE 子句來捨棄 CatalogDescriptions 為 NULL 的 WHERE 子句。  
  
 以下是部份結果：  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
