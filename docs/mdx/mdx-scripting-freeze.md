---
title: FREEZE 陳述式 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b7eb3a3939ce8525dc57d27a24ac005ecb2cf2d
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579900"
---
# <a name="mdx-scripting---freeze"></a>MDX 指令碼-凍結
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  將指定的 Subcube 資料格的值鎖定為它們目前的值。 鎖定資料格值時，其他資料格的變更對已鎖定的資料格沒有影響。  
  
## <a name="syntax"></a>語法  
  
```  
  
FREEZE Subcube_Expression   
```  
  
## <a name="arguments"></a>引數  
 *Subcube_Expression*  
 傳回 Subcube 的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **凍結**陳述式會鎖定指定 subcube 中的資料格的值，防止在 MDX 中的後續陳述式的指令碼從變更中後續的計算其值會傳遞。  
  
 在下列範例中，A 與 B 代表 MDX 計算指令碼中的 Subcube：  
  
```  
B = 2;  
A = B;  
B = 3  
```  
  
 此時，A 與 B 都等於 3。  
  
 我們現在插入**凍結**函數來鎖定 A subcube 中的資料格：  
  
```  
B = 2;  
A = B;  
FREEZE(A);  
B = 3  
```  
  
 A 現在等於 2，而 B 等於 3。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼陳述式&#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
