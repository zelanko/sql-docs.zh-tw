---
title: 資料庫鏡像：互通性與共存性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- high availability [SQL Server], interoperability and coexistence
- Database Engine [SQL Server], high availability
ms.assetid: 89fef397-e0cf-4e08-b598-25b8d4170523
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ba2e5af89a4a9eabb420e0d75a8a90b4ef48540
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136693"
---
# <a name="database-mirroring-interoperability-and-coexistence-sql-server"></a>資料庫鏡像：互通性與共存性 (SQL Server)
  資料庫鏡像可與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的下列功能或元件搭配使用：  
  
-   [AlwaysOn 容錯移轉叢集執行個體 （SQL Server 容錯移轉叢集）](database-mirroring-and-sql-server-failover-cluster-instances.md)  
  
-   [異動資料擷取與變更追蹤](../../relational-databases/track-changes/change-data-capture-and-other-sql-server-features.md)  
  
-   [資料庫快照集](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
-   [全文檢索目錄](database-mirroring-and-full-text-catalogs-sql-server.md)  
  
-   [記錄傳送](database-mirroring-and-log-shipping-sql-server.md)  
  
-   [複寫](database-mirroring-and-replication-sql-server.md)  
  
 資料庫鏡像不會與下列項目交互操作：  
  
-   跨資料庫交易/分散式交易  
  
     如需這類交易不受支援之原因的相關資訊，請參閱[資料庫鏡像或 AlwaysOn 可用性群組不支援跨資料庫交易 &#40;SQL Server&#41;](../availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)。  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  