---
title: "除 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6d139460bac6aa653da3d378de1c1b4c3cb80869
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="divide-mdx"></a>除 (MDX)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  執行除法運算，並傳回替代結果或除以 0 的 BLANK()。  
  
## <a name="syntax"></a>語法  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>引數  
 *分子*  
 被除數或要除以的數字。  
  
 *分母*  
 除數或要除的數字。  
  
 *alternateresult*  
 (選擇性) 除以零產生錯誤結果時所傳回的值。 未提供時，預設值為 BLANK()。  
  
## <a name="remarks"></a>備註  
 除以 0 的替代結果必須是常數。  
  
## <a name="see-also"></a>請參閱＜  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
