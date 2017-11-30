---
title: "AllMembers (MDX) |Microsoft 文件"
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
f1_keywords: ALLMEMBERS
dev_langs: kbMDX
helpviewer_keywords: AllMembers function
ms.assetid: 202e81d4-d2ee-4ec1-a019-4835eb19f446
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b4953bd5bff4ab578cc492991918ee5c90abb7a1
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  評估階層或層級運算式，並且傳回集合，其中包含指定之階層或層級的所有成員，包括階層或層級中的所有導出成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>引數  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 傳回層級的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **AllMembers**函式會傳回一組，包含所有成員，其中包含導出的成員、 指定的階層或層級中。 **AllMembers**函式會傳回導出的成員，即使指定的階層或層級包含沒有可見的成員。  
  
> [!IMPORTANT]  
>  當維度只包含單一可見的階層，該階層可由維度名稱或階層名稱參考，因為此狀況下維度名稱會解析成其唯一可見的階層。 例如，`Measures.AllMembers` 即是有效的 MDX 運算式，因為它解析成量值維度上唯一的階層。  
  
> [!NOTE]  
>  **AllMembers**函式會與語意相似[AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md)函式。  
  
## <a name="examples"></a>範例  
 下列範例會傳回中的所有成員 [`Date].[Calendar Year]`資料行軸上的屬性階層，這包括導出的成員和集合之所有子系`[Product].[Model Name]`屬性階層中的資料列軸上**Adventure Works** cube。  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 下列範例會傳回中的所有成員**量值**維度資料行在軸上，這包括所有導出的成員和集合之所有子系`[Product].[Model Name]`屬性階層中的資料列軸上**Adventure Works** cube。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>請參閱  
 [AddCalculatedMembers &#40;MDX &#41;](../mdx/addcalculatedmembers-mdx.md)   
 [子系 &#40;MDX &#41;](../mdx/children-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
