---
title: 對齊 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288603"
---
# <a name="alignment"></a>Alignment
ODBC 應用程式中的對齊問題通常與其他任何應用程式中的不同。 也就是說，大部分的 ODBC 應用程式都沒有對齊的問題。 未對齊位址的懲罰會因硬體和作業系統而異，而且可能會因為輕微的效能影響或嚴重的執行階段錯誤而變小。 因此，ODBC 應用程式和可移植的 ODBC 應用程式尤其應該小心地對齊資料。  
  
 當 ODBC 應用程式遇到對齊問題的其中一個範例，就是當它們配置大型記憶體區塊，並將該記憶體的不同部分系結至結果集內的資料行時。 當泛型應用程式必須在執行時間判斷結果集的形狀，並據以配置和系結記憶體時，最可能發生這種情況。  
  
 例如，假設應用程式會執行使用者所輸入的**SELECT**語句，並從這個語句提取結果。 在撰寫程式時，因為此結果集的形狀不是已知的，所以應用程式必須在建立結果集之後，判斷每個資料行的類型，並據以系結記憶體。 若要這麼做，最簡單的方法是配置大型記憶體區塊，並將該區塊中的不同位址系結至每個資料行。 若要存取資料行中的資料，應用程式會將系結到該資料行的記憶體轉型。  
  
 下圖顯示範例結果集，以及如何使用每個 SQL 資料類型的預設 C 資料類型，將記憶體區塊系結至它。 每個 "X" 代表記憶體的單一位元組。 （此範例只會顯示系結至資料行的資料緩衝區。 這是為了簡單起見而完成。 在實際的程式碼中，長度/指標緩衝區也必須對齊）。  
  
 ![以預設的 C 資料型別繫結到 SQL 資料型別](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假設系結位址儲存在*位址*陣列中，應用程式會使用下列運算式來存取系結至每個資料行的記憶體：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 請注意，系結至第二個和第三個數據行的位址是以奇數位節開頭，而且系結至第三個數據行的位址無法被四個（也就是 SDWORD 的大小）整除。 在某些電腦上，這不會是問題;而在其他情況下，它會造成些許效能的負面影響;而在其他情況下，則會造成嚴重的執行階段錯誤。 較好的解決方案是將每個系結位址對齊其自然對齊界限。 假設這是 UCHAR 的1、寶劍的2和 SDWORD 的4，這會提供如下圖所示的結果，其中 "X" 代表所使用的記憶體位元組，而 "O" 代表未使用的記憶體位元組。  
  
 ![以自然對齊的界限繫結](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 雖然此解決方案不會使用所有應用程式的記憶體，但它不會遇到任何對齊問題。 可惜的是，它會採用相當多的程式碼來執行這個解決方案，因為每個資料行都必須根據其型別個別對齊。 較簡單的解決方法是將所有資料行對齊最大的對齊界限大小，在下圖所示的範例中為4。  
  
 ![以最大的對齊界限繫結](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 雖然此解決方案會留下較大的漏洞，但執行程式碼相當簡單且快速。 在大部分情況下，這會抵銷未使用記憶體中所支付的負面影響。 如需使用此方法的範例，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。
