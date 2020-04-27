---
title: 記憶體內部 OLTP 資料庫的高可用性支援 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 37c719beb625a533c2d8f279a8500365c4786c05
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62990578"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>記憶體內部 OLTP 資料庫的高可用性支援
  不論包含或不含原生編譯的預存程序，包含記憶體最佳化資料表的資料庫完全支援 AlwaysOn 可用性群組。  設定中並沒有任何差異，但與不含的情況相比，包含原生編譯的預存程序還支援包含 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 物件的資料庫。  
  
## <a name="alwayson-availability-groups-and-in-memory-oltp-databases"></a>AlwaysOn 可用性群組和記憶體內部 OLTP 資料庫  
 利用 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 元件設定資料庫提供了下列好處：  
  
-   **完全整合的體驗**   
    您可以使用同樣支援同步和非同步次要複本的相同精靈，設定包含記憶體最佳化資料表的資料庫。 此外，還可以使用 SQL Server Management Studio 中熟悉的 AlwaysOn 儀表板提供健全狀況監視。  
  
-   **可比較的容錯移轉時間**   
    次要複本可維護持久性記憶體最佳化資料表的記憶體內部狀態。 在自動或強制容錯移轉的情況下，由於不需要進行復原，容錯移轉至新主要複本的時間會相當於容錯移轉至磁碟基底資料表。 這項設定支援建立為 SCHEMA_ONLY 的記憶體最佳化資料表。 不過，系統不會記錄這些資料表的變更，因此次要複本上的這些資料表中不會有資料。  
  
-   **可讀取次要**   
    您可以存取與查詢次要複本上的記憶體最佳化資料表 (如果它已設定讀取權限)。 如需詳細資訊，請參閱[使用中次要：可讀取的次要複本 (AlwaysOn 可用性群組)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>容錯移轉叢集執行個體 (FCI) 和記憶體內部 OLTP 資料庫  
 若要達到共用儲存體設定的高可用性，您可以設定執行個體與一個或多個具有記憶體最佳化資料表之資料庫的容錯移轉叢集。 在設定 FCI 的過程中，您必須考慮下列因素。  
  
-   **復原時間目標**   
    由於記憶體最佳化的資料表必須先載入到記憶體才能使用資料庫，因此會有較高的容錯移轉時間。  
  
-   **SCHEMA_ONLY 資料表**   
    請注意，在容錯移轉之後，SCHEMA_ONLY 資料表將會是空的，沒有任何資料列。 這是由應用程式進行設計與定義。 這種行為與您重新啟動具有一或多個 SCHEMA_ONLY 資料表的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫完全相同。  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>支援記憶體內部 OLTP 的異動複寫  
 做為異動複寫訂閱者的資料表 (不包括點對點異動複寫) 可以設定為記憶體最佳化資料表。 其他複寫組態與記憶體最佳化資料表不相容。  如需詳細資訊，請參閱複寫[至記憶體優化資料表訂閱者](../replication/replication-to-memory-optimized-table-subscribers.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組（SQL Server）](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用中次要：可讀取的次要複本 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [複寫至記憶體最佳化資料表訂閱者](../replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
