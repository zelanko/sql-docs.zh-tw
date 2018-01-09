---
title: "函式 （MDX 語法） |Microsoft 文件"
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
dev_langs: kbMDX
helpviewer_keywords:
- MDX [Analysis Services], functions
- Multidimensional Expressions [Analysis Services], functions
- functions [MDX]
ms.assetid: 74ca5e79-1f33-4795-9d68-98eff9c190c1
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 00259604fe891a21f6f52835b1844762a751f09a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="functions-mdx-syntax"></a>函數 (MDX 語法)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  多維度運算式 (MDX) 有數個內建函數類別，以執行特定作業。 下表列出 MDX 中可用的函數類別。  
  
> [!NOTE]  
>  如需個別函數的詳細資訊，請參閱[MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md).  
  
|函數類別|描述|  
|-----------------------|-----------------|  
|陣列函數|提供可在預存程序中使用的陣列。<br /><br /> 如需詳細資訊，請參閱[使用預存程序 &#40;MDX &#41;](../mdx/using-stored-procedures-mdx.md).|  
|維度函數|傳回階層、層級或成員維度的參考。<br /><br /> 如需詳細資訊，請參閱[使用維度、 階層和層級函數](../mdx/using-dimension-hierarchy-and-level-functions.md)。|  
|階層函數|傳回層級或成員階層的參考。<br /><br /> 如需詳細資訊，請參閱[使用維度、 階層和層級函數](../mdx/using-dimension-hierarchy-and-level-functions.md)。|  
|層級函數|傳回成員、維度、階層層級的參考，或字串運算式的參考。<br /><br /> 如需詳細資訊，請參閱[使用維度、 階層和層級函數](../mdx/using-dimension-hierarchy-and-level-functions.md)。|  
|邏輯函數|執行邏輯作業和比較物件及運算式。<br /><br /> 如需詳細資訊，請參閱[使用邏輯函數](../mdx/using-logical-functions.md)。|  
|成員函數|傳回其他物件成員的參考，或字串運算式的參考。<br /><br /> 如需詳細資訊，請參閱[使用成員函式](../mdx/using-member-functions.md)。|  
|數值函數|執行物件及運算式上的數學及統計函數。<br /><br /> 如需詳細資訊，請參閱[使用數學函數](../mdx/using-mathematical-functions.md)。|  
|集合函數|傳回其他物件集合的參考，或字串運算式的參考。<br /><br /> 如需詳細資訊，請參閱[使用 Set 函式](../mdx/using-set-functions.md)。|  
|字串函數|傳回其他物件或伺服器的字串值。<br /><br /> 如需詳細資訊，請參閱[使用字串函數](../mdx/using-string-functions.md)。|  
|Tuple 函數|傳回集合 Tuple 的參考，或字串運算式的參考。<br /><br /> 如需詳細資訊，請參閱＜使用 Tuple 函數＞。|  
  
## <a name="uses-of-functions"></a>函數的使用  
 任何 MDX 運算式中都可以使用或包括函數： 函數也可以為巢狀 (將一函數置於另一個函數中)。  
  
## <a name="see-also"></a>請參閱  
 [MDX 語法元素 &#40;MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
