---
title: AlwaysOn 可用性群組 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: a1591695b5676e4c37e7cd2a38b6c95c3a84ef75
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037294"
---
# <a name="always-on-availability-groups-sql-server"></a>AlwaysOn 可用性群組 (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 功能是提供資料庫鏡像之企業級替代方案的高可用性與災害復原解決方案。 在 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]中導入的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可讓企業將一組使用者資料庫的可用性提高到最大程度。 *「可用性群組」* (Availability Group) 支援一組可一起容錯移轉之離散化使用者資料庫的容錯移轉環境，也就是所謂的 *「可用性資料庫」*(Availability Database)。 可用性群組支援一組讀寫的主要資料庫，以及一到八組對應的次要資料庫。 此外，您可以將次要資料庫用於唯讀存取及/或某些備份作業。  
  
 可用性群組會在可用性複本層級容錯移轉。 容錯移轉不是因資料庫問題 (例如資料庫因為資料檔案遺失而變得可疑、資料庫刪除或交易記錄損毀) 而造成的。  
  
  
##  <a name="Benefits"></a> 優點  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 提供了一組豐富的選項，可改善資料庫可用性並實現改善的資源使用方式。 關鍵元件如下：  
  
-   最多支援九個可用性複本。 *「可用性複本」* (Availability Replica) 是特定 SQL Server 執行個體所裝載之可用性群組的具現化，其中維護屬於可用性群組之每個可用性資料庫的本機複本。 每個可用性群組都支援一個主要複本和最多八個次要複本。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)。  
  
    > [!IMPORTANT]  
    >  每個可用性複本都必須位在單一 Windows Server 容錯移轉叢集 (WSFC) 叢集的不同節點。 如需有關必要條件、 限制和建議的可用性群組的詳細資訊，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組。SQL Server;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   支援替代可用性模式，如下所示：  
  
    -   非同步認可模式。 這種可用性模式是一種當可用性複本分散距離相當遠時仍可正常運作的災害復原方案。  
  
    -   同步認可模式。 這種可用性模式強調的是高可用性和資料保護而非效能，但是相對地增加了交易延遲。 給定的可用性群組最多可支援三個同步認可的可用性複本，包括目前的主要複本。  
  
     如需詳細資訊，請參閱[可用性模式。Alwayson 可用性群組。](availability-modes-always-on-availability-groups.md).  
  
