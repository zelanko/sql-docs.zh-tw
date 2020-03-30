---
title: 高可用性 - 記憶體內部 OLTP 資料庫
ms.custom: seo-dt-2019
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dd467c8f6d942f53dade5ec6bb7d46ae9f39bdd9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412665"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>記憶體內部 OLTP 資料庫的高可用性支援
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  不論是否具有原生編譯的預存程序，包含記憶體最佳化資料表的資料庫皆可完整支援 AlwaysOn 可用性群組。  設定中並沒有任何差異，但與不含的情況相比，包含原生編譯的預存程序還支援包含 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 物件的資料庫。  
  
 在 AlwaysOn 可用性群組組態中部署記憶體內部 OLTP 資料庫時，主要複本上記憶體最佳化資料表的變更會以記憶體內部方式套用至次要複本上的資料表 (套用 REDO 時)。 這表示容錯移轉至次要複本可能會非常快速，因為資料已在記憶體中。 此外，資料表可供已設定讀取權限之次要複本上的查詢使用。  
  
## <a name="always-on-availability-groups-and-in-memory-oltp-databases"></a>AlwaysOn 可用性群組和記憶體內部 OLTP 資料庫  
 利用 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 元件設定資料庫提供了下列好處：  
  
-   **完全整合的體驗**   
    您可以使用同樣支援同步和非同步次要複本的相同精靈，設定包含記憶體最佳化資料表的資料庫。 此外，還可以使用 SQL Server Management Studio 中熟悉的 AlwaysOn 儀表板提供健全狀況監視。  
  
-   **可比較的容錯移轉時間**   
    次要複本可維護持久性記憶體最佳化資料表的記憶體內部狀態。 在自動或強制容錯移轉的情況下，由於不需要進行復原，容錯移轉至新主要複本的時間會相當於容錯移轉至磁碟基底資料表。 這項設定支援建立為 SCHEMA_ONLY 的記憶體最佳化資料表。 不過，系統不會記錄這些資料表的變更，因此次要複本上的這些資料表中不會有資料。  
  
-   **可讀取次要**   
    您可以存取與查詢次要複本上的記憶體最佳化資料表 (如果它已設定讀取權限)。 在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]中，次要複本上的讀取時間戳記與主要複本上的讀取時間戳記接近同步，這表示主要複本上的變更很快會顯示在次要複本上。 此接近同步的行為與 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 記憶體內部 OLTP 不同。  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>容錯移轉叢集執行個體 (FCI) 和記憶體內部 OLTP 資料庫  
 若要達到共用儲存體設定的高可用性，您可以設定執行個體與一個或多個具有記憶體最佳化資料表之資料庫的容錯移轉叢集。 在設定 FCI 的過程中，您必須考慮下列因素。  
  
-   **復原時間目標**   
    由於記憶體最佳化的資料表必須先載入到記憶體才能使用資料庫，因此會有較高的容錯移轉時間。  
  
-   **SCHEMA_ONLY 資料表**   
    請注意，在容錯移轉之後，SCHEMA_ONLY 資料表將會是空的，沒有任何資料列。 這是由應用程式進行設計與定義。 這種行為與您重新啟動具有一或多個 SCHEMA_ONLY 資料表的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫完全相同。  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>支援記憶體內部 OLTP 的異動複寫  
 做為異動複寫訂閱者的資料表 (不包括點對點異動複寫) 可以設定為記憶體最佳化資料表。 其他複寫組態與記憶體最佳化資料表不相容。  如需詳細資訊，請參閱 [複寫至記憶體最佳化資料表訂閱者](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)。  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [使用中次要：可讀取的次要複本 (AlwaysOn 可用性群組)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [複寫至記憶體最佳化資料表訂閱者](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
