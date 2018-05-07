---
title: 層級 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Levels
dev_langs:
- kbMDX
helpviewer_keywords:
- Levels function
ms.assetid: 1a989cc9-8aa8-4ec3-b5e9-795d6fa84983
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 3e50783a6d59315441f76549f32607d17a2100c0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="levels-mdx"></a>Levels (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回層級，而其在維度或階層中的位置是由數值運算式指定，或者其名稱是由字串運算式指定。  
  
## <a name="syntax"></a>語法  
  
```  
  
Numeric expression syntax  
Hierarchy_Expression.Levels( Level_Number )  
  
String expression syntax  
Hierarchy_Expression.Levels( Level_Name )  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Number*  
 指定層級編號的有效數值運算式。  
  
 *L*  
 指定層級名稱的有效字串運算式。  
  
## <a name="remarks"></a>備註  
 如果指定層級編號，**層級**函式會傳回與指定的以零為起始位置相關聯的層級。  
  
 如果指定層級的名稱，則**層級**函式會傳回指定層級。  
  
> [!NOTE]  
>  對於使用者自訂函數，請使用字串運算式語法。  
  
## <a name="examples"></a>範例  
 下列範例將說明每個**層級**函數的語法。  
  
### <a name="numeric"></a>數值  
 下列範例會傳回 Country 層級：  
  
```  
SELECT [Geography].[Geography].Levels(1) ON 0  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>字串  
 下列範例會傳回 Country 層級：  
  
```  
SELECT [Geography].[Geography].Levels('Country') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
