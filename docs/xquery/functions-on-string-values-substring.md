---
title: "substring 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2fbe33b349def61c3b093079554db626b56f2f09
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-string-values---substring"></a>字串值的子字串的函式
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回值的部分*$sourceString*處的值所指定的位置開始， *$startingLoc，*並繼續進行的值所指示的字元數*$長度*。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc  as as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>引數  
 *$sourceString*  
 來源字串。  
  
 *$startingLoc*  
 來源字串中子字串開始的起點。 如果此值是負數或 0，則只傳回位置大於 0 的那些字元。 如果大於的長度*$sourceString*，會傳回零長度字串。  
  
 *$length*  
 [選擇性] 要擷取的字元數。 如果未指定，它會傳回所有字元中指定的位置*$startingLoc*到字串的結尾。  
  
## <a name="remarks"></a>備註  
 此函數的三引數版本會傳回 `$sourceString` 中位置 `$p` 遵守的字元數：  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 值*$length*可能的值中的字元數大於*$sourceString*遵循開始位置。 在此情況下，則 substring 會傳回之前的結尾的字元*$sourceString*。  
  
 字串的第一個字元是在位置 1。  
  
 如果值*$sourceString*是空的序列，它以零長度字串來處理。 否則，如果*$startingLoc*或*$length*是空的序列，傳回空的序列。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱主題中的 「 XQuery 函式是 Surrogate 感知 」 區段[SQL Server 2016 中對於 Database Engine 功能的突破性變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另請參閱[ALTER DATABASE 相容性層級 &#40;TRANSACT-SQL &#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="implementation-limitations"></a>實作限制  
 SQL Server 需要*$startingLoc*和*$length 參數*是而不是 xs: double 類型 xs: decimal。  
  
 SQL Server 允許*$startingLoc*和*$length*是空的序列，因為空的序列是動態錯誤對應到 （） 的結果可能的值。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫。  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. 使用 substring() XQuery 函式擷取產品型號描述的部分摘要  
 此查詢會擷取產品型號描述文字的前 50 個字元，即文件中的 <`Summary`> 元素。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **String （)**函式會傳回的字串值 <`Summary`> 項目。 會使用此函數，是因為 <`Summary`> 元素同時包含文字和子元素 (html 格式設定元素)，而且因為您會略過這些元素而擷取所有文字。  
  
-   **Substring （)**函式會擷取前 50 個字元的字串值，來擷取從**string （)**。  
  
 以下是部份結果：  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
