---
title: "SQL Server：HTTP_STORAGE_OBJECT | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: 7
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# SQL Server：HTTP_STORAGE_OBJECT
  **SQLServer:HTTP_STORAGE_OBJECT** 效能物件包含監視 Windows Azure 儲存體帳戶的效能計數器。 您可以使用 [Microsoft Azure 中的 SQL Server 資料檔案](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)功能，在 Windows Azure 儲存體 Blob 中儲存資料庫檔案。 這個效能物件會將每個 Windows Azure 儲存體帳戶視為不同的磁碟機。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**Read Bytes/sec**|讀取作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**Write Bytes/sec**|寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**Total Bytes/sec**|讀取或寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**讀取次數/秒**|HTTP 儲存體的每秒讀取次數。|  
|**寫入次數/秒**|HTTP 儲存體的每秒寫入次數。|  
|**Transfers/sec**|HTTP 儲存體的每秒讀取和寫入作業數目。|  
|**Avg. Bytes/Read**|每次讀取時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**Avg. Bytes/Read BASE**|僅供內部使用。|
|**Avg. Bytes/Transfer**|讀取或寫入作業期間傳輸自 HTTP 儲存體的平均位元組數目。|  
|**Avg. Bytes/Transfer BASE**|僅供內部使用。|
|**Avg. Bytes/Write**|每次寫入時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**Avg. Bytes/Write BASE**|僅供內部使用。|
|**Avg. microsec/Read**|每次讀取自 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Read BASE**|僅供內部使用。|
|**Avg. microsec/Read Comp**|HTTP 完成讀取儲存體所花費的平均毫秒數。| 
|**Avg. microsec/Read Comp BASE**|僅供內部使用。|
|**Avg. microsec/Write**|每次寫入 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Transfer**|每次傳輸至 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Transfer BASE**|僅供內部使用。|
|**Avg. microsec/Write BASE**|僅供內部使用。|
|**Avg. microsec/Write Comp**|HTTP 完成寫入儲存體所花費的平均毫秒數。|  
|**Avg. microsec/Write Comp BASE**|僅供內部使用。|
|**Outstanding HTTP Storage I/O**|目標是 HTTP 儲存體的未完成 I/O 總數。|  
|**HTTP Storage IO failed/sec**|每秒傳送至 HTTP 儲存體的失敗寫入要求數目。| 
|**HTTP Storage I/O Retry/sec**|每秒傳送至 HTTP 儲存體的重試要求數目。|  
  
## 另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  