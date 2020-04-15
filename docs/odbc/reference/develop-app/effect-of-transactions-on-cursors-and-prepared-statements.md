---
title: 交易對游標和準備語句的影響 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef3cb4095410b8ccb03b0a138f65b8df2cfb1a4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300468"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>對資料指標和已備妥陳述式的交易影響
提交或回滾事務對游標和存取計畫具有以下影響:  
  
-   所有游標都將關閉,並且將刪除該連接上已準備好的語句的訪問計劃。  
  
-   所有游標都已關閉,並且該連接上已準備好的語句的訪問計劃保持不變。  
  
-   所有游標保持打開狀態,並且在該連接上準備好的語句的訪問計劃保持不變。  
  
 例如,假設數據源顯示此清單中的第一個行為,即這些行為中限制最嚴格的行為。 現在假設應用程式執行以下操作:  
  
1.  將提交模式設置為手動提交。  
  
2.  在報表 1 上創建銷售訂單的結果集。  
  
3.  當使用者突出顯示該訂單時,在報表 2 上的銷售訂單中創建行的結果集。  
  
4.  呼叫**SQLExecute**以執行在使用者更新行時在語句 3 上編寫的定位更新語句。  
  
5.  呼叫**SQLEndTran**提交定位的更新語句。  
  
 由於數據源的行為,步驟 5 中對**SQLEndTran**的調用會導致它關閉語句 1 和 2 上的游標,並刪除所有語句的訪問計劃。 應用程式必須重新執行語句 1 和 2 才能重新建立結果集,並在語句 3 上重新準備語句。  
  
 在自動提交模式下 **,SQLEndTran**提交事務以外的函數:  
  
-   **SQLExecute**或**SQLExecDirect**在前面的示例中,步驟 4 中對**SQLExecute**的調用提交事務。 這將導致數據源關閉語句 1 和 2 上的游標,並刪除該連接上所有語句的訪問計劃。  
  
-   **SQLBulk操作**或**SQLSetPos**在前面的範例中,假設在步驟 4 中,應用程式使用語句 2 上的SQL_UPDATE選項調用**SQLSetPos,** 而不是在語句 3 上執行定位的更新語句。 這將提交事務,並導致數據源關閉語句 1 和 2 上的遊標,並丟棄該連接上的所有訪問計劃。  
  
-   **SQLCloseCursor**在前面的示例中,假設當使用者突出顯示不同的銷售訂單時,應用程式在報表 2 上調用**SQLCloseCursor,** 然後再為新銷售訂單的行創建結果。 對**SQLCloseCursor 的**呼叫提交**SELECT**語句,該語句創建了結果行集,並導致資料源關閉語句 1 上的遊標,然後丟棄該連接上的所有訪問計畫。  
  
 應用程式(尤其是基於螢幕的應用程式,使用者滾動的結果集並更新或刪除行)必須小心編寫圍繞此行為的代碼。  
  
 要確定資料來源在提交或回滾事務時的行為方式,應用程式使用SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR選項調用**SQLGetInfo。**
