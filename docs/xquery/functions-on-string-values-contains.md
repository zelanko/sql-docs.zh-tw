---
title: 包含函式 (XQuery) |Microsoft Docs
description: 瞭解如何在 XQuery 中使用 contains 函式來判斷指定的字串值是否包含指定的子字串值。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c1f313a5316059a05cb30a5af6ef7a451353a3d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724220"
---
# <a name="functions-on-string-values---contains"></a>字串值的相關函式 - contains
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  傳回 xs： boolean 類型的值，指出 *$arg 1* 的值是否包含 *$arg 2*所指定的字串值。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>引數  
 *$arg 1*  
 要測試的字串值。  
  
 *$arg2*  
 要尋找的子字串。  
  
## <a name="remarks"></a>備註  
 如果 *$arg 2* 的值是長度為零的字串，則函數會傳回 **True**。 如果 *$arg 1* 的值是長度為零的字串，而 *$arg 2* 的值不是長度為零的字串，則函數會傳回 **False**。  
  
 如果 *$arg 1* 或 *$arg 2* 的值是空的序列，則會將引數視為零長度的字串。  
  
 contains() 函數會使用 XQuery 的預設 Unicode 字碼元素定序來進行字串比較。  
  
 針對 *$arg 2* 指定的子字串值必須小於或等於4000個字元。 如果指定的值大於4000個字元，就會發生動態錯誤狀況，而且 contains ( # A1 函式會傳回空的序列，而不是布林值 **True** 或 **False**。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不會針對 XQuery 運算式引發動態錯誤。  
  
 為了取得不區分大小寫的比較，可以使用 [大寫](../xquery/functions-on-string-values-upper-case.md) 或小寫函數。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱 [SQL Server 2016 中資料庫引擎功能的重大變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)主題中的「XQuery 函式是可代理感知」一節。 另請參閱 [ALTER DATABASE 相容性層級 &#40;transact-sql&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) 和定 [序和 Unicode 支援](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
 本主題針對儲存在 AdventureWorks 資料庫的各種 xml 類型資料行中的 XML 實例提供 XQuery 範例。  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>A. 使用 contains() XQuery 函式來搜尋特定的字元字串  
 下列查詢會尋找產品摘要描述中有包含 Aerodynamic 一詞的產品。 此查詢會傳回 ProductID 和 `Summary` 這類產品的 <> 元素。  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
   /pd:ProductDescription/pd:Summary//text()  
    [contains(., "Aerodynamic")]') = 1  
```  
  
 結果  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `28     <Prod ProductModelID="28">`  
  
 `<pd:Summary xmlns:pd=`  
  
 `"https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
