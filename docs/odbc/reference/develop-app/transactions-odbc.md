---
description: 交易 ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c40c51fa2b0154d90d5ea08952266997d175e3e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456422"
---
# <a name="transactions-odbc"></a>交易 ODBC
*交易*是以單一、不可部分完成的作業來完成的工作單位;也就是說，此作業會以整體方式成功或失敗。 例如，請考慮從一個銀行帳戶轉移到另一個銀行帳戶。 這包括兩個步驟：從第一個帳戶提款 money，然後將它放在第二個帳戶中。 這兩個步驟都必須成功;一個步驟無法接受，而另一個步驟失敗。 支援交易的資料庫能夠保證這一點。  
  
 您可以藉由 *認可* 或 *復原*來完成交易。 認可交易時，會將該交易中所做的變更設為永久。 當交易回復時，受影響的資料列會傳回至交易開始之前的狀態。 為了延伸帳戶轉移範例，應用程式會執行一個 SQL 語句來為第一個帳戶進行付款，並使用不同的 SQL 語句來點數第二個帳戶。 如果兩個語句都成功，則應用程式會認可交易。 但是，如果其中一個語句因為任何原因而失敗，應用程式就會回復交易。 無論是哪一種情況，應用程式都可保證交易結束時的一致狀態。  
  
 單一交易可包含在不同時間執行的多個資料庫作業。 如果其他交易具有中繼結果的完整存取權，交易可能會彼此干擾。 例如，假設有一個交易插入一個資料列，第二筆交易讀取該資料列，然後回復第一個交易。 第二筆交易現在具有不存在之資料列的資料。  
  
 若要解決此問題，您可以使用各種不同的配置來隔離彼此的交易。 *交易隔離* 通常是藉由鎖定資料列來執行，這可防止多個交易同時使用同一個資料列。 在某些資料庫中，鎖定資料列也可能會鎖定其他資料列。  
  
 提高交易隔離會減少 *平行存取，* 或兩筆交易同時使用相同資料的能力。 如需詳細資訊，請參閱 [設定交易隔離等級](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 中的交易](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [交易隔離](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [並行控制](../../../odbc/reference/develop-app/concurrency-control.md)
