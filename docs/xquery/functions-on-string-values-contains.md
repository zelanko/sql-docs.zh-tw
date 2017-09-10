---
title: "contains 函數 (XQuery) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- contains function (XQuery)
- fn:contains function
ms.assetid: 2c88c015-04fc-429b-84b2-835596a28b65
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 025d47883976e0cf17ef9435d7bf127677a7b5b1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="functions-on-string-values---contains"></a>函式的字串值-包含
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回值的類型 xs: boolean，指出是否值*$arg1*包含所指定的字串值*$arg2*。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:contains ($arg1 as xs:string?, $arg2 as xs:string?) as xs:boolean?  
```  
  
## <a name="arguments"></a>引數  
 *$ arg1*  
 要測試的字串值。  
  
 *$ arg2<*  
 要尋找的子字串。  
  
## <a name="remarks"></a>備註  
 如果值*$arg2*是零長度字串，此函數會傳回**True**。 如果值*$arg1*是零長度字串和值*$arg2*不是零長度字串，此函數會傳回**False**。  
  
 如果值*$arg1*或*$arg2*是空的序列，引數會當成零長度字串。  
  
 contains() 函數會使用 XQuery 的預設 Unicode 字碼元素定序來進行字串比較。  
  
 指定的子字串值*$arg2*必須小於或等於 4000 個字元。 如果指定的值大於 4000 個字元，就會發生動態錯誤狀況，而且 contains （） 函數會傳回空的序列，而不是布林值**True**或**False**。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不會針對 XQuery 運算式引發動態錯誤。  
  
 若要取得不區分大小寫的比較，[大寫](../xquery/functions-on-string-values-upper-case.md)或 lower-case 函式可使用。  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補充字元 (Surrogate 字組)  
 XQuery 函式中 Surrogate 字組的行為相依於資料庫相容性層級，而且在某些情況下，還相依於函式的預設命名空間 URI。 如需詳細資訊，請參閱主題中的 「 XQuery 函式是 Surrogate 感知 」 區段[SQL Server 2016 中對於 Database Engine 功能的突破性變更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)。 另請參閱[ALTER DATABASE 相容性層級 &#40;TRANSACT-SQL &#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)和[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 AdventureWorks 資料庫中的各種 xml 類型資料行中儲存 XML 執行個體。  
  
### <a name="a-using-the-contains-xquery-function-to-search-for-a-specific-character-string"></a>A. 使用 contains() XQuery 函式來搜尋特定的字元字串  
 下列查詢會尋找產品摘要描述中有包含 Aerodynamic 一詞的產品。 此查詢會傳回這類產品的 ProductID 及 <`Summary`> 元素。  
  
```  
--The product model description document uses  
--namespaces. The WHERE clause uses the exit()  
--method of the xml data type. Inside the exit method,  
--the XQuery contains()function is used to  
--determine whether the <Summary> text contains the word  
--Aerodynamic.   
  
USE AdventureWorks  
GO  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
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
  
 `"http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">`  
  
 `A TRUE multi-sport bike that offers streamlined riding and`  
  
 `a revolutionary design. Aerodynamic design lets you ride with`  
  
 `the pros, and the gearing will conquer hilly roads.</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
