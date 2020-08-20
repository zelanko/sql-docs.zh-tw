---
description: 可序列化能力
title: 可序列化能力 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b627d24b16e0bae4a117dba38de8cc1755feadac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476440"
---
# <a name="serializability"></a>可序列化能力
在理想情況下，交易應該 *是可序列化*的。 如果同時執行交易的結果與循序執行的結果相同（也就是在另一個之後），則會將交易視為可序列化。 第一次執行的交易並不重要，只有結果不會反映任何混合的交易。  
  
 例如，假設交易 A 將資料值乘以2，交易 B 會將1加上資料值。 現在假設有兩個數據值：0和10。 如果這些交易是在另一個之後執行，則如果先執行交易 A，新的值會是1和21，如果是第一次執行交易 B 則為2和22。 但是，如果這兩個交易的執行順序不同于每個值，該怎麼辦？ 如果先在第一個值上執行交易 A，然後第二個值執行交易 B，則新的值為1和22。 如果反轉此順序，新值為2和21。 如果1、21和2、22是唯一可能的結果，則交易可序列化。 如果1、22或2、21是可能的結果，則無法序列化交易。  
  
 那麼，為什麼需要可序列化能力？ 換句話說，為什麼在下一次交易開始之前，某一筆交易就會完成？ 請考慮下列問題。 當職員正在送出帳單時，會同時進入訂單。 假設推銷員從公司 X 輸入訂單，但未認可，銷售人員仍在與公司 X 的代表交談。職員會要求所有開啟訂單的清單，並探索公司 X 的訂單，並將帳單傳送給他們。 公司 X 的代表現在決定要變更訂單，讓銷售人員在認可交易之前變更。 公司 X 取得不正確的帳單。  
  
 如果推銷員和職員的交易是可序列化的，則永遠不會發生此問題。 在開始執行員的交易之前，可能會有一筆推銷員的交易完成，在這種情況下，職員會送出正確的帳單，或讓職員的交易在推銷員的交易開始之前完成，在這種情況下，職員完全不會傳送帳單給公司 X。
