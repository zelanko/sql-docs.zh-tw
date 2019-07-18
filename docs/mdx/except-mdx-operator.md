---
title: '- （除外）(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf0121d1be3cd2943a801f3c72ca4952b70ec681
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139075"
---
# <a name="except-mdx-operator"></a>Except 運算子 (MDX)


  執行集合運算，傳回兩個集合間的差異、移除重複的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>參數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
## <a name="return-value"></a>傳回值  
 集合包含的成員不由兩個指定的參數共用。  
  
## <a name="remarks"></a>備註  
 **-（例外）** 運算子在功能上等於[除了](../mdx/except-mdx-function.md)函式。  
  
## <a name="examples"></a>範例  
 以下範例示範此運算子的用法：  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
