---
title: 交易 ODBC |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297953"
---
# <a name="transactions-odbc"></a>交易 ODBC
*事務*是作為單個原子操作完成的工作單元;也就是說,操作作為一個整體成功或失敗。 例如,考慮將資金從一個銀行帳戶轉移到另一個銀行帳戶。 這涉及兩個步驟:從第一個帳戶提取資金,然後存入第二個帳戶。 這兩個步驟都很重要;一步成功是不能接受的,另一個步驟是失敗的。 支援事務的資料庫能夠保證這一點。  
  
 事務可以通過*提交*或*回滾*來完成。 提交事務時,該事務中所做的更改將永久化。 回滾事務時,受影響的行將返回到啟動事務之前的狀態。 要擴展帳戶轉移範例,應用程式將執行一個 SQL 語句來轉帳第一個帳戶,另一個 SQL 語句貸記第二個帳戶。 如果兩個語句都成功,則應用程式隨後將提交事務。 但是,如果任一語句由於任何原因失敗,應用程式將回滾事務。 在這兩種情況下,應用程式都保證事務結束時的狀態一致。  
  
 單個事務可以包含在不同時間發生的多個資料庫操作。 如果其他事務完全有權訪問中間結果,則事務可能會相互干擾。 例如,假設一個事務插入一行,第二個事務讀取該行,第一個事務回滾。 第二個事務現在具有不存在的行的數據。  
  
 為了解決這個問題,有各種方案可以隔離事務彼此。 *事務隔離*通常通過鎖定行實現,這排除了多個事務同時使用同一行。 在某些資料庫中,鎖定行也可能鎖定其他行。  
  
 隨著事務隔離的增加,*併發性降低,* 或者兩個事務同時使用相同的數據的能力。 有關詳細資訊,請參閱[設定事務隔離等級](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 中的交易](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [併發控制](../../../odbc/reference/develop-app/concurrency-control.md)
