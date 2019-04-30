---
title: 交易 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6ce5decd2744c0ce9d753e355321a40d00fd620
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305806"
---
# <a name="transactions-odbc"></a>交易 ODBC
A*交易*是工作單位，是以單一、 不可部分完成的作業; 也就是說，作業成功或失敗的整體。 比方說，請考慮將 money 從一個銀行帳戶傳輸到另一個。 這牽涉到兩個步驟： 從第一個帳戶提款金額和存入第二個。 很重要，這兩個步驟都成功您不接受用於成功的一個步驟，另一個則失敗。 支援交易的資料庫可保證這點。  
  
 在也可以完成的交易*認可*或正在*回復*。 認可交易時，所做的在交易進行永久變更。 當交易回復時，受影響的資料列會回到交易啟動之前的狀態。 若要擴充帳戶傳輸範例，在應用程式會執行一個 SQL 陳述式，來轉帳的第一個帳戶和不同的 SQL 陳述式來第二個帳戶。 如果兩個陳述式成功，然後在應用程式就會認可交易。 但是，如果其中一個陳述式因為任何原因失敗，應用程式回復交易。 在任一情況下，應用程式可確保一致的狀態，在交易結束。  
  
 在單一交易可以包含多個資料庫作業發生在不同的時間。 如果其他交易都有完整的存取權的中繼結果，交易可能會干擾另一個。 例如，假設一筆交易中插入一個資料列，第二筆交易讀取該資料列，且第一個交易已回復。 第二筆交易現在已不存在的資料列的資料。  
  
 若要解決此問題，有各種不同的配置，以找出從另一個交易。 *交易隔離*通常會實作鎖定的資料列，無法讓多個交易同時使用相同的資料列。 在某些資料庫中，鎖定資料列可能也會鎖定其他資料列。  
  
 增加了交易隔離開始降低*並行存取，* 或兩個交易能夠同時使用相同的資料。 如需詳細資訊，請參閱 <<c0> [ 設定 Transaction Isolation Level](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 中的交易](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [並行控制](../../../odbc/reference/develop-app/concurrency-control.md)
