---
description: ToggleDrillState (MDX)
title: ToggleDrillState (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e10c62742e28b69545efac51f70bf9628b43e08d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412899"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


  切換成員的鑽研模式 (向下鑽研及向上鑽研模式)。  
  
## <a name="syntax"></a>語法  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression1*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Set_Expression2*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *遞 歸*  
 (選擇性)。 表示遞迴比較集合的關鍵字。 **ToggleDrillState**函數是**DrillupMember**和**DrilldownMember**函數的組合。 只有當成員處於 **DrilldownMember** 狀態時，才會套用遞迴。  
  
 *Include_calc_members*  
 (選擇性)。 旗標，指出在向下鑽研層級中若有導出成員存在，是否要包含它們。  
  
## <a name="remarks"></a>備註  
 **ToggleDrillState**函式會切換第二個集合中出現在第一個集合中每個成員的切入狀態。 第一個集合可以包含具有任何維度的 Tuple，但第二個集合只能包含單一維度的成員。 **ToggleDrillState**函數是**DrillupMember**和**DrilldownMember**函數的組合。 如果第二個集合的成員 *m*是出現在第一個集合中，而且該成員 (也就是，在它) 之後緊接著有子系，則會套用 `DrillupMember(Set_Expression1, {m})` 至第一個集合中的成員或元組。 如果該*m*成員正在進行 (也就是，沒有任何緊接在 m *) 的子*系*m* ，會套用 `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` 至第一個集合。  
  
 如果使用選擇性 **遞迴** 旗標，則會以遞迴方式套用向上切入和向下切入。 如需遞迴旗標的詳細資訊，請參閱 [DrillupMember](../mdx/drillupmember-mdx.md) 和 [DrilldownMember](../mdx/drilldownmember-mdx.md) 函數。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您驗證服務器為切入函數提供的支援層級;如需詳細資訊，請參閱 [&#40;xmla&#41;支援的 Xmla 屬性 ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
 請參閱 [資料庫日誌： MDX Set Function： ToggleDrillState ( # A1](https://go.microsoft.com/fwlink/?LinkId=517759) 函式，以瞭解包含此函式的案例和範例。  
  
## <a name="example"></a>範例  
 下列範例會在第一個集合的 Australia 成員向下鑽研，並且在第一個集合的 United States 成員向上鑽研。  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
