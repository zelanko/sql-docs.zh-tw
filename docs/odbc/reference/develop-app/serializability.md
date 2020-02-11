---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49552e7333d8cac2b55a9ae6e8dd7a41ff4c5955
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094327"
---
# <a name="serializability"></a>可序列化能力
在理想的情況下，交易應該*是可序列化*的。 如果同時執行交易的結果與以序列方式執行的結果相同（也就是在另一個之後），則會將交易視為可序列化。 第一次執行交易並不重要，只有結果不會反映任何混合的交易。  
  
 例如，假設交易 A 將資料值乘以2，而交易 B 加1到資料值。 現在假設有兩個數據值：0和10。 如果這些交易會逐一執行，新的值將會是1和21（如果先執行交易 A）或2和22（如果先執行交易 B）。 但是，如果兩個交易的執行順序不同于每個值，該怎麼辦？ 如果先在第一個值上執行交易 A，然後在第二個值上先執行交易 B，則新的值為1和22。 如果此順序相反，新的值會是2和21。 如果1、21和2、22是唯一可能的結果，則交易可序列化。 如果1、22或2、21是可能的結果，則無法序列化交易。  
  
 那麼，為什麼需要可序列化能力呢？ 換句話說，為什麼在下一個交易開始之前，它會顯示一個交易完成？ 請考慮下列問題。 業務員會同時輸入當員送出帳單時的訂單。 假設推銷員從公司 X 輸入訂單，但未認可，銷售人員仍在與公司 X 的代表溝通。此職員會要求所有已開啟訂單的清單，並探索公司 X 的訂單，並將帳單傳送給他們。 現在，公司 X 的代表會決定他們想要變更訂單，讓銷售人員在認可交易之前變更它。 公司 X 取得不正確的帳單。  
  
 如果推銷員和職員的交易是可序列化的，就不會發生這個問題。 業務員的交易會在開始執行者的交易之前完成，在這種情況下，人員會送出正確的帳單，或在推銷員的交易開始之前，該職員的交易已完成，在此情況下，職員不會完全傳送帳單到公司 X。
