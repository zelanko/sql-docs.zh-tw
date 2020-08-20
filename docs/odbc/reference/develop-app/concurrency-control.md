---
description: 並行控制
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e47308cc0224ef73689a3b82d1ab4186fd0c823a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461550"
---
# <a name="concurrency-control"></a>並行控制
*並行* 存取是兩筆交易同時使用相同資料的能力，而增加的交易隔離通常會減少並行。 這是因為交易隔離通常是藉由鎖定資料列來執行，而且當鎖定更多資料列時，可以完成較少的交易，而不會被鎖定的資料列暫時封鎖。 雖然減少平行存取通常是為了維護資料庫完整性所需的較高交易隔離等級而被接受，但使用資料指標的大量讀取/寫入活動的互動式應用程式可能會造成問題。  
  
 例如，假設應用程式執行 ** \* 從 Orders 選取**的 SQL 語句。 它會呼叫 **SQLFetchScroll** 以在結果集周圍滾動，並允許使用者更新、刪除或插入訂單。 當使用者更新、刪除或插入訂單之後，應用程式就會認可交易。  
  
 如果隔離等級是可重複讀取的，交易可能會根據其實的方式來鎖定 **SQLFetchScroll**傳回的每個資料列。 如果隔離等級是可序列化的，交易可能會鎖定整個 Orders 資料表。 在任一種情況下，只有在認可或回復交易時，交易才會釋放鎖定。 如此一來，如果使用者花了很多時間來閱讀訂單，而且很少時間更新、刪除或插入，交易就可以輕鬆地鎖定大量的資料列，讓其他使用者無法使用。  
  
 即使資料指標是唯讀的，而且應用程式允許使用者唯讀取現有的訂單，也是問題。 在此情況下，當應用程式在自動認可模式中呼叫 **SQLCloseCursor** (時，應用程式會認可交易，並釋放鎖定) 或在手動認可模式) 中 **SQLEndTran** (。  
  
 此章節包含下列主題。  
  
-   [並行類型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [開放式並行存取](../../../odbc/reference/develop-app/optimistic-concurrency.md)
