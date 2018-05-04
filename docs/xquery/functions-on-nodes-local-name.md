---
title: local-name 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3844608511c847d1ae87d8ca966d920fbb3cc658
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-nodes---local-name"></a>節點的本機名稱的函式
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回本機名稱部份 *$arg* xs: string 會是零長度字串，或將會有 xs: ncname 的語彙格式。 如果沒有提供引數，預設值是內容節點。  
  
## <a name="syntax"></a>語法  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 將會擷取節點名稱的本機名稱部份。  
  
## <a name="remarks"></a>備註  
  
-   在 SQL Server， **fn:local-name()** 不只可以在內容相依述詞的內容中使用的引數。 具體而言，它只能在括號 (`[ ]`) 內使用。  
  
-   如果提供引數，而且是空白時序，函數會傳回零長度的字串。  
  
-   如果目標節點沒有名稱，因為它是文件節點、註解或文字節點，函數會傳回零長度的字串。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
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
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>B. 使用述詞中沒有引數的本機名稱  
 下列查詢針對具類型的 Instructions 資料行指定**xml** ProductModel 資料表的資料行。 運算式會傳回 QName 本機名稱部份為 "Location" 的 <`root`> 元素之所有的元素子系。 **Local-name （)** 函式是述詞中的指定，且它沒有任何函數會使用內容節點的引數。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 查詢會傳回 <`root`> 元素的所有 <`Location`> 元素子系。  
  
## <a name="see-also"></a>另請參閱  
 [在節點上的函式](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [namespace-uri 函數&#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
