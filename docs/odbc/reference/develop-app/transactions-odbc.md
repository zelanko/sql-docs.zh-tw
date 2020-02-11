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
ms.openlocfilehash: 521a2ffbf0f8eb5e2590ae6e42d50dc71d536683
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086039"
---
# <a name="transactions-odbc"></a>交易 ODBC
*交易*是做為單一、不可部分完成作業的工作單位。也就是說，作業會成功或整體失敗。 例如，請考慮將金錢從一個銀行帳戶轉移到另一個。 這包含兩個步驟：從第一個帳戶提款 money，然後將它放在第二個帳戶。 這兩個步驟都必須成功;一個步驟無法接受，而另一個則失敗。 支援交易的資料庫能夠保證此情況。  
  
 交易可以藉由*認可*或*回復*來完成。 認可交易時，在該交易中所做的變更會成為永久的。 當交易回復時，受影響的資料列會回到其所在的狀態，然後才啟動交易。 為了擴充帳戶傳輸範例，應用程式會執行一個 SQL 語句來為第一個帳戶進行付款，並使用不同的 SQL 語句來取得第二個帳戶的信用額度。 如果這兩個語句都成功，應用程式就會認可交易。 但是，如果任一語句因任何原因而失敗，應用程式就會回復交易。 不論是哪一種情況，應用程式都保證交易結束時的狀態一致。  
  
 單一交易可以包含在不同時間發生的多個資料庫作業。 如果其他交易擁有中繼結果的完整存取權，交易可能會彼此干擾。 例如，假設有一個交易插入一個資料列，第二筆交易讀取該資料列，而第一個交易已回復。 第二筆交易現在具有不存在之資料列的資料。  
  
 若要解決這個問題，有各種不同的配置可以隔離彼此的交易。 *交易隔離*通常是藉由鎖定資料列來執行，這可防止多個交易同時使用相同的資料列。 在某些資料庫中，鎖定資料列可能也會鎖定其他資料列。  
  
 交易隔離增加時，會降低*並行，* 或兩筆交易同時使用相同資料的能力。 如需詳細資訊，請參閱[設定交易隔離等級](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 中的交易](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [並行控制](../../../odbc/reference/develop-app/concurrency-control.md)
