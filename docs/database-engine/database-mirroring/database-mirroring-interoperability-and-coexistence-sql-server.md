---
title: 資料庫鏡像：互通性與共存性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc1edc91226f5b8d20e982c9b1234f32db5cee44
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>資料庫鏡像：互通性與共存性 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  資料庫鏡像可與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的下列功能或元件搭配使用：  
  
-   [AlwaysOn 容錯移轉叢集執行個體 (SQL Server 容錯移轉叢集)](../../database-engine/database-mirroring/database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [異動資料擷取與變更追蹤](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [資料庫快照集](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
-   [全文檢索目錄](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [記錄傳送](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)  
  
-   [複寫](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)  
  
 資料庫鏡像不會與下列項目交互操作：  
  
-   跨資料庫交易/分散式交易  
  
     如需這類交易不受支援之原因的相關資訊，請參閱 [AlwaysOn 可用性群組和資料庫鏡像的跨資料庫交易和分散式交易 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)。  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
