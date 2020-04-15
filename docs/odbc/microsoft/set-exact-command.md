---
title: 設定精確命令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300868"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定用於比較兩個不同長度的字串的規則。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 指定表示式必須匹配字元,字元為等效字元。 對於比較,將忽略表達式中的任何尾隨空格。 為了進行比較,兩個表達式的較短時間在右側用空格填充,以匹配較長表達式的長度。  
  
 OFF  
 (預設值。指定要等效的是,表達式必須匹配字元的字元,直到到達右側表達式的末尾。  
  
## <a name="remarks"></a>備註  
 如果兩個字串的長度相同,則 SET EXACT 設置不起作用。  
  
## <a name="string-comparisons"></a>字串比較  
 Visual FoxPro 有兩個關係運算符,用於測試相等性。  
  
 _ 運算元對相同類型的兩個值執行比較。 此運算元適用於比較字元、數位、日期和邏輯數據。  
  
 但是,當您將字元表達式與 + 運算元進行比較時,結果可能不完全是您期望的結果。 字元表示式從左到右比較字元的字元,直到其中一個運算式不等於另一個運算式,直到到達 _ 運算元右側的運算式末尾(SET EXACT OFF),或直到達到兩個表達式的末尾(SET EXACT ON)。  
  
 當需要精確比較字元資料時,可以使用 * 運算元。 如果將兩個字元表達式與 * 運算元進行比較,則 _ 運算元兩側的運算式必須包含完全相同的字元(包括空白)才能被視為相等。 使用 *比較字串時,將忽略 SET EXACT 設定。  
  
 下表顯示了運算符的選擇和 SET EXACT 設定如何影響比較。 (下劃線表示空白。  
  
|比較|• 完全關閉|• 精確開啟|• 精確開啟或關閉|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|相符項目|相符項目|相符項目|  
|"ab" = "abc"|沒有符合的結果|沒有符合的結果|沒有符合的結果|  
|"abc" = "ab"|相符項目|沒有符合的結果|沒有符合的結果|  
|"abc" = "ab_"|沒有符合的結果|沒有符合的結果|沒有符合的結果|  
|"ab" = "ab_"|沒有符合的結果|相符項目|沒有符合的結果|  
|"ab_" = "ab"|相符項目|相符項目|沒有符合的結果|  
|"" = "ab"|沒有符合的結果|沒有符合的結果|沒有符合的結果|  
|"ab" = ""|相符項目|沒有符合的結果|沒有符合的結果|  
|"__" = ""|相符項目|相符項目|沒有符合的結果|  
|"" = "___"|沒有符合的結果|相符項目|沒有符合的結果|  
|修剪("*") = ""|相符項目|相符項目|相符項目|  
|"" = 修剪("*"|相符項目|相符項目|相符項目|  
  
## <a name="see-also"></a>另請參閱  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
