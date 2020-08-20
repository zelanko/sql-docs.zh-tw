---
description: OR (MDX)
title: 或 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d5ea3e65dd9bad768ef829858d42d6e4adea7a72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471750"
---
# <a name="or-mdx"></a>OR (MDX)


  在兩個數值運算式上執行邏輯分離。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>參數  
 Expression1  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
 Expression2  
 傳回數值的有效 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值，如果其中一個或兩個引數都評估為**true**，則傳回**true** ;否則**為 false**。  
  
## <a name="remarks"></a>備註  
 **OR**運算子會將兩個引數視為布林值 (零、0、為**false**;否則，在運算子執行邏輯分離之前，) **true** 。 下表說明 **或** 運算子如何執行邏輯分離。  
  
|*Expression1*|*Expression2*|傳回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>範例  
 下列查詢包含匯出量值，如果客戶維度的性別階層上的目前成員為男性，或 Customer 維度之婚姻狀態階層上的目前成員已結婚，則會傳回字串 "結婚或男性";否則，它會傳回字串 "UNMARRIED OR 女性"。  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
