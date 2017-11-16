---
title: "SQL Server 的 Plan Cache 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Plan Cache object
- SQLServer:Plan Cache
ms.assetid: 225e2b02-8d2f-4f29-9eba-f5847c36ea99
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87782a0bf224fbc570f8bec97572ab3278d1fd6d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-plan-cache-object"></a>SQL Server 的 Plan Cache 物件
  **Plan Cache** 物件所提供的計數器，可監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何使用記憶體來儲存物件，例如預存程序、特定與備妥 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以及觸發程序。 可同時監視 **Plan Cache** 物件的多個執行個體，每個執行個體都代表所要監視的不同計畫類型。  
  
 下表描述 **SQLServer:Plan Cache**計數器。  
  
|SQL Server Plan Cache 計數器|描述|  
|------------------------------------|-----------------|  
|**Cache Hit Ratio**|快取叫用數和查閱數之間的比率|  
|**Cache Hit Ratio Base**|僅供內部使用。| 
|**Cache Object Counts**|快取中的快取物件數。|  
|**快取頁面**|快取物件所用的 8 KB 分頁數。|  
|**Cache Objects in use**|使用中的快取物件數目。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|Plan Cache 執行個體|描述|  
|-------------------------|-----------------|  
|**_Total**|所有快取執行個體類型的資訊。|  
|**Sql Plans**|從特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢 (包括自動參數化查詢) 產生的查詢計劃，或從使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_prepare **或** sp_cursorprepare **準備之**陳述式產生的查詢計劃。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會快取特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的計畫，以便稍後執行相同的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時重複使用。 使用者的參數化查詢 (即使未確實預備) 也會當作預備的 SQL 計畫來監視。|  
|**Object Plans**|藉著建立預存程序、函數或觸發程序而產生的查詢計畫。|  
|**Bound Trees**|檢視、規則、計算資料行與檢查條件約束的正規化樹。|  
|**擴充預存程序**|擴充預存程序的目錄資訊。|  
|**暫存資料表 & 資料表變數**|與暫存資料表和資料表變數相關的快取資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server 的 Buffer Manager 物件](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
