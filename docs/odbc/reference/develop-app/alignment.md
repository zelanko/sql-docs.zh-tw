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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8b5a107f5ed8cd1c6c45317e60cc515a2601316
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077273"
---
# <a name="alignment"></a>對齊
在 ODBC 應用程式中的對齊問題通常與並無不同它們位於其他任何應用程式。 也就是大部分的 ODBC 應用程式有少數或沒有對齊問題。 未對齊位址處分會隨著硬體和作業系統而有所不同，而且可能會為次要效能稍微降低為或，主要為嚴重的執行階段錯誤。 因此，ODBC 應用程式和可攜式的 ODBC 應用程式特別的是，應該要特別小心適當對齊的資料。  
  
 一個範例中的 ODBC 應用程式何時發生對齊問題是配置大區塊的記憶體及記憶體的不同的組件繫結至結果集的資料行時。 這是最有可能發生時的一般應用程式必須在執行階段判斷結果集的形狀和配置，並據以繫結的記憶體。  
  
 例如，假設應用程式執行**選取**使用者輸入陳述式，並從這個陳述式中擷取結果。 當寫入程式，不知道此結果集的形狀，因為應用程式必須判斷每個資料行的類型，建立結果集之後，並據以繫結的記憶體。 若要這樣做最簡單的方式，就是記憶體的配置大量區塊，並將該區塊中的不同的位址繫結至每個資料行。 若要存取的資料行中的資料，應用程式會轉換繫結至該資料行的記憶體。  
  
 下圖顯示範例結果，設定及如何的記憶體區塊可能會繫結至每個 SQL 資料類型使用預設 C 資料類型。 每個"X"代表單一位元組的記憶體。 （此範例會示範只會繫結至資料行的資料緩衝區。 這是為了簡單起見。 在實際的程式碼中的長度/指標緩衝區必須也對齊。）  
  
 ![繫結 SQL 資料類型的預設 C 資料類型所](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 假設繫結的地址會儲存在*地址*陣列中，應用程式使用下列運算式來存取繫結至每個資料行的記憶體：  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 請注意，位址繫結至第二個和第三個資料行開始奇數位元組上而位址繫結到第三個資料行不是可由四個，也就是 SDWORD 的大小。 在某些電腦，這並不會發生問題;其他人，它會導致效能稍微降低;仍有部份，它會導致嚴重的執行階段錯誤。 更好的解決方案是將每個繫結的位址，其自然對齊界限上對齊。 假設這 1 UCHAR，2 代表拉鋸，以及 4 個 SDWORD，這會讓下圖中，其中"X"代表記憶體位元組之用，而"O"代表未使用的記憶體位元組之 所示的結果。  
  
 ![以自然對齊界限繫結](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 雖然這個解決方案不使用的所有應用程式的記憶體，它不會碰到任何對齊問題。 不幸的是，需要相當多的程式碼來實作此解決方案中，為每個資料行必須個別對齊根據其型別。 簡單的解決方案是為所有的資料行大小的最大的對齊界限，也就是 4 在下圖所示的範例。  
  
 ![最大的對齊界限繫結](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 雖然此解決方案可讓更大的漏洞，來實作它的程式碼會是相當簡單又快速。 在大部分情況下，此位移支付未使用的記憶體中的負面影響。 如需使用這個方法的範例，請參閱 <<c0> [ 使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。
