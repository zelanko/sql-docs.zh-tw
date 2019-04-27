---
title: 了解記憶體最佳化資料表上的交易 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ceedcedae64bf2ec8f8ede0ccbb99350b979fd7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773375"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>了解記憶體最佳化資料表上的交易
  交易會使用一種開放式多重版本並行控制的形式，存取記憶體最佳化的資料表。 這表示有不同版本的資料。 每一筆交易都會在它自己的交易一致性資料庫版本上運作，與其他並行執行的交易無關。 此外，交易會在開放式假設下運作，並不會與其他並行交易發生衝突。 如此就不需要使用鎖定，不過需要系統偵測衝突，並終止其中一個衝突的交易。 只有寫入-寫入交易和讀取-寫入交易會發生衝突。 如果發生寫入-寫入衝突，其中一個寫入交易會終止。  
  
 就 READ_COMMITTED_SNAPSHOT 和 SNAPSHOT 交易隔離等級而言，記憶體最佳化資料表的並行存取控制與以磁碟為基礎的資料表的並行存取控制之間有相似之處。 (如需有關磁碟基礎之資料表的詳細資訊，請參閱[Database Engine 中資料列版本設定式隔離等級](https://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx)。)  
  
## <a name="topics-in-this-section"></a>本節主題  
 本節中有關記憶體最佳化資料表交易的說明，涵蓋下列主題：  
  
-   [搭配經記憶體最佳化的資料表使用交易隔離等級的方針](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [經記憶體最佳化的資料表上交易的重試邏輯方針](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [經記憶體最佳化的資料表中的交易](transactions-in-memory-optimized-tables.md)  
  
-   [交易隔離等級](transaction-isolation-levels.md)  
  
-   [跨容器交易](cross-container-transactions.md)  
  
 如需詳細資訊，請參閱[控制交易持久性](../relational-databases/logs/control-transaction-durability.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
