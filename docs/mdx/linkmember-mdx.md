---
title: "LinkMember (MDX) |Microsoft 文件"
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
- LINKMEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c87723c4d7db370b46b2e41cf2d67064f1978f91
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="linkmember-mdx"></a>LinkMember (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="see-also"></a>另請參閱  
 [Hierarchize &#40;MDX &#41;](../mdx/hierarchize-mdx.md)   
 [上階 &#40;MDX &#41;](../mdx/ascendants-mdx.md)   
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

