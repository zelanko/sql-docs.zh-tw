---
title: number 函數（XQuery） |Microsoft Docs
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31a52f86692d5769fe22f4cf0b5a04ad324c3ac0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930110"
---
# <a name="functions-on-nodes---number"></a>節點的相關函式 - number
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回 *$arg*所表示的節點數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 節點值將以數字傳回。  
  
## <a name="remarks"></a>備註  
 如果未指定 *$arg* ，則會傳回內容節點的數值（轉換為 double）。 在 SQL Server 中，沒有引數的**fn： number （）** 只可用於內容相依述詞的內容中。 具體而言，它只能在括號 ([ ]) 內使用。 例如，下列運算式會傳回 <`ROOT`> 元素。  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 如果節點的值不是數值簡單類型的有效詞法標記法，如**XML 架構第2部分：資料類型、W3C 建議事項**中所定義，函數會傳回空的序列。 不支援 NaN。  
  
## <a name="examples"></a>範例  
 本主題針對儲存在 AdventureWorks 資料庫的各種**xml**類型資料行中的 xml 實例提供 XQuery 範例。  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. 使用 number() XQuery 函數擷取屬性的數值  
 下列查詢會從第一個工作中心位置的製造產品型號 7 之過程中，擷取配置大小屬性的數值。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 請注意下列項目是從上一個查詢而來：  
  
-   不需要**number （）** 函數，如**LotSizeA**屬性的查詢所示。 這是 XPath 1.0 函數，主要是基於回溯相容性而包含它。  
  
-   **LotSizeB**的 XQuery 會指定 number 函數，而且是多餘的。  
  
-   **LotSizeD**的查詢說明如何在算數運算中使用數位值。  
  
 以下是結果：  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>實作限制  
 以下為其限制：  
  
-   **Number （）** 函數只接受節點。 它不接受不可部份完成值。  
  
-   當值無法當做數位傳回時， **number （）** 函數會傳回空的序列，而不是 NaN。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函數](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
