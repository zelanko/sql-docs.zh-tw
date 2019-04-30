---
title: LinkMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71235953f592572bd7ac0dcb2493d97dd509f8b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269940"
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)


  傳回相當於指定階層架構中的指定成員的成員  
  
## <a name="syntax"></a>語法  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Member_Expression*  
 傳回成員的有效多維度運算式 (MDX) 運算式。  
  
 *Hierarchy_Expression*  
 傳回階層的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **LinkMember**函式會傳回從指定比對索引鍵的值，指定的成員相關的階層中的每個層級的階層。 每個層級的屬性必須有相同的索引鍵基數和資料類型。 在非自然階層中，如果有多個項目符合屬性的索引鍵值，結果會是錯誤或未定。  
  
## <a name="examples"></a>範例  
 下列範例會使用**LinkMember** Calendar 階層 Date.Date 屬性階層 July 1，2002年成員的上階 Adventure Works cube 中傳回的預設量值的函式。  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [上階&#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [MDX 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
