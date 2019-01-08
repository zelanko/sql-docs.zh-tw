---
title: 建立及設定可用性群組 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], creating
ms.assetid: 7f89fab8-6ee2-4273-9de0-e594bfb9407f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14dea0c618f754024a18ca24d64b98b08aa99f64
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368920"
---
# <a name="creation-and-configuration-of-availability-groups-sql-server"></a>建立及設定可用性群組 (SQL Server)
  本章節的主題將說明如何在位於單一 WSFC 容錯移轉叢集內不同 Windows Server 容錯移轉叢集 (WSFC) 節點上的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體上部署 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 實作。  
  
 建立第一個可用性群組之前，我們建議您先熟悉下列主題中的資訊：  
  
 [必要條件、 限制和建議，AlwaysOn 可用性群組的&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
 此主題描述電腦、WSFC 節點、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體、可用性群組、複本和資料庫的必要條件、限制和建議。 此主題也包含安全性考量的資訊。  
  
 [開始使用 AlwaysOn 可用性群組&#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
 包含下列作業的步驟資訊：設定伺服器執行個體、建立可用性群組、設定用戶端連接的可用性群組、管理可用性群組，以及監視可用性群組。  
  
 
  
##  <a name="RelatedTasks"></a> 相關工作  
 **為 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]**  
  
-   [啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [建立資料庫鏡像 AlwaysOn 可用性群組的&#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [建立 Windows 驗證的資料庫鏡像端點 &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [允許資料庫鏡像端點使用輸出連線的憑證 &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
 **若要開始設定 AlwaysOn 可用性群組**  
  
-   [開始使用 AlwaysOn 可用性群組&#40;SQL Server&#41;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
 **建立並設定新的可用性群組**  
  
-   [使用可用性群組精靈 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [建立可用性群組 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
-   [建立可用性群組 &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [在新增或修改可用性複本時指定端點 URL &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [設定彈性容錯移轉原則以控制自動容錯移轉 （AlwaysOn 可用性群組） 的條件](configure-flexible-automatic-failover-policy.md)  
  
-   [設定可用性複本的備份 &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [設定可用性複本的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [設定可用性群組的唯讀路由 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [將次要複本聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [於 AlwaysOn 次要資料庫啟動資料移動&#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [將次要資料庫聯結至可用性群組 &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [管理可用性群組之資料庫的登入及工作 &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)  
  
 **若要疑難排解**  
  
-   [疑難排解 AlwaysOn 可用性群組組態 (SQL Server) 刪除](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [疑難排解失敗的加入檔案作業&#40;AlwaysOn 可用性群組&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [AlwaysON-HADRON 學習系列：Worker Pool Usage for HADRON 功能之資料庫](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](https://blogs.msdn.com/b/psssql/)  
  
-   **影片：**  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 1 部分：下一代高可用性解決方案簡介](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named"Denali"AlwaysOn 系列，第 2 部分：建立使用 AlwaysOn 任務關鍵性的高可用性解決方案](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **白皮書：**  
  
     [Microsoft SQL Server AlwaysOn 解決方案指南高可用性和災害復原](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Microsoft 的 SQL Server 2012 白皮書](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客戶諮詢團隊白皮書](http://sqlcat.com/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性群組的管理 &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [與 AlwaysOn 可用性群組 (SQL Server) 的操作問題適用的 AlwaysOn 原則](always-on-policies-for-operational-issues-always-on-availability.md)   
 [監視可用性群組 &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組：互通性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)  
  
  
