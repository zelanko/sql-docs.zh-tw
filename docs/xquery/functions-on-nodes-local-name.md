---
title: " (XQuery) 的本機名稱函數 |Microsoft Docs"
description: '瞭解如何使用 XQuery 函數區功能變數名稱稱 ( # A1 來傳回節點的本機名稱部分。'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
author: rothja
ms.author: jroth
ms.openlocfilehash: dc7c25d1b953b98c81691843a4de6dc924bca651
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038067"
---
# <a name="functions-on-nodes---local-name"></a>節點的相關函式 - local-name
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  以 xs： string 傳回 *$arg* 名稱的本機部分，該字串會是長度為零的字串，或具有 Xs： NCName 的詞法形式。 如果沒有提供引數，預設值是內容節點。  
  
## <a name="syntax"></a>語法  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 將會擷取節點名稱的本機名稱部份。  
  
## <a name="remarks"></a>備註  
  
-   在 SQL Server 中，沒有引數的 **fn： local-name ( # B1 ** 只能用於內容相依述詞的內容中。 具體而言，它只能在括號 (`[ ]`) 內使用。  
  
-   如果提供引數，而且是空白時序，函數會傳回零長度的字串。  
  
-   如果目標節點沒有名稱，因為它是文件節點、註解或文字節點，函數會傳回零長度的字串。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在 AdventureWorks 資料庫的各種 **xml** 類型資料行中。  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. 擷取特定節點的本機名稱  
 下列查詢是針對不具類型的 XML 執行個體所指定。 查詢運算式 `local-name(/ROOT[1])` 會擷取指定節點的本機名稱部份。  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 下列查詢是針對 ProductModel 資料表的 Instructions 資料行 (具類型的 xml 資料行) 所指定。 運算式 `local-name(/AWMI:root[1]/AWMI:Location[1])` 會傳回指定節點的本機名稱 `Location`。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. 使用述詞中沒有引數的本機名稱  
 下列查詢是針對 ProductModel 資料表的指示資料行（具類型的 **xml** 資料行）所指定。 運算式會傳回 <> 專案的所有元素子系，而 `root` QName 的本機名稱部分為 "Location"。 在述詞中指定了 **區功能變數名稱稱 ( # B1 函式 ** ，且函式不會使用內容節點。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 此查詢會傳回 `Location` <> 元素的所有 <> 元素子系 `root` 。  
  
## <a name="see-also"></a>另請參閱  
 [節點上的函數](./xquery-functions-against-the-xml-data-type.md)   
 [命名空間 uri 函式 &#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
