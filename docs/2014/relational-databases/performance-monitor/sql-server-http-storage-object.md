---
title: SQL Server、HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f104f7a6395442484be15f1e72c849edbf11e74f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70152683"
---
# <a name="sql-server-http_storage_object"></a>SQL Server：HTTP_STORAGE_OBJECT
  **SQLServer： HTTP_STORAGE_OBJECT**效能物件包含監視 Azure 儲存體帳戶的效能計數器。 使用[Azure 功能中 SQL Server 資料檔案](../databases/sql-server-data-files-in-microsoft-azure.md)，您可以將資料庫檔案儲存在 Azure 儲存體 blob 中。 這個效能物件將每個 Azure 儲存體帳戶視為不同的磁碟機。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**讀取位元組/秒**|讀取作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**寫入位元組/秒**|寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**位元組總數/秒**|讀取或寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**讀取/秒**|HTTP 儲存體的每秒讀取次數。|  
|**寫入數/秒**|HTTP 儲存體的每秒寫入次數。|  
|**傳輸/秒**|HTTP 儲存體的每秒讀取和寫入作業數目。|  
|**平均位元組/讀取**|每次讀取時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**平均位元組/寫入**|每次寫入時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**平均位元組/傳送**|讀取或寫入作業期間傳輸自 HTTP 儲存體的平均位元組數目。|  
|**Avg. microsec/Read**|每次讀取自 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Write**|每次寫入 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Transfer**|每次傳輸至 HTTP 儲存體所花費的平均微秒數目。|  
|**未處理的 HTTP 儲存體 i/o**|目標是 HTTP 儲存體的未完成 I/O 總數。|  
|**HTTP 儲存體 i/o 重試/秒**|每秒傳送至 HTTP 儲存體的重試要求數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
