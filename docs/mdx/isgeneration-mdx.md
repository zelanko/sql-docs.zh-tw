---
title: "IsGeneration (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: ISGENERATION
dev_langs: kbMDX
helpviewer_keywords: IsGeneration function
ms.assetid: fd11d2e0-d81d-45af-ac45-c98634d05550
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d1b73679fed735599104dd3588d298602e48d3e7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="isgeneration-mdx"></a>IsGeneration (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回指定的成員是否在指定的生成集內。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsGeneration(Member_Expression, Generation_Number)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Generation_Number*  
 指定用來評估指定成員之生成集的有效數值運算式。  
  
## <a name="remarks"></a>備註  
 **IsGeneration**函式會傳回**true**指定的成員是否在指定層代數目。 否則，函數會傳回**false**。 也，如果指定的成員評估為空成員， **IsGeneration**函式會傳回**false**。  
  
 為了生成集索引用途，分葉成員是生成集索引 0。 如果是非分葉成員，首先從指定成員之所有子成員的聯集，取得最高生成集索引，然後在該索引加 1，決定其生成集索引。 因為已決定非分葉成員的生成集索引，所以特定非分葉成員能夠屬於一個以上的生成集。  
  
## <a name="example"></a>範例  
 如果 [Date].[Fiscal].CurrentMember 是第二個生成集的一部分，下列範例會傳回 TRUE：  
  
 `WITH MEMBER MEASURES.ISGENERATIONDEMO AS`  
  
 `IsGeneration([Date].[Fiscal].CURRENTMEMBER, 2)`  
  
 `SELECT {MEASURES.ISGENERATIONDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
