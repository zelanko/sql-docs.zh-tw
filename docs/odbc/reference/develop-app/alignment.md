---
title: 對齊 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205cc3ff95dd60db215150f46ae894fbb99bd9ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288603"
---
# <a name="alignment"></a>Alignment
ODBC 應用程式中的對齊問題通常與任何其他應用程式中的對齊問題沒有什麼不同。 也就是說,大多數 ODBC 應用程式在對齊方面幾乎沒有問題或沒有問題。 不對齊位址的處罰與硬體和操作系統不同,可能很小,如輕微的性能損失或主要作為致命的運行時錯誤。 因此,ODBC 應用程式,特別是便攜式ODBC應用程式,應小心正確對齊數據。  
  
 當 ODBC 應用程式遇到對齊問題時,一個例子是,當它們分配一大塊記憶體並將該記憶體的不同部分綁定到結果集中的列時。 當泛型應用程式必須在運行時確定結果集的形狀並相應地分配和綁定記憶體時,最有可能發生這種情況。  
  
 例如,假設應用程式執行使用者輸入的**SELECT**語句並從該語句中獲取結果。 由於編寫程式時不知道此結果集的形狀,因此應用程式必須在創建結果集后確定每列的類型並相應地綁定記憶體。 最簡單的方法是分配一個大記憶體塊,並將該塊中的不同位址綁定到每列。 要造訪列中的數據,應用程式將強制轉換綁定到該列的記憶體。  
  
 下圖顯示了示例結果集,以及如何使用每個 SQL 數據類型的預設 C 數據類型將其綁定到它。 每個"X"表示記憶體的單個字節。 (此示例僅顯示綁定到列的數據緩衝區。 這樣做是為了簡單起見。 在實際代碼中,長度/指示器緩衝區也必須對齊。  
  
 ![以預設的 C 資料型別繫結到 SQL 資料型別](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假設繫結位址儲存在*Address*陣列中,則應用程式使用以下表示式存取連結到每欄位的記憶體:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 請注意,綁定到第二列和第三列的位址以奇數位節開頭,並且綁定到第三列的位址不能被四個整除,即 SDWORD 的大小。 在某些計算機上,這不是問題;因此,這將成為問題。對他人,將造成輕微的績效處罰;在其他人上,它會導致致命的運行時錯誤。 更好的解決方案是對齊其自然對齊邊界上的每個綁定位址。 假設 UCHAR 為 1,SWORD 為 2,SDWORD 為 4,則給出下圖所示的結果,其中"X"表示使用的記憶體位元組,"O"表示未使用的記憶體位元組。  
  
 ![以自然對齊的界限繫結](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 雖然此解決方案不使用應用程式的所有記憶體,但它不會遇到任何對齊問題。 遺憾的是,實現此解決方案需要大量代碼,因為每列必須根據其類型單獨對齊。 更簡單的解決方案是對齊最大對齊邊界大小上的所有列,如下圖所示示例中為 4。  
  
 ![以最大的對齊界限繫結](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 儘管此解決方案留下了較大的漏洞,但實現它的代碼相對簡單且快速。 在大多數情況下,這抵消了在未使用的記憶體中支付的罰款。 有關使用此方法的範例,請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。
