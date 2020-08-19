---
description: FREEZE 陳述式 (MDX)
title: 凍結語句 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 41c71987fec932b2693740792a8d86e200fcf526
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429740"
---
# <a name="mdx-scripting---freeze"></a>MDX 指令碼 - FREEZE


  將指定的 Subcube 資料格的值鎖定為它們目前的值。 鎖定資料格值時，其他資料格的變更對已鎖定的資料格沒有影響。  
  
## <a name="syntax"></a>語法  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>引數  
 *Subcube_Expression*  
 傳回 Subcube 的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **凍結**語句會鎖定指定之子集中的資料格值，防止 MDX 腳本中的後續語句在後續的計算階段中變更其值。  
  
 在下列範例中，A 與 B 代表 MDX 計算指令碼中的 Subcube：  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 此時，A 與 B 都等於 3。  
  
 現在，我們會插入 **凍結** 函數來鎖定子集中的儲存格：  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 A 現在等於 2，而 B 等於 3。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼陳述式 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
