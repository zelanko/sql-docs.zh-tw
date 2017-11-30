---
title: "會導致 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LEAD
dev_langs: kbMDX
helpviewer_keywords: Lead function
ms.assetid: f3250092-7b98-40b5-8dca-77e3b50734a0
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 03512a3e07e9b041f794bbdc75ba067539a28e24
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="lead-mdx"></a>Lead (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回成員層級中，在特定成員之後特定幾個位置的成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Index*  
 指定成員位置數目的有效數值運算式。  
  
## <a name="remarks"></a>備註  
 層級內的成員位置是由屬性階層的自然順序決定。 位置的編號是以零為基底。  
  
 如果指定的開頭是零 (0)，**導致**函式會傳回指定的成員。  
  
 如果指定的開頭是負數，**導致**函式傳回之前的成員。  
  
 `Lead(1)`相當於[NextMember](../mdx/nextmember-mdx.md)函式。 `Lead(-1)`相當於[PrevMember](../mdx/prevmember-mdx.md)函式。  
  
 **導致**函數很相似[延隔](../mdx/lag-mdx.md)函式中，不同處在於**延隔**函式會以相反的方向，以尋找**導致**函式。 也就是說，`Lead(n)` 相當於 `Lag(-n)`。  
  
## <a name="example"></a>範例  
 下列範例會傳回 2001 年 12 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 下列範例會傳回 2002 年 3 月的值：  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
