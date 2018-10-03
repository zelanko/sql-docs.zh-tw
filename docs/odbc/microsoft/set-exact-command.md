---
title: SET EXACT 命令 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 16651df836ac3fb87c5e28b4b8fa25088e9dd86a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606797"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定的規則來比較兩個字串的長度不同。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 指定運算式必須符合為相等的字元的字元。 比較會忽略任何運算式中的尾端空白。 如需比較，較短的兩個運算式會填補右側以空白比對較長的運算式的長度。  
  
 OFF  
 （預設值）。指定，為相等，運算式必須符合字元的字元運算式右邊的結尾為止。  
  
## <a name="remarks"></a>備註  
 如果這兩個字串都有相同的長度，完全設定的設定會有任何作用。  
  
## <a name="string-comparisons"></a>字串比較  
 Visual FoxPro 有兩個關聯式運算子，測試相等。  
  
 = 運算子會執行相同類型的兩個值之間的比較。 此運算子適用於比較的字元、 數字、 日期和邏輯的資料。  
  
 不過，當您比較使用的字元運算式 = 運算子，結果可能不會完全不如預期。 字元運算式的比較字元的字元右方，直到其中一個運算式的右側運算式的結尾之前不等於另一個，從左 = 運算子為止 （設定完全關閉），或直到兩個運算式結尾已達 (確切設定 ON)。  
  
 = = 運算子用於需要精確比較的字元資料時。 如果兩個字元運算式會比較使用 = = 運算子，兩邊的運算式 = = 運算子必須包含完全相同的字元，包括空格時，才會被視為相等。 完全設定的設定會被忽略，當比較字元字串時使用 = =。  
  
 下表顯示選擇的運算子和完全設定的設定如何影響比較。 （底線字元代表一個空格）。  
  
|比較|= 完全關閉|= 確切上|= = 確切的 ON 或 OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc"="abc"|相符項目|相符項目|相符項目|  
|"ab"="abc"|沒有相符項目|沒有相符項目|沒有相符項目|  
|"abc"="ab"|相符項目|沒有相符項目|沒有相符項目|  
|"abc"="ab_ 」|沒有相符項目|沒有相符項目|沒有相符項目|  
|"ab"="ab_ 」|沒有相符項目|相符項目|沒有相符項目|  
|「 ab_"="ab"|相符項目|相符項目|沒有相符項目|  
|「"="ab"|沒有相符項目|沒有相符項目|沒有相符項目|  
|"ab"=""|相符項目|沒有相符項目|沒有相符項目|  
|"__" = ""|相符項目|相符項目|沒有相符項目|  
|"" = "___"|沒有相符項目|相符項目|沒有相符項目|  
|TRIM("___") =""|相符項目|相符項目|相符項目|  
|「"= TRIM("___")|相符項目|相符項目|相符項目|  
  
## <a name="see-also"></a>另請參閱  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
