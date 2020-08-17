---
description: 程式註解 (MDX 語法)
title: " (MDX 語法) 的批註 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8fa1312e361bf0ef673254c0eb804ed7b8b7ca7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387671"
---
# <a name="comments-mdx-syntax"></a>程式註解 (MDX 語法)


  註解是程式碼中不會執行的文字字串。 (註解也稱為備註)。 您可以使用註解來說明程式碼，或是把要診斷的部份多維度運算式 (MDX) 陳述式及指令碼暫時停用。 使用註解來說明程式碼，可使未來的程式碼維護工作更加容易。 您可以經常使用註解記錄程式名稱、作者姓名，以及主要程式碼變更的日期。 您也可以使用註解描述複雜的計算或說明撰寫程式的方法。  
  
 MDX 中的註解要遵循下列指導方針：  
  
-   您可以在註解中使用所有英數字元或符號。  批註內的所有字元都會被忽略。  
  
-   陳述式或指令碼中的註解並無長度上限。 一個註解可以由一或多行組成。  
  
 MDX 支援兩種註解字元類型：  
  
 // (雙斜線)  
 這些註解字元可以跟程式碼放在同一行來執行，或是將註解本身全部放在一行。 從雙斜線到該行結尾之間，全部都是註解的一部份。 對於多行註解而言，雙斜線必須出現在每一行註解的開頭。 如需詳細資訊，請參閱 [&#40;批註&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)。  
  
 -- (雙連字號)  
 這些註解字元可以跟程式碼放在同一行來執行，或是將註解本身全部放在一行。 從雙連字號到該行結尾之間，全部都是註解的一部份。 對於多行註解而言，雙連字號必須出現在每一行註解的開頭。 如需詳細資訊，請參閱 [--&#40;批註&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)。  
  
 /* ... \*/ (斜線-星號字元配對)   
 這些註解字元可以跟程式碼放在同一行來執行、也可以將註解本身全部放在一行，或甚至放在可執行的程式碼中。 開啟批註組 (/)  () 的所有專案都會被 \* \* 視為批註的一部分。 若為多行批註， (/) 的開啟批註字元組 \* 必須開始批註，且關閉批註字元組 (\* /) 必須結束批註。 任一行註解中不能出現其他任何註解字元。 如需詳細資訊，請參閱 [/* ... \*/ (批註) ](../mdx/comment-mdx.md)。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [MDX 語法元素 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
