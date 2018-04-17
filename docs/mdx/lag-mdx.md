---
title: Lag (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LAG
dev_langs:
- kbMDX
helpviewer_keywords:
- Lag function
ms.assetid: 08c704ea-35d8-44ee-abe5-93bd24b99906
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a219e0b8455ff3a66d20a8c670bb8675481498e4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="lag-mdx"></a>Lag (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回成員層級中，在特定成員之前特定幾個位置的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Index*  
 指定落後的成員位置數目之有效數值運算式。  
  
## <a name="remarks"></a>備註  
 層級內的成員位置是由屬性階層的自然順序決定。 位置的編號是以零為基底。  
  
 如果指定的落後是零，**延隔**函式會傳回指定的成員本身。  
  
 如果指定的落後是負數，**延隔**函式會傳回後續成員。  
  
 `Lag(1)`相當於[PrevMember](../mdx/prevmember-mdx.md)函式。 `Lag(-1)`相當於[NextMember](../mdx/nextmember-mdx.md)函式。  
  
 **延隔**函數很相似[導致](../mdx/lead-mdx.md)函式中，不同處在於**導致**函式會以相反的方向，以尋找**延隔**函式。 也就是說，`Lag(n)` 相當於 `Lead(-n)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
