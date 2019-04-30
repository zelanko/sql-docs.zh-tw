---
title: 資料指標和已備妥的陳述式的交易影響 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41c2c6b06744965144ca9d5feb27e9ea16d9903c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305720"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>對資料指標和已備妥陳述式的交易影響
認可或回復交易，包含對資料指標和存取計劃的下列影響：  
  
-   所有的資料指標都會關閉，而且存取計劃在該連接上備妥的陳述式會刪除。  
  
-   所有的資料指標都會關閉，並已備妥的陳述式的存取方案，在該連接上維持不變。  
  
-   所有的資料指標維持開啟，並已備妥的陳述式的存取方案，在該連接上維持不變。  
  
 例如，假設資料來源會表現這份清單，最嚴格的限制，這些行為中的第一個行為。 現在假設應用程式會進行下列作業：  
  
1.  將認可模式設定為手動認可。  
  
2.  陳述式 1 中建立銷售訂單的結果集。  
  
3.  使用者會反白顯示該訂單時，請建立陳述式 2 上的銷售訂單中的結果集一條線。  
  
4.  呼叫**SQLExecute**時要執行定位的 update 陳述式已備妥的陳述式 3，使用者更新一條線。  
  
5.  呼叫**SQLEndTran**認可定位的 update 陳述式。  
  
 由於資料來源的行為，呼叫**SQLEndTran**在步驟 5 會導致它關閉 1 和 2 的陳述式中的資料指標，並刪除所有陳述式的存取計劃。 應用程式必須重新執行陳述式 1 和 2 來重新建立結果集，並 reprepare 陳述式 3 中的陳述式。  
  
 在自動認可模式下，函式以外**SQLEndTran**認可交易：  
  
-   **SQLExecute**或是**SQLExecDirect**在上述範例中，呼叫**SQLExecute**在步驟 4 會認可交易。 這會導致要關閉資料指標陳述式 1 和 2，並刪除存取計劃，在該連接上的所有陳述式的資料來源。  
  
-   **SQLBulkOperations**或是**SQLSetPos**在上述範例中，假設在步驟 4 中的應用程式會呼叫這些**SQLSetPos**帶有 SQL_UPDATE 選項，而不是執行的陳述式 2陳述式 3 上的定位的 update 陳述式。 此認可交易會使的資料指標的陳述式 1 和 2，資料來源，並會捨棄該連接上的所有存取計劃。  
  
-   **SQLCloseCursor**在上述範例中，假設使用者會反白顯示不同的銷售訂單，當應用程式呼叫**SQLCloseCursor**上建立新的銷售行的結果之前的陳述式 2順序。 若要在呼叫**SQLCloseCursor**認可**選取**陳述式，建立結果集的行並會導致要關閉陳述式 1，資料指標的資料來源，然後再捨棄上的所有存取計劃連接。  
  
 應用程式，尤其是螢幕為基礎的應用程式在使用者捲動的結果集和更新或刪除資料列，必須非常小心略過這個問題的程式碼。  
  
 若要判斷認可或回復交易時，資料來源的運作方式，應用程式會呼叫**SQLGetInfo**使用 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項。
