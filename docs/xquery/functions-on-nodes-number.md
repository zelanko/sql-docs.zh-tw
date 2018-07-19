---
title: 數字函數 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 65faec31c6e89421ce05bab28dae97e18195bdde
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031516"
---
# <a name="functions-on-nodes---number"></a>節點數目的相關函式
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  傳回的節點所表示的數值 *$arg*。  
  
## <a name="syntax"></a>語法  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 節點值將以數字傳回。  
  
## <a name="remarks"></a>備註  
 如果 *$arg*是未指定，會傳回內容節點，並轉換為雙精度浮點數，數字值。 在 SQL Server **fn:number()** 沒有引數僅適用於內容相依述詞的內容中。 具體而言，它只能在括號 ([ ]) 內使用。 例如，下列運算式會傳回 <`ROOT`> 元素。  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 如果節點的值不是數值簡單類型的有效語彙表示法中所定義**XML 結構描述組件 2:Datatypes，W3C 建議事項**，此函數會傳回空的序列。 不支援 NaN。  
  
## <a name="examples"></a>範例  
 本主題提供 XQuery 範例，針對 XML 執行個體儲存在各種**xml**類型資料行中的 AdventureWorks 資料庫。  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. 使用 number() XQuery 函數擷取屬性的數值  
 下列查詢會從第一個工作中心位置的製造產品型號 7 之過程中，擷取配置大小屬性的數值。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
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
  
-   **Number （)** 函式不是必要項，針對查詢所示**LotSizeA**屬性。 這是 XPath 1.0 函數，主要是基於回溯相容性而包含它。  
  
-   針對 XQuery **LotSizeB**指定 number 函數和冗餘。  
  
-   查詢**LotSizeD**說明中的算術運算的數字值的使用方式。  
  
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
  
-   **Number （)** 函式只接受節點。 它不接受不可部份完成值。  
  
-   無法傳回值，表示為數字，當**number （)** 函式會傳回空的序列，而不是 NaN。  
  
## <a name="see-also"></a>另請參閱  
 [針對 xml 資料類型的 XQuery 函式](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
