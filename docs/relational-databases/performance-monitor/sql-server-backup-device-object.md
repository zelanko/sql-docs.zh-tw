---
title: SQL Server 的 Backup Device 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17d029490d00ac4ef3df58a83deeb4360e7e4bdf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-backup-device-object"></a>SQL Server 的 Backup Device 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **Backup Device** 物件提供計數器來監視備份與還原作業所使用的 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份裝置。 藉由監視備份裝置，即可決定產能，或每個裝置的備份與還原作業的進度與效能。 若要監視整個資料庫備份或還原作業的輸送量，請使用 **之** Databases [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Databases** object. 如需詳細資訊，請參閱 [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md)。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** 計數器。  
  
|SQL Server Backup Device 計數器|描述|  
|---------------------------------------|-----------------|  
|**Device Throughput Bytes/sec**|備份或還原資料庫時，所使用備份裝置的讀取與寫入作業輸送量 (位元組/秒)。 只有在備份或還原作業執行時，才會出現此計數器。|  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
