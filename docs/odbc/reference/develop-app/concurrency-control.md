---
title: "並行控制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a10dc30810a1ea71bd4e2c9d823ed010f7f611d4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-control"></a>並行存取控制
*並行*是兩筆交易能夠使用相同的資料在相同的時間，並增加了交易的隔離通常會降低的並行。 這是因為交易隔離通常實作鎖定的資料列，而且因為多個資料列已鎖定，而不會至少暫時封鎖的鎖定資料列已較少的交易完成。 並行性降低通常會獲接受成為維護資料庫的完整性需要高交易隔離等級的取捨，而會變得與使用資料指標的高的讀取/寫入活動的互動式應用程式中的問題。  
  
 例如，假設應用程式執行的 SQL 陳述式**選取\*從訂單**。 它會呼叫**SQLFetchScroll**來捲動結果集以及可讓使用者更新，請刪除或插入訂單。 使用者更新、 刪除或插入訂單之後，應用程式就會認可交易。  
  
 交易隔離等級是 Repeatable Read，如果可能，根據它的實作方式 — 鎖定所傳回的每個資料列**SQLFetchScroll**。 如果隔離等級為 Serializable，交易可能會鎖定整個 Orders 資料表。 在任一情況下，交易認可或回復時，才釋放鎖定。 因此，如果使用者耗費大量時間來閱讀訂單和一點時間更新、 刪除或插入，交易無法輕鬆地鎖定大量的資料列，讓其他使用者無法使用。  
  
 這會是問題，即使資料指標是唯讀，且應用程式可讓使用者讀取唯一的現有訂單。 在此情況下，應用程式認可交易，並呼叫時，會釋放鎖定， **SQLCloseCursor** （處於自動認可模式） 或**SQLEndTran** （在手動認可模式）。  
  
 此章節包含下列主題。  
  
-   [並行類型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)
