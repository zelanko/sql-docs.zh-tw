---
title: SQL Server、HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6ce8040b37ec08c82b11c9ff572c13125064523b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70155783"
---
# <a name="sql-server-http-storage"></a>SQL Server、HTTP 儲存體
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:HTTP Storage** 效能物件包含監視 Microsoft Azure 儲存體帳戶的效能計數器。 您可以使用 [Microsoft Azure 中的 SQL Server 資料檔案](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)功能，在 Azure 儲存體 Blob 中儲存資料庫檔案。 這個效能物件將每個 Azure 儲存體帳戶視為不同的磁碟機。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**平均Bytes/Read**|每次讀取時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**平均Bytes/Transfer**|讀取或寫入作業期間傳輸自 HTTP 儲存體的平均位元組數目。|  
|**平均Bytes/Write**|每次寫入時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**Avg. microsec/Read**|每次讀取自 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Read Comp**|HTTP 完成讀取儲存體所花費的平均毫秒數。| 
|**Avg. microsec/Transfer**|每次傳輸至 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Write**|每次寫入 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Write Comp**|HTTP 完成寫入儲存體所花費的平均毫秒數。|  
|**HTTP Storage IO failed/sec**|每秒傳送至 HTTP 儲存體的失敗寫入要求數目。| 
|**HTTP Storage I/O retry/sec**|每秒傳送至 HTTP 儲存體的重試要求數目。|  
|**Outstanding HTTP Storage I/O**|目標是 HTTP 儲存體的未完成 I/O 總數。|  
|**Read Bytes/sec**|讀取作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**讀取次數/秒**|HTTP 儲存體的每秒讀取次數。|  
|**Total Bytes/sec**|讀取或寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**Transfers/sec**|HTTP 儲存體的每秒讀取和寫入作業數目。|  
|**Write Bytes/sec**|寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**寫入次數/秒**|HTTP 儲存體的每秒寫入次數。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
