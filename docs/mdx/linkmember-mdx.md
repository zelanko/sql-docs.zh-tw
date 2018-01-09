---
title: "LinkMember (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LINKMEMBER
dev_langs: kbMDX
helpviewer_keywords: LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 39de8bf43f01354e06a24305c650b52852687f4c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 **LinkMember**函式會傳回符合指定的成員相關的階層中的每個層級的索引鍵值指定階層的成員。 每個層級的屬性必須有相同的索引鍵基數和資料類型。 在非自然階層中，如果有多個項目符合屬性的索引鍵值，結果會是錯誤或未定。  
  
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
  
## <a name="see-also"></a>請參閱  
 [Hierarchize &#40;MDX &#41;](../mdx/hierarchize-mdx.md)   
 [上階 &#40;MDX &#41;](../mdx/ascendants-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
