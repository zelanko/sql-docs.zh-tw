---
description: 對資料指標和已備妥陳述式的交易影響
title: 交易對資料指標和已備妥語句的影響 |Microsoft Docs
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
ms.openlocfilehash: 248865b70115a64f73ce93dbd966dac94db61a0a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482971"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>對資料指標和已備妥陳述式的交易影響
認可或回復交易對資料指標和存取計畫會有下列影響：  
  
-   所有資料指標都會關閉，而且會刪除該連接上備妥語句的存取計畫。  
  
-   所有資料指標都會關閉，且該連接上備妥語句的存取計畫會維持不變。  
  
-   所有資料指標都會保持開啟狀態，而該連接上備妥之語句的存取計畫仍會保持不變。  
  
 例如，假設資料來源展示了這份清單中的第一個行為，這些行為最嚴格。 現在假設應用程式會執行下列動作：  
  
1.  將認可模式設定為手動認可。  
  
2.  在語句1上建立銷售訂單的結果集。  
  
3.  當使用者反白顯示該順序時，在語句2的銷售訂單中建立各行的結果集。  
  
4.  當使用者更新一行時，呼叫 **SQLExecute** 來執行已在語句3上備妥的定點更新語句。  
  
5.  呼叫 **SQLEndTran** 來認可定位的 update 語句。  
  
 由於資料來源的行為，在步驟5中呼叫 **SQLEndTran** 會導致它關閉語句1和2上的資料指標，並在所有語句上刪除存取計畫。 應用程式必須重新建立語句1和2，才能重新建立結果集，並 reprepare 語句3上的語句。  
  
 在自動認可模式中， **SQLEndTran** 認可交易以外的函數：  
  
-   **SQLExecute** 或 **SQLExecDirect** 在上述範例中，步驟4中的 **SQLExecute** 呼叫會認可交易。 這會導致資料來源關閉語句1和2上的資料指標，並在該連接上的所有語句上刪除存取計畫。  
  
-   **SQLBulkOperations** 或 **SQLSetPos** 在上述範例中，假設在步驟4中，應用程式會使用語句2上的 SQL_UPDATE 選項來呼叫 **SQLSetPos** ，而不是在語句3上執行定位的 UPDATE 語句。 這會認可交易，並導致資料來源關閉語句1和2上的資料指標，並捨棄該連接上的所有存取計畫。  
  
-   **SQLCloseCursor** 在上述範例中，假設當使用者強調不同的銷售訂單時，應用程式會在語句2上呼叫 **SQLCloseCursor** ，然後再為新的銷售訂單建立線條結果。 對 **SQLCloseCursor** 的呼叫會認可建立程式列結果集的 **SELECT** 語句，並導致資料來源關閉語句1上的資料指標，然後捨棄該連接上的所有存取計畫。  
  
 應用程式（尤其是以螢幕為基礎的應用程式，使用者會在其中滾動結果集和更新或刪除資料列），必須小心地針對此行為進行編碼。  
  
 若要判斷資料來源在認可或回復交易時的行為方式，應用程式會使用 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項來呼叫 **SQLGetInfo** 。
