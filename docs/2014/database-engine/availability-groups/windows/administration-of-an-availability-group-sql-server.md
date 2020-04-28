---
title: 可用性群組的管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], managing
ms.assetid: 0b7542fa-235e-413d-81bf-3eff9ee07480
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8d826201f44bb666050f5229b4824b5c2198dc0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75229000"
---
# <a name="administration-of-an-availability-group-sql-server"></a>可用性群組的管理 (SQL Server)
  在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中管理現有的 AlwaysOn 可用性群組包括下列一個或多個工作：  
  
-   改變現有可用性副本的屬性 (例如，變更用戶端連接存取 (以設定可讀取的次要副本))；變更其容錯移轉模式、可用性模式或工作階段逾時設定。  
  
-   加入或移除次要副本。  
  
-   加入或移除資料庫。  
  
-   暫停或恢復資料庫。  
  
-   執行已規劃的手動容錯移轉 ( *「手動容錯移轉」*(Manual Failover)) 或強制手動容錯移轉 ( *「強制容錯移轉」*(Forced Failover))。  
  
-   建立或設定可用性群組接聽程式。  
  
-   管理給定可用性群組之 [可讀取的次要複本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) 。 這項作業包括以次要角色執行時，將一個或多個複本設定為唯讀存取，以及設定唯讀路由。  
  
-   管理給定可用性群組之 [次要複本上的備份](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) 。 這項作業包括設定您希望執行備份作業的位置，然後編寫備份作業的指令碼以實作您的備份喜好設定。 您必須為裝載可用性複本的每一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上之可用性群組中的每一個資料庫，編寫備份作業的指令碼。  
  
-   刪除可用性群組。  
  
-   針對作業系統升級進行 AlwaysOn 可用性群組的跨叢集移轉  
  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
 **設定現有的可用性群組**  
  
-   [將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [將次要複本從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [將資料庫加入至可用性群組 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [將次要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [將主要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [設定彈性容錯移轉原則，以控制自動容錯移轉 &#40;AlwaysOn 可用性群組的條件&#41;](configure-flexible-automatic-failover-policy.md)  
  
 **管理可用性群組**  
  
-   [設定可用性複本的備份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [執行可用性群組的已規劃手動容錯移轉 &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [執行可用性群組的強制手動容錯移轉 &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [移除可用性群組 &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
  
 **管理可用性複本**  
  
-   [將次要複本加入至可用性群組 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [將次要複本聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [將次要複本從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [變更可用性複本的可用性模式 &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [變更可用性複本的容錯移轉模式 &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [設定可用性複本的備份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [設定可用性複本的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [設定可用性群組的唯讀路由 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [變更可用性複本的工作階段逾時期限 &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **管理可用性資料庫**  
  
-   [將資料庫加入至可用性群組 &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [將主要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [將次要資料庫從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [暫止可用性資料庫 &#40;SQL Server&#41;](suspend-an-availability-database-sql-server.md)  
  
-   [繼續可用性資料庫 &#40;SQL Server&#41;](resume-an-availability-database-sql-server.md)  
  
 **監視可用性群組**  
  
-   [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
 **若要支援將可用性群組移轉至新的 WSFC 叢集 (跨叢集移轉)**  
  
-   [變更伺服器執行個體的 HADR 叢集內容 &#40;SQL Server&#41;](change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
-   [讓可用性群組離線 &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](https://blogs.msdn.com/b/psssql/)  
  
-   **影片：**  
  
     [Microsoft SQL Server Code-Named "Denali" AlwaysOn 系列，第 1 部：新一代高可用性解決方案簡介](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali" AlwaysOn 系列，第 2 部：使用 AlwaysOn 建立關鍵任務的高可用性方案](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮書：**  
  
     [Microsoft 的 SQL Server 2012 白皮書](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客戶諮詢團隊白皮書](http://sqlcat.com/)  
  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [設定 AlwaysOn 可用性群組 &#40;SQL Server 的伺服器實例&#41;](configuration-of-a-server-instance-for-always-on-availability-groups-sql-server.md)  
 [建立及設定可用性群組 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [使用中次要：可讀取的次要複本 &#40;AlwaysOn 可用性群組&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [作用中次要資料庫：次要複本上的備份 &#40;AlwaysOn 可用性群組&#41;](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server 的操作問題 AlwaysOn 原則&#41;](always-on-policies-for-operational-issues-always-on-availability.md)   
 [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組：互通性 &#40;SQL Server&#41;](always-on-availability-groups-interoperability-sql-server.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;的 Transact-sql 語句總覽](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;的 PowerShell Cmdlet 總覽](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
