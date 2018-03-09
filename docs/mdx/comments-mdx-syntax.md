---
title: "註解 （MDX 語法） |Microsoft 文件"
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
- remarks [MDX]
- MDX [Analysis Services], comments
- commenting characters
- nonexecuting text strings [MDX]
- Multidimensional Expressions [Analysis Services], comments
- comments [MDX]
ms.assetid: 9c00b30c-28f6-4f23-b812-ccc0e900daa5
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9430eeb2613b77ce1f34918382cd57e4958ac512
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="comments-mdx-syntax"></a>程式註解 (MDX 語法)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  註解是程式碼中不會執行的文字字串。 (註解也稱為備註)。 您可以使用註解來說明程式碼，或是把要診斷的部份多維度運算式 (MDX) 陳述式及指令碼暫時停用。 使用註解來說明程式碼，可使未來的程式碼維護工作更加容易。 您可以經常使用註解記錄程式名稱、作者姓名，以及主要程式碼變更的日期。 您也可以使用註解描述複雜的計算或說明撰寫程式的方法。  
  
 MDX 中的註解要遵循下列指導方針：  
  
-   您可以在註解中使用所有英數字元或符號。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]會忽略註解內的所有字元。  
  
-   陳述式或指令碼中的註解並無長度上限。 一個註解可以由一或多行組成。  
  
 MDX 支援兩種註解字元類型：  
  
 // (雙斜線)  
 這些註解字元可以跟程式碼放在同一行來執行，或是將註解本身全部放在一行。 從雙斜線到該行結尾之間，全部都是註解的一部份。 對於多行註解而言，雙斜線必須出現在每一行註解的開頭。 如需詳細資訊，請參閱[&#40;註解 &#41;&#40;MDX &#41;](../mdx/comment-mdx-double-slash.md).  
  
 -- (雙連字號)  
 這些註解字元可以跟程式碼放在同一行來執行，或是將註解本身全部放在一行。 從雙連字號到該行結尾之間，全部都是註解的一部份。 對於多行註解而言，雙連字號必須出現在每一行註解的開頭。 如需詳細資訊，請參閱[-&#40;註解 &#41;&#40;MDX &#41;](../mdx/comment-mdx-operator-reference.md).  
  
 /* ...\*/ （正斜線-星號字元配對）  
 這些註解字元可以跟程式碼放在同一行來執行、也可以將註解本身全部放在一行，或甚至放在可執行的程式碼中。 所有內容都將開啟註解配對 (/\*) 到關閉註解配對 (\*/) 會被視為註解的一部分。 多行註解，開啟註解字元配對 (/\*) 必須開始註解和註解字元配對 (\*/) 必須結束註解。 任一行註解中不能出現其他任何註解字元。 如需詳細資訊，請參閱[/ *...\*/ (Comment)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>範例  
 下列查詢顯示註解的所有三種類型：  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>請參閱  
 [MDX 語法元素 &#40;MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
