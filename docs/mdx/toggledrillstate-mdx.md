---
title: ToggleDrillState (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58acac77e4826855997791476b0602699452b7b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228086"
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
  
 *遞迴*  
 (選擇性)。 表示遞迴比較集合的關鍵字。 **ToggleDrillState**函式是組成**DrillupMember**並**DrilldownMember**函式。 中的成員時，僅適用於遞迴**DrilldownMember**狀態。  
  
 *Include_calc_members*  
 (選擇性)。 旗標，指出在向下鑽研層級中若有導出成員存在，是否要包含它們。  
  
## <a name="remarks"></a>備註  
 **ToggleDrillState**函式切換向下鑽研的狀態會出現在第一個集合的第二個集合的每個成員。 第一個集合可以包含具有任何維度的 Tuple，但第二個集合只能包含單一維度的成員。 **ToggleDrillState**函式是組成**DrillupMember**並**DrilldownMember**函式。 如果成員*m*、 第二個集合出現在第一個集合，並為該成員向下鑽研 （亦即，具有緊接著下階），然後`DrillupMember(Set_Expression1, {m})`套用至的成員或 tuple 中第一個集合。 如果該*m*成員處於向上 (也就是沒有任何子系*m*緊接著*m*)，`DrilldownMember(Set_Expression1, {m}[, RECURSIVE])`會套用到第一個集合。  
  
 如果選擇性**遞迴**旗標，則向上鑽研和向下的鑽研會遞迴套用。 如需有關遞迴旗標的詳細資訊，請參閱 < [DrillupMember](../mdx/drillupmember-mdx.md)並[DrilldownMember](../mdx/drilldownmember-mdx.md)函式。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器提供鑽研函數; 支援的層級請參閱[支援的 XMLA 屬性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)如需詳細資訊。  
  
 請參閱[資料庫日誌：MDX 設定函數：Toggledrillstate （） 函數](https://go.microsoft.com/fwlink/?LinkId=517759)案例和涉及此函式的範例。  
  
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
  
  
