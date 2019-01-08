---
title: 並行存取控制 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2e54298e9c25777f10b92f322f1b1e6a3d94c243
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52528026"
---
# <a name="concurrency-control"></a>並行存取控制
*並行*是兩個交易的能力，在此同時，使用相同的資料和增加的交易隔離通常是並行減少。 這是因為交易隔離通常會實作鎖定的資料列，而且多個資料列被鎖住，因為較少的交易可以完成而不被鎖定的資料列至少要暫時封鎖。 雖然並行減少一般認為需要維護資料庫的完整性較高交易隔離等級的取捨，它具有使用資料指標的高的讀取/寫入活動成為互動式應用程式中的問題。  
  
 例如，假設應用程式執行的 SQL 陳述式**選取 \*從訂單**。 它會呼叫**SQLFetchScroll**來捲動結果設定，並可讓使用者更新，請刪除或插入訂單。 使用者更新、 刪除或插入訂單之後，應用程式就會認可交易。  
  
 如果隔離等級是 Repeatable Read，交易可能會為根據的實作方式-鎖定所傳回的每個資料列**SQLFetchScroll**。 如果隔離等級為 Serializable，交易可能會鎖定整個 Orders 資料表。 在任一情況下，交易認可或回復時，才釋放其鎖定。 因此如果使用者耗費太多時間來閱讀訂單和很短的時間更新、 刪除或插入，交易可以輕鬆地鎖定大量的資料列，讓其他使用者無法使用。  
  
 即使資料指標是唯讀的且應用程式可讓使用者讀取只有現有的訂單，這會是問題。 在此情況下，應用程式認可交易，並釋放鎖定，它會呼叫**SQLCloseCursor** （在自動認可模式） 或**SQLEndTran** （在手動認可模式）。  
  
 此章節包含下列主題。  
  
-   [並行類型](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [開放式並行](../../../odbc/reference/develop-app/optimistic-concurrency.md)
