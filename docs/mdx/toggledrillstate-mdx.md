---
title: ToggleDrillState （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8d027a76a82de3fd82b6c0c81c54ace08167039b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036607"
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
  
 *式*  
 (選擇性)。 表示遞迴比較集合的關鍵字。 **ToggleDrillState**函數是**DrillupMember**和**DrilldownMember**函數的組合。 只有在成員處於**DrilldownMember**狀態時，才會套用遞迴。  
  
 *Include_calc_members*  
 (選擇性)。 旗標，指出在向下鑽研層級中若有導出成員存在，是否要包含它們。  
  
## <a name="remarks"></a>備註  
 **ToggleDrillState**函數會切換第二個集合中每個成員的 [切入狀態]，這會出現在第一個集合中。 第一個集合可以包含具有任何維度的 Tuple，但第二個集合只能包含單一維度的成員。 **ToggleDrillState**函數是**DrillupMember**和**DrilldownMember**函數的組合。 如果第二個集合中的成員*m*是出現在第一個集合中，而且該成員向下切入（也就是緊接在它後面的子系）， `DrillupMember(Set_Expression1, {m})`則會套用至第一個集合中的成員或元組。 如果要對*m*成員進行鑽（也就是，沒有緊接在*m*後面的*m*的子系） `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` ，會套用至第一個集合。  
  
 如果使用選擇性**遞迴**旗標，向上切入和向下切入會以遞迴方式套用。 如需遞迴旗標的詳細資訊，請參閱[DrillupMember](../mdx/drillupmember-mdx.md)和[DrilldownMember](../mdx/drilldownmember-mdx.md)函數。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions 可讓您驗證服務器為鑽孔函數提供的支援層級;如需詳細資訊，請參閱[支援的 Xmla 屬性 &#40;xmla&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 。  
  
 如需有關此函式的案例和範例，請參閱[資料庫日誌： MDX 集合函式： ToggleDrillState （）函數](https://go.microsoft.com/fwlink/?LinkId=517759)。  
  
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
  
  
