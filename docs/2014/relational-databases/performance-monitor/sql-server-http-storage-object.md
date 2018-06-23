---
title: SQL Server、HTTP_STORAGE_OBJECT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ae849f79-c581-42a5-a5cc-0a9ebea171b9
caps.latest.revision: 4
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 84ba27202f0a1d95810d80d474b9db91dfa4201a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145837"
---
# <a name="sql-server-httpstorageobject"></a>SQL Server：HTTP_STORAGE_OBJECT
  **SQLServer:HTTP_STORAGE_OBJECT** 效能物件包含監視 Windows Azure 儲存體帳戶的效能計數器。 使用[Windows Azure 中的 SQL Server 資料檔案](../databases/sql-server-data-files-in-microsoft-azure.md)功能，您可以將資料庫檔案儲存在 Windows Azure 儲存體 Blob。 這個效能物件會將每個 Windows Azure 儲存體帳戶視為不同的磁碟機。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**Read Bytes/sec**|讀取作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**Write Bytes/sec**|寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**Total Bytes/sec**|讀取或寫入作業期間每秒傳輸自 HTTP 儲存體的資料量。|  
|**讀取次數/秒**|HTTP 儲存體的每秒讀取次數。|  
|**寫入次數/秒**|HTTP 儲存體的每秒寫入次數。|  
|**Transfers/sec**|HTTP 儲存體的每秒讀取和寫入作業數目。|  
|**平均Bytes/Read**|每次讀取時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**平均Bytes/Write**|每次寫入時傳輸自 HTTP 儲存體的平均位元組數目。|  
|**平均Bytes/Transfer**|讀取或寫入作業期間傳輸自 HTTP 儲存體的平均位元組數目。|  
|**Avg. microsec/Read**|每次讀取自 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Write**|每次寫入 HTTP 儲存體所花費的平均微秒數目。|  
|**Avg. microsec/Transfer**|每次傳輸至 HTTP 儲存體所花費的平均微秒數目。|  
|**Outstanding HTTP Storage I/O**|目標是 HTTP 儲存體的未完成 I/O 總數。|  
|**HTTP Storage I/O Retry/sec**|每秒傳送至 HTTP 儲存體的重試要求數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](monitor-resource-usage-system-monitor.md)  
  
  