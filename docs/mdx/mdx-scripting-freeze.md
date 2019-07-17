---
title: FREEZE 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4738dab411fe55808034a6d9d81a16994089ea74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138292"
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
 **凍結**陳述式會鎖定指定 subcube 中的儲存格的值，防止在 MDX 中的後續陳述式無法變更其值在後續計算中的指令碼將傳遞。  
  
 在下列範例中，A 與 B 代表 MDX 計算指令碼中的 Subcube：  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 此時，A 與 B 都等於 3。  
  
 我們現在插入**凍結**函式鎖定 A subcube 中的資料格：  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 A 現在等於 2，而 B 等於 3。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼陳述式 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
