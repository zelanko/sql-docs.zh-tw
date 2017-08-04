---
title: "分葉 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LEAVES
dev_langs:
- kbMDX
helpviewer_keywords:
- Leaves function
ms.assetid: 09f908aa-1b2d-4af9-8c8d-c023915241b2
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0c6201939c5bfb6f5ad61c009aac5a7e4740af63
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="leaves-mdx"></a>Leaves (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一組由所有屬性 (選擇性地限定屬於特定維度的屬性) 組成的集合。 對於傳回集合中的每個屬性 x，如果 x 是資料粒度屬性或是與資料粒度屬性直接或間接相關，則會在屬性 x 上設定資料粒度，而不會影響配量。 **離開**函數設計用於 SCOPE 陳述式內或指派的左側。  
  
## <a name="syntax"></a>語法  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>引數  
 *Dimension_Expression*  
 傳回維度的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 分葉成員是 Tuple，由所有屬性階層之最低層級的交叉聯結所形成。 導出成員被排除在外。  
  
-   如果指定維度名稱，則**離開**函式會傳回包含指定之維度的索引鍵屬性的分葉成員的集合。  
  
-   如果此維度與多個量值群組有關聯，則會使用目前範圍中的其中一個量值。  
  
-   如果沒有指定維度名稱，此函數會傳回包含整個 Cube 之分葉成員的集合。  
  
    > [!NOTE]  
    >  如果維度運算式解析成階層，並且階層唯一名稱與維度唯一名稱相同 (Cube 維度屬性 HierarchyUniqueNameStyle=ExcludeDimensionName，並且階層名稱=維度名稱)，則會使用維度。  
  
    > [!IMPORTANT]  
    >  如果目前範圍內量值群組上的所有屬性沒有相同的資料粒度，則會產生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

