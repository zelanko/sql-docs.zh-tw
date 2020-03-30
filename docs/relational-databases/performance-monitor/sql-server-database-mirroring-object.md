---
title: SQL Server 的 Database Mirroring 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Database Mirroring
- database mirroring [SQL Server], performance counters
- performance counters [SQL Server], database mirroring
- Database Mirroring object
ms.assetid: a27b51ee-7637-4525-9424-bcc16947dc13
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 639d661dd9a7196119bbb34f11f0ed5a9161a978
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67986674"
---
# <a name="sql-server-database-mirroring-object"></a>SQL Server 的 Database Mirroring 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:Database Mirroring** 效能物件含有效能計數器，可報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫鏡像的相關資訊。 下表列出這個物件包含的計數器。  
  
|名稱|描述|  
|----------|-----------------|  
|**Bytes Received/sec**|每秒接收的位元組數目。|  
|**Bytes Sent/sec**|每秒傳送的位元組數目。|  
|**Log Bytes Received/sec**|每秒接收的記錄位元組數目。|  
|**Log Bytes Redone from Cache/sec**|上一秒從鏡像記錄快取中取得的重做記錄位元組數目。<br /><br /> 這個計數器只會用於鏡像伺服器。 在主體伺服器上，這個值一定是 0。|  
|**Log Bytes Sent from Cache/sec**|上一秒從鏡像記錄快取中取得的傳送記錄位元組數目。<br /><br /> 這個計數器只會用於主體伺服器。 在鏡像伺服器上，這個值一定是 0。|  
|**Log Bytes Sent/sec**|每秒傳送的記錄位元組數目。|  
|**Log Compressed Bytes Rcvd/sec**|上一秒接收的壓縮記錄位元組數目。|  
|**Log Compressed Bytes Sent/sec**|上一秒傳送的壓縮記錄位元組數目。|  
|**Log Harden Time (ms)**|上一秒等候將記錄區塊強行寫入磁碟的毫秒數。|  
|**Log Remaining for Undo KB**|新的鏡像伺服器在容錯移轉之後仍然要掃描的記錄 KB 總數。<br /><br /> 這個計數器只會在恢復階段用於鏡像伺服器。 當恢復階段完成之後，此計數器會重設為 0。 在主體伺服器上，這個值一定是 0。|  
|**Log Scanned for Undo KB**|新的鏡像伺服器在容錯移轉之後已經掃描的記錄 KB 總數。<br /><br /> 這個計數器只會在恢復階段用於鏡像伺服器。 當恢復階段完成之後，此計數器會重設為 0。 在主體伺服器上，這個值一定是 0。|  
|**Log Send Flow Control Time (ms)**|上一秒記錄資料流訊息等候傳送流量控制的毫秒數。<br /><br /> 將記錄資料和中繼資料傳送給鏡像夥伴伺服器是資料庫鏡像中需要最大量資料的作業，而且可能會獨佔資料庫鏡像和 Service Broker 傳送緩衝區。 使用此計數器可監視資料庫鏡像工作階段對於這個緩衝區的使用。|  
|**Log Send Queue KB**|尚未傳送到鏡像伺服器之記錄的 KB 總數。|  
|**Mirrored Write Transactions/sec**|上一秒寫入鏡像資料庫，並等候記錄傳送到鏡像端進行認可的交易數目。<br /><br /> 只有當主體伺服器主動傳送記錄檔記錄到鏡像伺服器時，這個計數器才會遞增。|  
|**Pages Sent/sec**|每秒傳送的頁數。|  
|**Receives/sec**|每秒接收的鏡像訊息數目。|  
|**Redo Bytes/sec**|每秒在鏡像資料庫向前復原的記錄位元組數目。|  
|**Redo Queue KB**|目前仍套用到鏡像資料庫以便向前復原的強化記錄 KB 總數。 這是從鏡像端傳送到主體端。|  
|**Send/Receive Ack Time**|訊息在上一秒等候來自夥伴之收條的毫秒數。<br /><br /> 這個計數器對於排解可能由網路瓶頸造成的問題很有幫助，例如無法解釋的容錯移轉、大型傳送佇列或高度交易延遲等問題。 在這類情況下，您可以分析此計數器的值，以判斷網路是否發生問題。|  
|**Sends/sec**|每秒傳送的鏡像訊息數目。|  
|**Transaction Delay**|等候未終止之認可收條的延遲時間。|  
  
> [!NOTE]  
>  在每一個夥伴伺服器上，有些計數器會顯示零值，這是依據夥伴伺服器目前正在執行的角色而定。  
  
## <a name="remarks"></a>備註  
 效能計數器可讓您監視資料庫鏡像效能。 例如，您可以檢查 **[Transaction Delay]** 計數器，以查看資料庫鏡像是否影響主體伺服器的效能；您可以檢查 **[Redo Queue]** 與 **[Log Send Queue]** 計數器，以查看鏡像資料庫是否跟得上主體資料庫。 您可以檢查 [Log Bytes Sent/sec]  計數器，以監視每秒傳送的記錄量。  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
