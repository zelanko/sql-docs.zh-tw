---
title: "TupleToStr (MDX) |Microsoft 文件"
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
- TUPLETOSTR
dev_langs:
- kbMDX
helpviewer_keywords:
- TupletoStr function
ms.assetid: ad12347c-d1c4-4d8b-a910-3116bd6b68e0
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2da77853e8cd048a274f00a0deffe24d29a01346
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="tupletostr-mdx"></a>TupleToStr (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回多維度運算式 (MDX)–對應至指定 Tuple 的格式化字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
TupleToStr(Tuple_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Tuple_Expression*  
 傳回 Tuple 的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 這個函數是用來將 Tuple 的字串表示傳送至外部函數，以進行剖析。 所傳回的字串以大括號 {} 括住，如果在 Tuple 中明確定義一個以上的成員，則會以逗號分隔每個成員。  
  
## <a name="examples"></a>範例  
 下列範例會傳回字串 ([Date].[Calendar Year].&[2001],[Geography].[Geography].[Country].&[United States])：  
  
```  
WITH MEMBER Measures.x AS TupleToStr   
   (   
      ([Date].[Calendar Year].&[2001]  
         , [Geography].[Geography].[Country].&[United States]  
      )  
   )     
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 下列範例會傳回和上一個範例相同的字串。  
  
```  
WITH SET s AS   
   {  
      ([Date].[Calendar Year].&[2001],  
         [Geography].[Geography].[Country].&[United States]  
      )   
   }  
MEMBER Measures.x AS TupleToStr ( s.Item(0) )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

