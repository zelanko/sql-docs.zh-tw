---
title: "對資料指標和已備妥的陳述式的交易影響 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2533778f9b0e837ce59850d4f70a3c4545f8be60
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>對資料指標和已備妥的陳述式的交易影響
認可或回復的交易具有下列資料指標和存取計劃作用：  
  
-   所有的資料指標都會關閉，並備妥的陳述式的存取計畫在該連接上會被刪除。  
  
-   所有的資料指標都會關閉，並備妥的陳述式的存取計畫在該連接上維持不變。  
  
-   所有資料指標維持開啟，而且已備妥陳述式在該連接上的存取計畫仍維持不變。  
  
 例如，假設資料來源會表現這份清單，最嚴格的限制，這些行為中的第一個行為。 現在假設應用程式會進行下列作業：  
  
1.  將認可模式設定為手動認可。  
  
2.  陳述式 1 上建立結果集的銷售訂單。  
  
3.  當使用者反白顯示該訂單，建立陳述式 2 上的銷售訂單中線條的結果集。  
  
4.  呼叫**SQLExecute**執行定位的更新陳述式已經準備好陳述式 3 上，當使用者更新一條線。  
  
5.  呼叫**SQLEndTran**認可定位的 update 陳述式。  
  
 由於資料來源的行為，呼叫**SQLEndTran**在步驟 5 會使它時關閉資料指標陳述式 1 和 2，並刪除所有陳述式的存取計畫。 應用程式必須重新執行陳述式 1 和 2 來重新建立結果集，並 reprepare 3 陳述式中的陳述式。  
  
 在自動認可模式下，函式以外**SQLEndTran**認可的交易：  
  
-   **SQLExecute**或**SQLExecDirect**在上述範例中，呼叫**SQLExecute**在步驟 4 會認可交易。 這會導致資料來源，以關閉在 1 和 2 的陳述式上的資料指標並刪除該連接上的所有陳述式的存取計畫。  
  
-   **SQLBulkOperations**或**SQLSetPos**在上述範例中，假設在步驟 4 應用程式會呼叫這些**SQLSetPos**帶有 SQL_UPDATE 選項，而不會執行的陳述式 2 上3 陳述式上的定位的 update 陳述式。 如此會認可交易並造成來關閉資料指標陳述式 1 和 2，資料來源並會捨棄該連接上的所有存取計劃。  
  
-   **SQLCloseCursor**在上述範例中，假設當使用者反白顯示不同的銷售訂單，應用程式呼叫**SQLCloseCursor**上建立新的銷售的行的結果之前的 2 陳述式順序。 若要呼叫**SQLCloseCursor**認可**選取**陳述式，建立結果集的行和導致時關閉資料指標陳述式 1，資料來源，然後再捨棄上的所有存取計劃連接。  
  
 應用程式，尤其是螢幕型應用程式在使用者捲動的結果集和更新或刪除資料列，必須非常小心略過這個問題的程式碼。  
  
 若要判斷認可或回復交易時，資料來源的行為方式，應用程式呼叫**SQLGetInfo**與 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項。

