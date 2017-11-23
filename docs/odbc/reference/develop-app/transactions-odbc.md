---
title: "交易 ODBC |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e6e18576f4898b6902d15ab20cc5ebfcb336835
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="transactions-odbc"></a>ODBC 異動
A*交易*是工作的單位以單一、 不可部分完成的作業完成; 也就是說，作業成功，或整個失敗。 例如，請考慮將從銀行帳戶的金錢傳送到另一個。 這牽涉到兩個步驟： 從第一個帳戶提款金額和存款中第二個。 很重要，這兩個步驟就會成功。不是可接受的一個步驟，才會成功，而另一個則失敗。 支援交易的資料庫就能確保這項目。  
  
 交易的完成可能是因*認可*或正在*回復*。 認可交易時，在於交易會成為永久狀態所做的變更。 當交易回復時，受影響的資料列被回到交易啟動之前的狀態。 若要擴充帳戶傳輸範例中，應用程式會執行一個 SQL 陳述式借方的第一個帳戶和不同的 SQL 陳述式，以第二個帳戶的信用額度。 如果兩個陳述式成功，然後在應用程式就會認可交易。 但是，如果任一個陳述式失敗，因為任何原因，應用程式回復交易。 在任一情況下，應用程式可確保一致的狀態，交易的結尾。  
  
 在單一交易可以包含多個資料庫作業發生在不同的時間範圍。 如果其他的交易具有完整存取權的中繼結果，交易可能會干擾另一個。 例如，假設一筆交易中插入一個資料列，第二筆交易讀取該資料列，且第一筆交易都會回復。 第二筆交易現在具有資料列不存在的資料。  
  
 若要解決這個問題，有不同的配置，來找出與其他交易。 *交易隔離*通常實作鎖定的資料列，無法讓多個交易同時使用相同的資料列。 在某些資料庫中，鎖定資料列可能也鎖定的其他資料列。  
  
 增加交易的隔離是降低*的並行存取，*或兩個交易同時使用相同的資料的能力。 如需詳細資訊，請參閱[設定交易隔離等級](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 中的交易](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [並行控制](../../../odbc/reference/develop-app/concurrency-control.md)
