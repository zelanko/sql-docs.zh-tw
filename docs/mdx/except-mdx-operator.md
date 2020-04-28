---
title: '- 但是（MDX） |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf0121d1be3cd2943a801f3c72ca4952b70ec681
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139075"
---
# <a name="except-mdx-operator"></a>Except （MDX）運算子


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
 **-（Except）** 運算子的功能等同于[Except](../mdx/except-mdx-function.md)函數。  
  
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
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
