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
manager: craigg
ms.openlocfilehash: 7e7972fb72607edca8c1599c2d028b073c184642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251474"
---
# <a name="serializability"></a>可序列化能力
在理想情況下，交易應該*序列化*。 交易可以說是可序列化，如果同時執行交易的結果相同，則為循序-執行它們的結果也就是一個接著一個。 它並不重要交易第一次，執行僅，結果不會反映任何混合的交易。  
  
 例如，假設交易 A 將資料值乘以 2，而交易 B 會將 1 加到資料值。 現在假設有兩個資料值：0 到 10。 如果這些交易運作方式的其中一個接著一個新的值可 1 和 21，如果交易 A 已先執行，或 2 以及 22 交易 B 會執行第一次。 但如果在其中執行的兩個交易的順序不同的每個值？ 如果第一個值的第一個執行的交易與交易 B 上執行時第一次的第二個值，新的值會是 1 到 22。 如果此順序會顛倒，新的值為 2 和 21。 交易都是可序列化 22 1、 21 到 2，如果是唯一可能的結果。 交易如果 1，22 或 2，21 可序列化不可能的結果。  
  
 那麼為什麼是可序列化能力理想呢？ 換句話說，為何如此重要，它會出現一個交易完成的下一個交易開始之前嗎？ 請考慮下列問題。 業務員 clerk 送出物料單的同時輸入訂單。 假設業務員 X 公司從輸入訂單，但不會認可它;業務員仍與該代表從 X 公司。Clerk 要求一份所有開啟的訂單和會探索 X 公司的順序，並將它們傳送的帳單。 現在該代表從 X 公司決定他們想要變更其順序，因此業務員則會認可交易之前變更它。 X 公司取得不正確的帳單。  
  
 如果業務員的和 clerk 的交易可序列化，就永遠不會發生此問題。 Clerk 的交易開始，在此情況下您會有 clerk 送出正確的帳單之前, 會完成業務員的交易，或在此情況下業務員的交易開始之前會完成 clerk 的交易clerk 就不具有傳送物料單到 X 公司所有。
