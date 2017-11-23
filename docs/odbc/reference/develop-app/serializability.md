---
title: "可序列化能力 |Microsoft 文件"
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
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24abc4dee066853da7b201f19839063aa437d854
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="serializability"></a>可序列化能力
在理想情況下，應該是交易*序列化*。 交易都稱為是否同時執行交易的結果相同的循序執行這些結果可序列化 — 也就是一個接著一個。 它並不重要交易第一次，執行只有該結果並不會反映任何混用的交易。  
  
 例如，假設交易 A 將資料值乘以 2 並交易 B 將 1 加入至資料值。 現在，假設有兩個資料值： 0 到 10。 如果這些交易會執行一個接著一個新的值可 1 與 21 如果交易 A 執行第一次，或 2 以及 22 交易 B 優先執行。 但如果兩筆交易中執行的順序不同的是每個值嗎？ 如果第一個值優先執行的交易和交易 B 執行，第一個第二個值，新的值是 1 到 22。 如果此順序會顛倒，新的值為 2 和 21。 交易是序列化的 1、 21 和 2，22 是否唯一可能的結果。 交易是不 serializable 如果 1、 22 或 2、 21 是可能的結果。  
  
 為何，所以可序列化能力需要這樣做？ 換句話說，它為何如此重要，它會顯示該一筆交易完成之前啟動下一個交易嗎？ 請考慮下列問題。 拜訪客戶順序在同一時間 clerk 送出帳單輸入訂單。 假設拜訪客戶順序輸入訂單從公司 X，但不是會認可它。業務員仍向該代表從公司 X。Clerk 要求的所有開啟的訂單清單和探索 X 公司的順序，並將它們傳送帳單。 現在該代表從 X 公司決定他們想要變更其順序，因此拜訪客戶順序則會認可交易之前變更它。 X 公司取得不正確的帳單。  
  
 如果序列化拜訪客戶順序的和 clerk 的交易，永遠不可能發生這個問題。 Clerk 的交易開始，在此情況下您會有 clerk 送出正確的帳單之前, 會完成拜訪客戶順序的交易或交易的 clerk 會完成在此情況下拜訪客戶順序的交易開始之前clerk 就不具有傳送帳單到 X 公司完全。
