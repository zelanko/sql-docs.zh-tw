---
title: UniqueName (MDX) |Microsoft 文件
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
- UNIQUENAME
dev_langs:
- kbMDX
helpviewer_keywords:
- UniqueName function
ms.assetid: f186094e-670c-401c-a82f-6b634b3f71f5
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9c68a32d649cf9042e173dc3fa79b73a5c820b98
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="uniquename-mdx"></a>UniqueName (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回指定維度、階層、層級或成員的唯一名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
Dimension expression syntax  
Dimension_Expression.UniqueName  
  
Hierarchy expression syntax  
Hierarchy_Expression.UniqueName  
  
Level expression syntax  
Level_Expression.UniqueName  
  
Member expression syntax  
Member_Expression.UniqueName  
```  
  
## <a name="arguments"></a>引數  
 *Dimension_Expression*  
 解析成維度的有效多維度運算式 (MDX) 運算式。  
  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **UniqueName**函式會傳回物件，而不是所傳回的名稱的唯一名稱[名稱](../mdx/name-mdx.md)函式。 所傳回的名稱不包含 Cube 的名稱。 所傳回的結果相依於伺服器端設定或 MDX 唯一名稱樣式的連接字串屬性。  
  
## <a name="example"></a>範例  
 下列範例會傳回 Adventure Works Cube 中 Product 維度、Product Categories 階層、Subcategory 層級及 Bike Racks 成員的唯一名稱值。  
  
```  
WITH MEMBER DimensionUniqueName   
   AS [Product].UniqueName  
MEMBER HierarchyUniqueName   
   AS [Product].[Product Categories].UniqueName  
MEMBER LevelUniqueName   
   AS [Product].[Product Categories].[Subcategory].UniqueName  
MEMBER MemberUniqueName   
   AS [Product].[Product Categories].[Subcategory].[Bike Racks]  
SELECT   
   {DimensionUniqueName  
   , HierarchyUniqueName  
   , LevelUniqueName  
   , MemberUniqueName }  
   ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
