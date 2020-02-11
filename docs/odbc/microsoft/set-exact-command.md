---
title: 設定 EXACT 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 686ecc89f44bac4b219b760e55160f451a15c503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997723"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定比較不同長度之兩個字串的規則。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 指定運算式必須比對字元的字元，使其相等。 比較會忽略運算式中的尾端空白。 為了進行比較，這兩個運算式中較短的會以空白填補，以符合較長運算式的長度。  
  
 OFF  
 （預設值）。指定對等的運算式必須符合字元，才會到達右邊運算式的結尾。  
  
## <a name="remarks"></a>備註  
 如果兩個字串的長度相同，則 [設定精確] 設定不會有任何作用。  
  
## <a name="string-comparisons"></a>字串比較  
 Visual FoxPro 有兩個會測試是否相等的關係運算子。  
  
 = 運算子會執行相同類型的兩個值之間的比較。 這個運算子適合用來比較字元、數位、日期和邏輯資料。  
  
 不過，當您比較字元運算式與 = 運算子時，結果可能不完全符合您的預期。 字元運算式會從左至右的字元進行比較，直到其中一個運算式不等於另一個運算式為止，直到到達 = 運算子右邊運算式的結尾為止（設定為 OFF），或直到兩個運算式的結尾都是已達到（設定為 EXACT）。  
  
 當需要精確的字元資料比較時，可以使用 = = 運算子。 如果兩個字元運算式與 = = 運算子比較，= = 運算子兩邊的運算式必須包含完全相同的字元（包括空白），才會被視為相等。 使用 = = 比較字元字串時，會忽略 SET EXACT 設定。  
  
 下表顯示運算子的選擇和設定的確切設定會如何影響比較。 （底線代表空格）。  
  
|比較|= 完全關閉|= 精確于|= = 完全開啟或關閉|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|Match|Match|Match|  
|"ab" = "abc"|沒有相符的|沒有相符的|沒有相符的|  
|"abc" = "ab"|Match|沒有相符的|沒有相符的|  
|"abc" = "ab_"|沒有相符的|沒有相符的|沒有相符的|  
|"ab" = "ab_"|沒有相符的|Match|沒有相符的|  
|"ab_" = "ab"|Match|Match|沒有相符的|  
|"" = "ab"|沒有相符的|沒有相符的|沒有相符的|  
|"ab" = ""|Match|沒有相符的|沒有相符的|  
|"__" = ""|Match|Match|沒有相符的|  
|"" = "___"|沒有相符的|Match|沒有相符的|  
|TRIM （"___"） = ""|Match|Match|Match|  
|"" = TRIM （"___"）|Match|Match|Match|  
  
## <a name="see-also"></a>另請參閱  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