-   支援許多可用性群組容錯移轉形式：自動容錯移轉、規劃的手動容錯移轉 (通常只稱為「手動容錯移轉」)，以及強制手動容錯移轉 (通常只稱為「強制容錯移轉」)。 如需詳細資訊，請參閱[容錯移轉及容錯移轉模式。Alwayson 可用性群組。](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   可讓您將給定的可用性複本設定為支援下列其中一種或兩種使用中次要功能：  
  
    -   唯讀連接存取，讓複本的唯讀連接能夠在以次要複本的方式執行時存取並讀取其資料庫。 如需詳細資訊，請參閱[使用中次要： 可讀取的次要複本。Alwayson 可用性群組](https://msdn.microsoft.com/library/ff878253.aspx))。  
  
    -   以次要複本的方式執行時，針對其資料庫執行備份作業。 如需詳細資訊，請參閱[使用中次要： 在次要複本上備份](https://msdn.microsoft.com/library/ff878253.aspx))。  
  
     利用使用中次要功能可透過更善用次要硬體資源，改善 IT 效率並降低成本。 此外，透過將讀取意圖應用程式和備份作業卸載至次要複本，有助於提高主要複本的效能。  
  
-   支援每個可用性群組的可用性群組接聽程式。 *「可用性群組接聽程式」* (Availability Group Listener) 是用戶端可連接的伺服器名稱，以便存取 AlwaysOn 可用性群組之主要或次要複本中的資料庫。 可用性群組接聽程式會將內送連接導向至主要複本或唯讀次要複本。 接聽程式會在可用性群組容錯移轉之後提供快速應用程式容錯移轉。 如需詳細資訊，請參閱[可用性群組接聽程式、 用戶端連接性及應用程式容錯移轉。SQL Server;](../../listeners-client-connectivity-application-failover.md).  
  
-   支援彈性容錯移轉原則，以便有效控制可用性群組容錯移轉。 如需詳細資訊，請參閱[容錯移轉及容錯移轉模式。Alwayson 可用性群組。](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   支援防止頁面損毀的自動頁面修復。 如需詳細資訊，請參閱[自動修復頁面&#40;的可用性群組和資料庫鏡像;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)。  
  
-   支援加密和壓縮，可提供安全且高效能的傳輸方式。  
  
-   提供一組整合式工具，可簡化可用性群組的部署和管理作業，包括：  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] DDL 陳述式。 如需詳細資訊，請參閱[概觀的 TRANSACT-SQL 陳述式的 Alwayson 可用性群組。SQL Server;](transact-sql-statements-for-always-on-availability-groups.md).  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 工具，如下所示：  
  
        -   [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 會建立及設定可用性群組。 在某些環境中，此精靈還可以自動準備次要資料庫並且為每個資料庫啟動資料同步處理。 如需詳細資訊，請參閱[使用新的可用性群組 對話方塊。SQL Server Management Studio;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md).  
  
        -   [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]會將一個或多個主要資料庫加入至現有可用性群組。 在某些環境中，此精靈還可以自動準備次要資料庫並且為每個資料庫啟動資料同步處理。 如需詳細資訊，請參閱 [使用將資料庫加入至可用性群組精靈 (SQL Server)](availability-group-add-database-to-group-wizard.md)。  
  
        -   [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] 會將一個或多個次要複本加入至現有可用性群組。 在某些環境中，此精靈還可以自動準備次要資料庫並且為每個資料庫啟動資料同步處理。 如需詳細資訊，請參閱[使用將複本加入至可用性群組精靈。SQL Server Management Studio;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
        -   [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]會起始可用性群組的手動容錯移轉。 根據您指定為容錯移轉目標之次要複本的組態和狀態，此精靈可以執行規劃的手動容錯移轉或強制手動容錯移轉。 如需詳細資訊，請參閱[使用容錯移轉可用性群組精靈。SQL Server Management Studio;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
    -   [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)]監視 AlwaysOn 可用性群組、 可用性複本和可用性資料庫，以及評估 AlwaysOn 原則的結果。 如需詳細資訊，請參閱[使用 AlwaysOn 儀表板中;SQL Server Management Studio;](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
    -   [物件總管詳細資料] 窗格會顯示現有可用性群組的基本資訊。 如需詳細資訊，請參閱[使用物件總管詳細資料監視可用性群組。SQL Server Management Studio;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   PowerShell 指令程式。 如需詳細資訊，請參閱[的 PowerShell Cmdlet 概觀 Alwayson 可用性群組。SQL Server;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md).  
  
##  <a name="TermsAndDefinitions"></a> 詞彙和定義  
 可用性群組  
 一組一起容錯移轉之資料庫 (「可用性資料庫」) 的容器。  
  
 可用性資料庫  
 屬於可用性群組的資料庫。 對於每個可用性資料庫而言，可用性群組會維護單一讀寫複本 (「主要資料庫」) 以及一到八個唯讀複本 (「次要資料庫」)。  
  
 主要資料庫  
 可用性資料庫的讀寫複本。  
  
 次要資料庫  
 可用性資料庫的唯讀複本。  
  
 「可用性複本」  
 特定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體所裝載之可用性群組的具現化，它會維護屬於可用性群組之每個可用性資料庫的本機副本。 有兩種類型的可用性複本存在：單一 *「主要複本」* 以及一到八個 *「次要複本」*。  
  
 「主要複本」  
 可用性複本，該複本可讓主要資料庫用於用戶端的讀寫連接，同時也將每個主要資料庫的交易記錄檔記錄傳送到每個次要複本。  
  
 次要複本  
 可用性複本，該複本會維護每個可用性資料庫的次要副本，並且當做可用性群組的潛在容錯移轉目標。 (選擇性) 可支援以唯讀方式存取次要資料庫的次要複本，可以支援在次要資料庫上建立備份。  
  
 可用性群組接聽程式  
 用戶端可連接的伺服器名稱，以便存取 AlwaysOn 可用性群組之主要或次要複本中的資料庫。 可用性群組接聽程式會將內送連接導向至主要複本或唯讀次要複本。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱[AlwaysOn 可用性群組概觀;SQL Server;](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="Interoperability"></a> 與其他 Database Engine 功能的互通性和共存性  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 可搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的下列功能或元件使用：  
  
-   [關於異動資料擷取。SQL Server;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [關於變更追蹤。SQL Server;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [自主資料庫](../../../relational-databases/databases/contained-databases.md)  
  
-   [資料庫加密](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [資料庫快照集](database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [記錄傳送](../../log-shipping/about-log-shipping-sql-server.md)  
  
-   [遠端 Blob 存放區 (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [複寫](../../install-windows/install-sql-server-replication.md)  
  
-   [Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server Agent](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  如需有關限制和使用其他功能搭配的限制資訊[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[Always On 可用性群組： 互通性。SQL Server;](always-on-availability-groups-interoperability-sql-server.md).  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [開始使用 Alwayson 可用性群組。SQL Server;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [SQL Server Alwayson 團隊部落格： 官方 SQL Server AlwaysOn 團隊部落格](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](http://blogs.msdn.com/b/psssql/)  
  
-   **影片：**  
  
     [Microsoft SQL Server Code-Named "Denali" AlwaysOn Series,Part 1: Introducing the Next Generation High Availability Solution (Microsoft SQL Server 代碼 "Denali" AlwaysOn 系列第一部分：新一代高可用性解決方案簡介)](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named"Denali"Alwayson 系列第 2 部： 建立使用 AlwaysOn 關鍵任務的高可用性解決方案](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮書：**  
  
     [Microsoft SQL Server AlwaysOn 高可用性和災害復原方案指南](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組; 概觀SQL Server;](overview-of-always-on-availability-groups-sql-server.md)   
 [必要條件、 限制和建議的 AlwaysOn 可用性群組&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [設定 Alwayson 可用性群組; 的伺服器執行個體SQL Server;](always-on-availability-groups-sql-server.md)   
 [建立及設定可用性群組。SQL Server;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [可用性群組; 的管理SQL Server;](administration-of-an-availability-group-sql-server.md)   
 [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [針對 Alwayson 可用性群組; 的 TRANSACT-SQL 陳述式的概觀SQL Server;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性群組; PowerShell Cmdlet 概觀SQL Server;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  