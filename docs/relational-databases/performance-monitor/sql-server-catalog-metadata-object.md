---
title: "SQL Server, Catalog Metadata Object | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:Catalog Metadata"
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
caps.latest.revision: 4
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 4
---
# SQL Server, Catalog Metadata Object
**SQLServer:Catalog Metadata** 效能物件提供 SQL Server 之目錄中繼資料的計數器。

下表描述 SQL Server **Catalog Metadata** 效能物件。


|**SQL Server Catalog Metadata 計數器**|說明|  
|-------------|-----------------|  
|**Cache Entries Count**|目錄中繼資料快取中的項目數。|
|**Cache Entries Pinned Count**|已釘選的目錄中繼資料快取項目數。|
|**Cache Hit Ratio**|目錄中繼資料快取叫用數與查閱數之間的比率。|
|**Cache Hit Ratio Base**|僅供內部使用。|

每個資料庫都有一個計數器執行個體。

## 另請參閱  
[監視資源使用狀況 (系統監視器)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)