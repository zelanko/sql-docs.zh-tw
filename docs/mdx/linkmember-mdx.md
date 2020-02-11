---
title: LinkMember （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a00388e067878d9c2165cbae6844f8020b7c63e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905607"
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
 **LinkMember**函數會傳回指定之階層中的成員，該階層符合相關階層中指定成員之每個層級的索引鍵值。 每個層級的屬性必須有相同的索引鍵基數和資料類型。 在非自然階層中，如果有多個項目符合屬性的索引鍵值，結果會是錯誤或未定。  
  
## <a name="examples"></a>範例  
 下列範例會使用**LinkMember**函式，針對行事曆階層中 Date. date 屬性階層之2002成員的父項，傳回「艾德作品」 cube 中的預設量值。  
  
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
 [父 &#40;MDX&#41;](../mdx/ascendants-mdx.md)   
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
