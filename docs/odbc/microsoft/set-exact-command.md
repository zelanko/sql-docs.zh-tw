---
description: SET EXACT 命令
title: 設定確切的命令 |Microsoft Docs
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
ms.openlocfilehash: 6bae23ef0677061f92d0466564619e85d4ae1630
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466360"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定比較兩個不同長度之字串的規則。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 指定運算式必須比對字元，使字元相等。 比較會忽略運算式中的任何尾端空白。 為了進行比較，這兩個運算式中較短的空格會以空格填補，以符合較長的運算式長度。  
  
 OFF  
  (預設值。 ) 指定，除非到達右邊運算式的結尾，否則運算式必須符合字元的字元。  
  
## <a name="remarks"></a>備註  
 如果兩個字串的長度相同，則設定確切的設定不會有任何作用。  
  
## <a name="string-comparisons"></a>字串比較  
 Visual FoxPro 有兩個可測試是否相等的關係運算子。  
  
 = 運算子會執行相同類型的兩個值之間的比較。 這個運算子適用于比較字元、數位、日期和邏輯資料。  
  
 但是，當您比較字元運算式與 = 運算子時，結果可能不是您預期的結果。 字元運算式是從左至右的字元比較字元，直到其中一個運算式不等於另一個運算式為止，直到達到 = 運算子右邊的運算式結尾為止 (設定 [完全關閉]) ，或直到兩個運算式的兩端達到 (在) 上設定 [精確]。  
  
 當需要精確比較字元資料時，可以使用 = = 運算子。 如果兩個字元運算式與 = = 運算子比較，則 = = 運算子兩邊的運算式必須包含完全相同的字元，包括空白，以視為相等。 使用 = = 比較字元字串時，會忽略 SET 確切的設定。  
  
 下表顯示運算子的選擇和設定的確切設定如何影響比較。  (底線表示空格。 )   
  
|比較|= 完全關閉|= 完全開啟|= = 完全開啟或關閉|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|比對|比對|比對|  
|"ab" = "abc"|沒有符合的結果|沒有符合的結果|沒有符合的結果|  
|"abc" = "ab"|比對|沒有符合的結果|沒有符合的結果|  
|"abc" = "ab_"|沒有符合的結果|沒有符合的結果|沒有符合的結果|  
|"ab" = "ab_"|沒有符合的結果|比對|沒有符合的結果|  
|"ab_" = "ab"|比對|比對|沒有符合的結果|  
|"" = "ab"|沒有符合的結果|沒有符合的結果|沒有符合的結果|  
|"ab" = ""|比對|沒有符合的結果|沒有符合的結果|  
|"__" = ""|比對|比對|沒有符合的結果|  
|"" = "___"|沒有符合的結果|比對|沒有符合的結果|  
|TRIM ( "___" ) = ""|比對|比對|比對|  
|"" = TRIM ( "___" ) |比對|比對|比對|  
  
## <a name="see-also"></a>另請參閱  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
