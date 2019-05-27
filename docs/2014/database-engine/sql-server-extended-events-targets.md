---
title: SQL Server 擴充事件目標 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- extended events [SQL Server], targets
ms.assetid: e281684c-40d1-4cf9-a0d4-7ea1ecffa384
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7be4c1cc392516ffaf6d1e36fc10b93b517d772
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088873"
---
# <a name="sql-server-extended-events-targets"></a>SQL Server Extended Events Targets
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 擴充的事件目標是事件取用者。 目標可以寫入至檔案、在記憶體緩衝區中儲存事件資料，或彙總事件資料。 目標也能夠同步或非同步處理資料。  
  
 擴充的事件設計可保證目標一定會收到事件一次，而且每個工作階段只會收到一次。  
  
 擴充的事件會提供下列幾個目標，您可將其用於擴充的事件工作階段：  
  
-   [事件計數器](../../2014/database-engine/event-counter-target.md)  
  
     計算所有指定的事件於擴充的事件工作階段期間發生的數目。 用於取得有關工作負載特性的資訊，而不會增加完整事件收集的負擔。 這是同步目標。  
  
-   [事件檔案](../../2014/database-engine/event-file-target.md)  
  
     用於將完整記憶體緩衝區的事件工作階段輸出寫入磁碟。 這是非同步目標。  
  
-   [事件配對](../../2014/database-engine/event-pairing-target.md)  
  
     許多種類的事件都是以成對的形式發生，例如鎖定取得和鎖定釋放。 用於判斷指定之配對事件不會發生在相符集合中的時機。 這是非同步目標。  
  
-   [Windows (ETW) 事件追蹤](../relational-databases/extended-events/event-tracing-for-windows-target.md)  
  
     用於建立 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 事件與 Windows 作業系統或應用程式事件資料的關聯。 這是同步目標。  
  
-   [長條圖](../../2014/database-engine/histogram-target.md)  
  
     用於根據指定的事件資料行或動作，計算指定之事件的發生次數。 這是非同步目標。  
  
-   [信號緩衝區](../../2014/database-engine/ring-buffer-target.md)  
  
     用於根據先進先出 (FIFO) 規則或每一個事件的 FIFO 規則，將事件資料存放於記憶體。 這是非同步目標。  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../relational-databases/extended-events/extended-events.md)   
 [SQL Server 擴充事件封裝](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [SQL Server 擴充的事件工作階段](../relational-databases/extended-events/sql-server-extended-events-sessions.md)   
 [SQL Server 擴充的事件引擎](../relational-databases/extended-events/sql-server-extended-events-engine.md)  
  
  
