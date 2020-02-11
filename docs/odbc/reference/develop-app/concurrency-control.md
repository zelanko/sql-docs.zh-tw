---
title: 並行控制 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c541bf28c1d4c7ec2e2041201bd7c168625bb34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083266"
---
# <a name="concurrency-control"></a>並行控制
*並行*存取是兩筆交易同時使用相同資料的能力，而增加的交易隔離通常會降低並行。 這是因為交易隔離通常是藉由鎖定資料列來執行，而當鎖定更多資料列時，可以在不被鎖定資料列暫時封鎖的情況下完成較少的交易。 雖然降低並行通常是為了維護資料庫完整性所需的較高交易隔離等級而被視為取捨，但是在具有使用資料指標的高讀取/寫入活動的互動式應用程式中，可能會造成問題。  
  
 例如，假設應用程式執行**從 Orders 選取\* **的 SQL 語句。 它會呼叫**SQLFetchScroll**以在結果集附近進行滾動，並允許使用者更新、刪除或插入訂單。 在使用者更新、刪除或插入訂單之後，應用程式會認可交易。  
  
 如果隔離等級是可重複讀取的，則交易可能會根據其實作為方式來鎖定**SQLFetchScroll**所傳回的每個資料列。 如果隔離等級是可序列化的，交易可能會鎖定整個 Orders 資料表。 不論是哪一種情況，交易都會在認可或回復時釋放其鎖定。 因此，如果使用者花很多時間來閱讀和更新、刪除或插入訂單，交易就可以輕鬆地鎖定大量的資料列，讓其他使用者無法使用它們。  
  
 即使資料指標是唯讀的，而且應用程式允許使用者唯讀取現有的訂單，這也是問題。 在此情況下，應用程式會在呼叫**SQLCloseCursor** （處於自動認可模式）或**SQLEndTran** （在手動認可模式中）時，認可交易，並釋放鎖定。  
  
 此章節包含下列主題。  
  
-   [並行類型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)
