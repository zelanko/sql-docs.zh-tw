---
title: 可序列化 |微軟文件
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
ms.openlocfilehash: 0557e011578d313765614c05a2a9cf1b975bbc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304159"
---
# <a name="serializability"></a>可序列化能力
理想情況下,事務應該是*可序列化的*。 如果同時運行事務的結果與串行運行事務的結果相同(即一個接一個)時,事務就表示可序列化。 首先執行哪個事務並不重要,只是結果不反映事務的任何混合。  
  
 例如,假設事務 A 將數據值乘以 2,事務 B 將 1 添加到數據值。 現在假設有兩個數據值:0 和 10。 如果這些事務一個接一個運行,則如果事務 A 先運行,則新值為 1 和 21;如果事務 B 先運行,則為 2 和 22。 但是,如果兩個事務的運行順序因每個值而異,該怎麼辦? 如果事務 A 先在第一個值上運行,而事務 B 在第二個值上首先運行,則新值為 1 和 22。 如果反轉此順序,則新值為 2 和 21。 如果唯一可能的結果為 1、21 和 2、22,則事務是可序列化的。 如果可能是 1、22 或 2、21,則事務不可序列化。  
  
 那麼,為什麼序列化是可取的呢? 換句話說,為什麼在下一個事務開始之前,一個事務似乎完成很重要? 請考慮以下問題。 一個推銷員正在輸入訂單,同時一個職員正在發單。 假設銷售員從 X 公司輸入訂單,但不提交訂單;售貨員還在和X公司的代表談話。店員請求所有已結訂單的清單,並發現公司 X 的訂單併發送給他們帳單。 現在,公司 X 的代表決定要更改訂單,因此銷售員在提交交易之前更改了訂單。 公司 X 收到不正確的帳單。  
  
 如果銷售員和職員的交易是可連載的,那麼這個問題就不會發生。 要麼銷售員的交易在店員的交易開始之前就完成,在這種情況下,職員會寄出正確的帳單,要麼職員的交易在銷售員的交易開始之前完成,在這種情況下,職員根本不會向 X 公司發送帳單。
