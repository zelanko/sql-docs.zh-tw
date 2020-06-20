---
title: SQL Server 的 Backup Device 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e3126310ad31dcc153fc79508dbfaccf86f5da78
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016995"
---
# <a name="sql-server-backup-device-object"></a>SQL Server 的 Backup Device 物件
  **Backup Device** 物件提供計數器來監視備份與還原作業所使用的 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份裝置。 藉由監視備份裝置，即可決定產能，或每個裝置的備份與還原作業的進度與效能。 若要監視整個資料庫備份或還原作業的輸送量，請使用  Databases[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件的 **Backup/Restore Throughput/sec** 計數器。 如需詳細資訊，請參閱 [SQL Server, Databases Object](sql-server-databases-object.md)。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Backup Device** 計數器。  
  
|SQL Server Backup Device 計數器|描述|  
|---------------------------------------|-----------------|  
|**Device Throughput Bytes/sec**|備份或還原資料庫時，所使用備份裝置的讀取與寫入作業輸送量 (位元組/秒)。 只有在備份或還原作業執行時，才會出現此計數器。|  
  
## <a name="see-also"></a>另請參閱  
 [備份裝置 &#40;SQL Server&#41;](../backup-restore/backup-devices-sql-server.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
