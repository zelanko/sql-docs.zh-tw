---
title: 資料庫鏡像：互通性與共存性
description: 了解 SQL Server 資料庫鏡像與其他 SQL Server 功能之間的互通性和共存性，這些功能包括全文檢索目錄和資料庫快照集。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b70007c2beaa26d93107f167013a240fe0fa5864
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751912"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>資料庫鏡像：互通性與共存性 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
  
