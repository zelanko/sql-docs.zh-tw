---
title: "SQL Server 的 FileTable 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLServer:FileTable
ms.assetid: 325f5e58-1095-450f-9321-dfacfe6fd55f
caps.latest.revision: "3"
author: dagiro
ms.author: v-dagir
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57a16709c701e8754446287f9d0b74b6e94581b3
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-filetable-object"></a>SQL Server 的 FileTable 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **SQLServer:FileTable** 效能物件提供與 FileTable 和非交易式存取相關聯的統計資料計數器。

下表描述 SQL Server **FileTable** 效能物件。

|**SQL Server 的 FileTable 計數器**|描述|  
|-------------|-----------------|  
|**Avg time delete FileTable item**|刪除 FileTable 項目所花費的平均時間 (以毫秒為單位)。|
|**Avg time FileTable enumeration**|FileTable 列舉要求所花費的平均時間 (以毫秒為單位)。|
|**Avg time FileTable handle kill**|終止 FileTable 處理所花費的平均時間 (以毫秒為單位)。|
|**Avg time move FileTable item**|移動 FileTable 項目所花費的平均時間 (以毫秒為單位)。|
|**Avg time per file I/O request**|處理傳入檔案 I/O 要求所花費的平均時間 (以毫秒為單位)。|
|**Avg time per file I/O response**|處理傳出檔案 I/O 回應所花費的平均時間 (以毫秒為單位)。|
|**Avg time rename FileTable item**|重新命名 FileTable 項目所花費的平均時間 (以毫秒為單位)。|
|**Avg time to get FileTable item**|擷取 FileTable 項目所花費的平均時間 (以毫秒為單位)。|
|**Avg time update FileTable item**|更新 FileTable 項目所花費的平均時間 (以毫秒為單位)。|
|**FileTable db operations/sec**|FileTable 存放區元件每秒處理的資料庫作業性事件總數。|
|**FileTable enumeration reqs/sec**|FileTable 每秒列舉項目要求的總數。|
|**FileTable file I/O requests/sec**|每秒傳入 FileTable 檔案 I/O 要求的總數。|
|**FileTable file I/O response/sec**|每秒傳出檔案 I/O 回應的總數。|
|**FileTable item delete reqs/sec**|FileTable 每秒刪除項目要求的總數。|
|**FileTable item get requests/sec**|FileTable 每秒擷取項目要求的總數。|
|**FileTable item move reqs/sec**|FileTable 每秒移動項目要求的總數。|
|**FileTable item rename reqs/sec**|FileTable 每秒重新命名項目要求的總數。|
|**FileTable item update reqs/sec**|FileTable 每秒更新項目要求的總數。|
|**FileTable kill handle ops/sec**|FileTable 每秒處理終止作業的總數。|
|**FileTable table operations/sec**|FileTable 存放區元件每秒處理的資料表作業性事件總數。|
|**Time delete FileTable item BASE**|僅供內部使用。|
|**Time FileTable enumeration BASE**|僅供內部使用。|
|**Time FileTable handle kill BASE**|僅供內部使用。|
|**Time move FileTable item BASE**|僅供內部使用。|
|**Time per file I/O request BASE**|僅供內部使用。|
|**Time per file I/O response BASE**|僅供內部使用。|
|**Time rename FileTable item BASE**|僅供內部使用。|
|**Time to get FileTable item BASE**|僅供內部使用。|
|**Time update FileTable item BASE**|僅供內部使用。| 
 
## <a name="see-also"></a>另請參閱  
[監視資源使用狀況 (系統監視器)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
