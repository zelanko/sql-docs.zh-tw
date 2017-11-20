---
title: "對齊 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 412c04f8181997738bac1fc7b457c9ec0c3efcde
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="alignment"></a>Alignment
ODBC 應用程式中的對齊問題通常與並無不同它們位於其他任何應用程式。 也就是說，大部分的 ODBC 應用程式有少數或沒有對齊問題。 未將對齊位址罰款因為硬體和作業系統而不同，而且可能效能稍微降低做為次要或成嚴重執行階段錯誤。 因此，ODBC 應用程式和可攜式的 ODBC 應用程式特別的是，應該小心正確對齊的資料。  
  
 一個範例說明當 ODBC 應用程式遇到對齊問題，當它們配置大量的記憶體區塊，並將該記憶體的不同部分繫結結果集中的資料行。 這是最有可能發生泛型應用程式必須在執行階段決定結果集的形狀和配置，並據此繫結記憶體。  
  
 例如，假設應用程式執行**選取**使用者輸入陳述式，並從這個陳述式擷取結果。 因為此結果集的形狀不為已知程式會寫入時，應用程式必須判斷每個資料行的類型，建立結果集之後，並據此繫結的記憶體。 若要這樣做最簡單的方式是記憶體的配置大量區塊和每個資料行繫結不同的位址在該區段。 若要存取資料行中的，應用程式會轉換為繫結至該資料行的記憶體。  
  
 下圖顯示範例結果集和如何的記憶體區塊可能會將繫結到每個 SQL 資料類型使用預設 C 資料類型。 每個"X"代表單一位元組的記憶體。 （這個範例示範只會繫結至資料行的資料緩衝區。 這是為了簡單起見。 在實際的程式碼的長度/指標緩衝區必須也對齊。）  
  
 ![繫結 SQL 資料類型的預設 C 資料類型所](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假設的繫結的位址會儲存在*位址*陣列，應用程式使用下列運算式來存取繫結至每個資料行的記憶體：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 請注意，位址繫結至第二個和第三個資料行開始奇數位元組的位址繫結到第三個資料行不是由四個，也就是 SDWORD 大小整除。 在某些電腦，這並不會發生問題;另一方面，它會導致效能稍微降低。仍有部份，它會導致嚴重的執行階段錯誤。 更好的解決方案就是對齊其自然對齊的界限上每個繫結的位址。 假設這是第 1 UCHAR 2 劍，以及 4 個 SDWORD，這會讓結果顯示在下圖中，其中"X"代表使用記憶體的位元組，而"O"代表的是未使用的記憶體位元組。  
  
 ![以自然對齊界限繫結](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 雖然這個解決方案不使用的所有應用程式的記憶體，它不會碰到對齊的任何問題。 不幸的是，它會牽涉到大量的程式碼來實作此解決方案中，為每個資料行必須個別對齊根據其類型。 比較簡單的解決方案是為所有的資料行大小的最大的對齊界限 4 在下圖中顯示的範例。  
  
 ![繫結的最大的對齊界限](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 雖然這個解決方案可讓更大的漏洞，來實作它的程式碼是相對較簡單且快速。 在大部分情況下，此位移付費未使用記憶體中的負面影響。 如需使用這個方法的範例，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。

