---
title: 記憶體最佳化資料表上的了解交易 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 604e6670d6a28f7b4a700d7a7b8f156cc67d0a54
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132711"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>了解記憶體最佳化資料表上的交易
  交易會使用一種開放式多重版本並行控制的形式，存取記憶體最佳化的資料表。 這表示有不同版本的資料。 每一筆交易都會在它自己的交易一致性資料庫版本上運作，與其他並行執行的交易無關。 此外，交易會在開放式假設下運作，並不會與其他並行交易發生衝突。 如此就不需要使用鎖定，不過需要系統偵測衝突，並終止其中一個衝突的交易。 只有寫入-寫入交易和讀取-寫入交易會發生衝突。 如果發生寫入-寫入衝突，其中一個寫入交易會終止。  
  
 就 READ_COMMITTED_SNAPSHOT 和 SNAPSHOT 交易隔離等級而言，記憶體最佳化資料表的並行存取控制與以磁碟為基礎的資料表的並行存取控制之間有相似之處。 (如需磁碟型資料表的詳細資訊，請參閱[Database Engine 中資料列版本設定式隔離等級](http://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx)。)  
  
## <a name="topics-in-this-section"></a>本節主題  
 本節中有關記憶體最佳化資料表交易的說明，涵蓋下列主題：  
  
-   [具有記憶體最佳化資料表交易隔離等級的指導方針](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [指導方針的記憶體最佳化資料表上的交易重試邏輯](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [記憶體最佳化資料表中的交易](transactions-in-memory-optimized-tables.md)  
  
-   [交易隔離等級](transaction-isolation-levels.md)  
  
-   [跨容器交易](cross-container-transactions.md)  
  
 如需詳細資訊，請參閱[控制交易持久性](../relational-databases/logs/control-transaction-durability.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  