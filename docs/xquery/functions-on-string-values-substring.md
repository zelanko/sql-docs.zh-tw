---
title: substring 函數 (XQuery) |Microsoft Docs
description: '瞭解會傳回來源字串指定部分 ( # A1 的 XQuery 函數子字串。'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a4881fc4710ba56439eb98b5b196af93247c11f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768153"
---
# <a name="functions-on-string-values---substring"></a>字串值的相關函式 - substring
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  傳回 *$sourceString*值的一部分，從 *$startingLoc* 的值所指示的位置開始，並繼續進行 *$length*的值所指出的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>引數  
 *$sourceString*  
 來源字串。  
  
 *$startingLoc*  
 來源字串中子字串開始的起點。 如果此值是負數或 0，則只傳回位置大於 0 的那些字元。 如果大於 *$sourceString*的長度，則會傳回長度為零的字串。  
  
 *$length*  
 [選擇性] 要擷取的字元數。 如果未指定，則會從 *$startingLoc* 中指定的位置傳回所有的字元到字串結尾。  
  
## <a name="remarks"></a>備註  
 此函數的三引數版本會傳回 `$sourceString` 中位置 `$p` 遵守的字元數：  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 *$Length*的值可以大於開始位置之後 *$sourceString*值中的字元數。 在此情況下，子字串會傳回 *$sourceString*結尾的字元。  
  
 字串的第一個字元是在位置 1。  
  
 如果 *$sourceString* 的值是空的序列，則會以零長度的字串來處理。 否則，如果 *$startingLoc* 或 *$length* 是空的序列，則會傳回空的序列。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱 [SQL Server 2016 中資料庫引擎功能的重大變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)主題中的「XQuery 函式是可代理感知」一節。 另請參閱 [ALTER DATABASE 相容性層級 &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 和定 [序和 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="implementation-limitations"></a>實作限制  
 SQL Server 需要 *$startingLoc* 和 *$length 參數* 的類型為 xs： decimal，而非 xs： double。  
  
 SQL Server 可讓 *$startingLoc* 和 *$length* 成為空的序列，因為空的序列是將動態錯誤對應到 ( # A1 的結果可能值。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在資料庫的各種 **xml** 類型資料行中 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 。  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. 使用 substring() XQuery 函式擷取產品型號描述的部分摘要  
 查詢會抓取描述產品型號之文字的前50個字元，也就是 `Summary` 檔中 <> 元素。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   **字串 ( # B1**函數會傳回<> 元素的字串值 `Summary` 。 使用這個函式是因為 <`Summary`> 專案同時包含文字和子項目 (html 格式設定元素) ，而且因為您將略過這些元素並取出所有文字。  
  
-   **子字串 ( # B1**函數會從**字串 ( # B3**取出的字串值抓取前50個字元。  
  
 以下是部份結果：  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
