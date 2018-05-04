---
title: SET 確實指令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d40e662bf6af67246e3d5ae8eecd491cb2d263a5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-exact-command"></a>SET 確切命令
指定的規則來比較兩個不同長度的字串。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 指定的運算式必須符合將對等字元的字元。 比較會忽略任何運算式中的尾端空白。 進行比較，較短的兩個運算式會填補右側以空白以符合較長的運算式的長度。  
  
 OFF  
 （預設值）。指定，為相等，運算式必須符合字元的字元運算式右邊的結尾為止。  
  
## <a name="remarks"></a>備註  
 如果這兩個字串相同的長度，設定實際的設定沒有任何作用。  
  
## <a name="string-comparisons"></a>字串比較  
 Visual FoxPro 有兩個關聯式運算子，以測試相等。  
  
 = 運算子會執行相同類型的兩個值之間的比較。 這個運算子適用於比較的字元、 數字、 日期和邏輯資料。  
  
 不過，當您比較使用的字元運算式 = 運算子的結果可能不會完全不如預期。 字元運算式的比較字元的右方，直到其中一個運算式的右側運算式的結尾不等於另一個，從左字元 = 運算子為止 （設定完全關閉），或直到兩個運算式結尾已達到 (確切設定 ON)。  
  
 = = 需要進行精確比較的字元資料時，就可以使用運算子。 如果兩個字元運算式進行比較與 = = 運算子的兩邊的運算式 = = 運算子必須包含完全相同的字元，包括空白時，才會被視為相等。 完全設定的設定會被忽略，當字元字串比較時使用 = =。  
  
 下表顯示運算子的選擇，並設定設定值如何影響比較。 （底線代表空格）。  
  
|比較|= 完全關閉|= 確切上|= = 確切的 ON 或 OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc"="abc"|比對|比對|比對|  
|"ab"="abc"|沒有相符項目|沒有相符項目|沒有相符項目|  
|"abc"="ab"|比對|沒有相符項目|沒有相符項目|  
|"abc"="ab_"|沒有相符項目|沒有相符項目|沒有相符項目|  
|"ab"="ab_"|沒有相符項目|比對|沒有相符項目|  
|「 ab_"="ab"|比對|比對|沒有相符項目|  
|""="ab"|沒有相符項目|沒有相符項目|沒有相符項目|  
|"ab"=""|比對|沒有相符項目|沒有相符項目|  
|"__" = ""|比對|比對|沒有相符項目|  
|"" = "___"|沒有相符項目|比對|沒有相符項目|  
|TRIM("___") =""|比對|比對|比對|  
|""= TRIM("___")|比對|比對|比對|  
  
## <a name="see-also"></a>另請參閱  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
