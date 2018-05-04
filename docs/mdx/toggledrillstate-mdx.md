---
title: ToggleDrillState (MDX) |Microsoft 文件
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
- TOGGLEDRILLSTATE
dev_langs:
- kbMDX
helpviewer_keywords:
- ToggleDrillState function
ms.assetid: 26fa1a0d-3ed1-45dc-955d-0591d49e4db9
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 63b5fb01cac2fe886bce15ded807b8e655d98056
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 *遞迴*  
 (選擇性)。 表示遞迴比較集合的關鍵字。 **ToggleDrillState**函式是組合**DrillupMember**和**DrilldownMember**函式。 中的成員時，只適用於遞迴**DrilldownMember**狀態。  
  
 *Include_calc_members*  
 (選擇性)。 旗標，指出在向下鑽研層級中若有導出成員存在，是否要包含它們。  
  
## <a name="remarks"></a>備註  
 **ToggleDrillState**函式切換的第二個集合並且出現第一個集合中每個成員的鑽研狀態。 第一個集合可以包含具有任何維度的 Tuple，但第二個集合只能包含單一維度的成員。 **ToggleDrillState**函式是組合**DrillupMember**和**DrilldownMember**函式。 如果成員*m*、 第二個集合中第一個集合，且該成員向下鑽研 （亦即，具有緊接著下階），然後`DrillupMember(Set_Expression1, {m})`套用至成員或 tuple 中第一個集合。 如果該*m*成員處於向上 (也就是沒有任何子代的*m*緊接著*m*)，`DrilldownMember(Set_Expression1, {m}[, RECURSIVE])`會套用到第一個集合。  
  
 如果選擇性**遞迴**旗標，則向上鑽研和向下的鑽研會遞迴地套用。 如需有關遞迴旗標的詳細資訊，請參閱[DrillupMember](../mdx/drillupmember-mdx.md)和[DrilldownMember](../mdx/drilldownmember-mdx.md)函式。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器為鑽研函數; 提供的支援層級請參閱[支援 XMLA 屬性&#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)如需詳細資訊。  
  
 請參閱[資料庫日誌： MDX 設定函數： Toggledrillstate （） 函數](http://go.microsoft.com/fwlink/?LinkId=517759)案例和涉及此函式的範例。  
  
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
 [MDX 函數參考 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
