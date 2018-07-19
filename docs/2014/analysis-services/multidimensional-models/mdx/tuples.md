---
title: Tuple |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe6e50c914973673806e23495ad15ea4821b7640
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169699"
---
# <a name="tuples"></a>Tuples
  Tuple 可以唯一識別 Cube 中的資料配量。 Tuple 是由維度成員的組合所構成，只要沒有兩個以上的成員屬於相同階層即可。  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>Tuple 中的隱含或預設屬性成員  
 在 MDX 查詢或運算式中定義 Tuple 時，您不需明確包含每個屬性階層的屬性成員。 如果屬性階層的成員沒有明確包含在查詢或運算式中，該屬性階層的預設成員就是 Tuple 中隱含包含的屬性成員。 除非 Cube 中另有明確定義，否則每個屬性階層的預設成員就是 (全部) 成員 (如果 (全部) 成員存在的話)。 如果 (全部) 成員不存在屬性階層中，預設成員就是屬性階層的最上層成員。 除非明確定義了預設量值，否則預設量值就是 Cube 中第一個指定的量值。 如需詳細資訊，請參閱[定義預設成員](../attribute-properties-define-a-default-member.md)和 [DefaultMember &#40;MDX&#41;](/sql/mdx/defaultmember-mdx)。  
  
 例如，藉由明確定義 Measures 維度的單一成員，下列 Tuple 會識別 Adventure Works 資料庫中的單一資料格。  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 上述範例唯一識別由 Measures 維度之 Reseller Sales Amount 成員及 Cube 中每個屬性階層之預設成員組成的資料格。 除了 Destination Currency 屬性階層，每個屬性階層的預設成員都是 (全部) 成員。 Destination Currency 階層的預設成員是 US Dollar 成員 (這個預設成員是在 Adventure Works Cube 的 MDX 指令碼中定義的)。  
  
 下列查詢會傳回上述範例中指定 Tuple 所參考之資料格的值：($80,450.596.98)。  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  當您在查詢中指定集合 (此處由單一 Tuple 組成) 的座標軸時，必須先指定資料行軸的集合，然後指定資料列軸的集合。 資料行軸也可以用 *axis(0)* 或僅僅 *0* 的方式來代表。 如需 MDX 查詢的詳細資訊，請參閱[基本 MDX 查詢 &#40;MDX&#41;](mdx-query-the-basic-query.md)。  
  
### <a name="tuples-as-values-or-member-references"></a>Tuple 做為值或成員參考  
 您可以在查詢中使用 Tuple，來傳回 Tuple 所參考之資料格的值，如上述範例所示。 或者，您也可以在運算式中使用 Tuple，明確參考 Tuple 中指定的成員。 查詢或運算式可以利用會傳回或取用 Tuple 的函數。 Tuple 可以用來參考 Tuple 所指定之資料格的值，或在函數中使用時用來指定成員組合。  
  
### <a name="tuple-dimensionality"></a>Tuple 維度性  
 Tuple 的 *「維度性」* 是指 Tuple 中的成員順序。 因為隱含成員一律以相同順序出現，所以就 Tuple 的明確定義成員方面最常考慮到維度性。 當您定義一組 Tuple 時，Tuple 的成員順序很重要。 下列範例包含資料行軸上 Tuple 的兩個成員。  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  當您從一個以上的維度明確指定 Tuple 的成員時，必須用括號含括整個 Tuple。 只指定 Tuple 中的單一成員時，括號是選擇性的。  
  
 在上述範例中，查詢中的 Tuple 指定傳回位於 Measures 維度之 Reseller Sales Amount 和 Date 維度中 Calendar Year 屬性階層之 CY 2004 成員交集處的 Cube 資料格。  
  
> [!NOTE]  
>  屬性成員可以其成員名稱或成員索引鍵代表。 在上述範例中，您可以將參考值從 [CY 2004] 取代成 &[2004]。  
  
## <a name="see-also"></a>另請參閱  
 [重要的概念在 MDX 中的&#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [Cube 空間](cube-space.md)   
 [「 自動存在 」](autoexists.md)   
 [使用成員、 Tuple 及集合 &#40;MDX &#41;](working-with-members-tuples-and-sets-mdx.md)  
  
  
