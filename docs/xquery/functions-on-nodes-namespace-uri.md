---
title: namespace-uri 函數 (XQuery) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
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
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a42004892b2bcfc5f51dd02ab2d43618333d466d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="functions-on-nodes---namespace-uri"></a>節點的命名空間 uri 相關函數
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回的命名空間 URI 中指定之 QName *$arg* xs: string。  
  
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
  
-   在 SQL Server， **fn:namespace-uri()** 不只可以在內容相依述詞的內容中使用的引數。 具體而言，它只能在括號 ([ ]) 內使用。  
  
-   如果 *$arg*是空的序列，則傳回零長度字串。  
  
-   如果 *$arg*是項目或屬性節點，其擴充 QName 不在命名空間，此函式會傳回零長度字串  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型 AdventureWorks 資料庫中的資料行。  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. 擷取特定節點的命名空間 URI  
 下列查詢是針對不具類型的 XML 執行個體所指定。 查詢運算式 `namespace-uri(/ROOT[1])` 將會擷取指定節點的命名空間 URI 部份。  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 因為指定的 QName 沒有命名空間 URI 部份，而只有本機名稱部份，所以結果是長度為零的字串。  
  
 下列查詢針對 Instructions 類型指定**xml**資料行。 運算式 `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` 將會傳回 <`root`> 元素之第一個 <`Location`> 元素子系的命名空間 URI。  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 以下是結果：  
  
```  
http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. 使用述詞中沒有引數的 namespace-uri()  
 以下查詢是針對已指定 CatalogDescription 類型的 xml 資料行而指定。 運算式會將命名空間 URI 為 `http://www.adventure-works.com/schemas/OtherFeatures` 的所有元素節點傳回。 命名空間-**uri （)** 函式已指定沒有引數，並使用內容節點。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "http://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 以下是部份結果：  
  
```  
<p1:wheel xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="http://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
…  
```  
  
 您可以將上一個查詢中的命名空間 URI 變更為 `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`。 接著，您將會收到 <`ProductDescription`> 元素的所有元素節點子系，而該元素之擴充 QName 的命名空間 URI 部份為 `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`。  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Namespace-uri （)** 函式傳回類型 xs: string，而不是 xs: anyuri 的執行個體。  
  
## <a name="see-also"></a>另請參閱  
 [在節點上的函式](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [local-name 函數&#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
  
