---
title: SQL Server XTP 儲存體 | Microsoft Docs
description: 了解 SQL Server XTP Storage 效能物件，其中包含與 SQL Server 中記憶體內部 OLTP 磁碟儲存相關的計數器。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: a12431a679ddbe4f47697b181c81ed3b7b3f08f3
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505462"
---
# <a name="sql-server-xtp-storage"></a>SQL Server XTP 儲存體
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL Server XTP Storage 效能物件包含與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中記憶體內部 OLTP 磁碟儲存相關的計數器。  
  
 下表描述 **SQL Server XTP Storage** 計數器。  
  
|計數器|描述|  
|-------------|-----------------|  
|**Checkpoints Closed**|線上代理程式已關閉的檢查點計數。|  
|**Checkpoints Completed**|離線檢查點執行緒已處理的檢查點計數。|  
|**Core Merges Completed**|合併工作者執行緒已完成的核心合併數目。 這些合併仍然需要予以安裝。|  
|**Merge Policy Evaluations**|自伺服器啟動後的合併原則評估數目。|  
|**Merge Requests Outstanding**|自伺服器啟動後之未處理的合併要求數目。|  
|**Merges Abandoned**|由於失敗而放棄的合併數目。|  
|**Merges Installed**|已成功安裝的合併數目。|  
|**Total Files Merged**|已合併的來源檔案總數。 此計數可用來尋找合併中的平均來源檔案數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server XTP &#40;記憶體內部 OLTP&#41; 效能計數器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
