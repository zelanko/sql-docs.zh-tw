---
description: Leaves (MDX)
title: 離開 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7beab859a2953b3eba52e74d97bed5718c59ea90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387304"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  傳回一組由所有屬性 (選擇性地限定屬於特定維度的屬性) 組成的集合。 對於傳回集合中的每個屬性 x，如果 x 是資料粒度屬性或是與資料粒度屬性直接或間接相關，則會在屬性 x 上設定資料粒度，而不會影響配量。 「 **葉子** 」函數的設計目的是在範圍語句或指派的左側使用。  
  
## <a name="syntax"></a>語法  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Dimension_Expression*  
 傳回維度的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 分葉成員是 Tuple，由所有屬性階層之最低層級的交叉聯結所形成。 導出成員被排除在外。  
  
-   如果指定了維度名稱，則「 **離開** 」函數會傳回一個集合，其中包含指定維度之索引鍵屬性（attribute）的分葉成員。  
  
-   如果此維度與多個量值群組有關聯，則會使用目前範圍中的其中一個量值。  
  
-   如果沒有指定維度名稱，此函數會傳回包含整個 Cube 之分葉成員的集合。  
  
    > [!NOTE]  
    >  如果維度運算式解析成階層，並且階層唯一名稱與維度唯一名稱相同 (Cube 維度屬性 HierarchyUniqueNameStyle=ExcludeDimensionName，並且階層名稱=維度名稱)，則會使用維度。  
  
    > [!IMPORTANT]  
    >  如果目前範圍內量值群組上的所有屬性沒有相同的資料粒度，則會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
