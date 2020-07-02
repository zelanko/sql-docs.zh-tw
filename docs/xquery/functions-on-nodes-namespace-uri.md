---
title: namespace-uri 函數（XQuery） |Microsoft Docs
description: 瞭解如何在 XQuery 中使用 namespace uri 函式，以傳回指定之 QName 的命名空間 URI。
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
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
author: rothja
ms.author: jroth
ms.openlocfilehash: e22aadcb6da106c28ff38fc5b9d455f04152d0ec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753595"
---
# <a name="functions-on-nodes---namespace-uri"></a>節點的相關函式 - namespace-uri
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

  傳回在 *$arg*中指定之 QName 的命名空間 URI，其為 xs： string。  
  
## <a name="syntax"></a>語法  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 將要擷取其命名空間 URI 部份的節點名稱。  
  
## <a name="remarks"></a>備註  
  
-   如果省略此引數，預設值就是內容節點。  
  
-   在 SQL Server 中，沒有引數的**fn： namespace-uri （）** 只能用於內容相依述詞的內容中。 具體而言，它只能在括號 ([ ]) 內使用。  
  
-   如果 *$arg*是空的序列，則會傳回長度為零的字串。  
  
-   如果 *$arg*是專案或屬性節點，其擴充的 QName 不在命名空間中，則函式會傳回長度為零的字串  
  
## <a name="examples"></a>範例  
 本主題針對儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中的 xml 實例提供 XQuery 範例。  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. 擷取特定節點的命名空間 URI  
 下列查詢是針對不具類型的 XML 執行個體所指定。 查詢運算式 `namespace-uri(/ROOT[1])` 將會擷取指定節點的命名空間 URI 部份。  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 因為指定的 QName 沒有命名空間 URI 部份，而只有本機名稱部份，所以結果是長度為零的字串。  
  
 下列查詢是針對指示類型的**xml**資料行所指定。 運算式會傳回 `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` <> 專案之第一個 <> 元素子系的命名空間 URI `Location` `root` 。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 以下是結果：  
  
```  
https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. 使用述詞中沒有引數的 namespace-uri()  
 以下查詢是針對已指定 CatalogDescription 類型的 xml 資料行而指定。 運算式會將命名空間 URI 為 `https://www.adventure-works.com/schemas/OtherFeatures` 的所有元素節點傳回。 指定了 namespace-**uri （）** 函數，但沒有引數，並使用內容節點。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "https://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部份結果：  
  
```  
<p1:wheel xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="https://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
...  
```  
  
 您可以將上一個查詢中的命名空間 URI 變更為 `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`。 接著，您將會收到 <> 元素的所有元素節點子系， `ProductDescription` 其已展開的 QName 的命名空間 URI 部分為 `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain` 。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Namespace-uri （）** 函數會傳回 xs： string 類型的實例，而不是 Xs： anyURI。  
  
## <a name="see-also"></a>另請參閱  
 [節點上的函式](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [&#40;XQuery&#41;的本機名稱函數](../xquery/functions-on-nodes-local-name.md)  
  
  
