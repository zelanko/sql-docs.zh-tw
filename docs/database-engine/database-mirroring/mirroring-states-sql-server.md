---
title: 鏡像狀態 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- PENDING_FAILOVER state
- mirroring states [SQL Server]
- DISCONNECTED state
- SYNCHRONIZING state
- SYNCHRONIZED state
- SUSPENDED state
- database mirroring [SQL Server], states
ms.assetid: 90062917-74f9-471b-b49e-bc153ae1a468
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: a73d25596d8815d773bdcdfcd0d1ee43d65340c7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795371"
---
# <a name="mirroring-states-sql-server"></a>鏡像狀態 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在資料庫鏡像工作階段期間，鏡像資料庫一定會處於特定狀態 (「鏡像狀態」  )。 資料庫的狀態會反映通訊狀態、資料流程，以及夥伴之間的資料差異。 資料庫鏡像工作階段會與主體資料庫採用相同的狀態。  
  
 在資料庫鏡像工作階段內，伺服器執行個體會彼此監視。 夥伴會使用鏡像狀態來監視資料庫。 除了 PENDING_FAILOVER 狀態之外，主體資料庫和鏡像資料庫永遠處於相同的狀態。 若為工作階段設定見證，則每部夥伴伺服器都會利用其連接狀態 (CONNECTED 或 DISCONNECTED) 來監視見證。  
  
 可能的資料庫鏡像狀態如下：  
  
|鏡像狀態|Description|  
|---------------------|-----------------|  
|SYNCHRONIZING|鏡像資料庫的內容落後於主體資料庫的內容。 主體伺服器將記錄檔記錄傳送至鏡像伺服器，將所做的變更套用到鏡像資料庫來向前復原。<br /><br /> 在資料庫鏡像工作階段開始時，資料庫處於 SYNCHRONIZING 狀態。 主體伺服器正為資料庫提供服務，而鏡像伺服器則試圖趕上。|  
|SYNCHRONIZED|當鏡像伺服器足以追趕上主體伺服器時，鏡像狀態就會變更為 SYNCHRONIZED。 只要主體伺服器繼續傳送變更到鏡像伺服器，而鏡像伺服器也繼續將變更套用到鏡像資料庫，資料庫便會保持在這種狀態。<br /><br /> 如果交易安全性設定為 FULL，SYNCHRONIZED 狀態將可同時支援自動容錯移轉和手動容錯移轉，而且容錯移轉之後不會遺失任何資料。<br /><br /> 如果關閉交易安全性，永遠都有可能遺失部分資料，即使是在 SYNCHRONIZED 狀態也是如此。|  
|SUSPENDED|無法使用資料庫的鏡像副本。 主體資料庫執行時並沒有傳送任何記錄檔到鏡像伺服器，這種狀況稱為「執行公開」  。 這是容錯移轉之後的狀態。<br /><br /> 工作階段也會因為重做錯誤或管理員暫停工作階段而變成 SUSPENDED。<br /><br /> SUSPENDED 是夥伴關機和啟動時仍然有效的永續性狀態。|  
|PENDING_FAILOVER|唯有開始進行容錯移轉之後但伺服器尚未轉換為鏡像角色之前，主體伺服器上才會出現此狀態。<br /><br /> 起始容錯移轉時，主體資料庫便會進入 PENDING_FAILOVER 狀態，迅速終止任何使用者連接，然後馬上接替鏡像角色。|  
|DISCONNECTED|夥伴已經與其他夥伴失去通訊。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)  
  
  
