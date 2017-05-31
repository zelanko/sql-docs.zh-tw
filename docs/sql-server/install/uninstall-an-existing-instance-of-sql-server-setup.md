---
title: "解除安裝現有的 SQL Server 執行個體 (安裝程式) | Microsoft Docs"
ms.custom: 
ms.date: 01/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
caps.latest.revision: 74
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 548949bad71213430b987383fd221a91bddcfdff
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>解除安裝現有的 SQL Server 執行個體 (安裝程式)
  本文描述如何解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的獨立執行個體。 遵循本主題的步驟，也可以讓系統做好準備，以便可以重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
>**重要！** 若要解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體，您必須是本機管理員，且具有以服務登入的權限。  
  
> **注意：**若要解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所提供的「移除節點」功能來分別移除每個節點。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集 &#40;Setup&#41; 中加入或移除節點](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  
  
 請注意，解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請先考慮下列重要狀況：  
  
-   從實體記憶體數量為最小需求量的電腦中移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件前，必須先確定分頁檔案大小是充足的。 分頁檔案大小必須等於實體記憶體數量的兩倍。 虛擬記憶體不足可能會造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移除不完全。  
  
-   若有多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會在解除安裝最後一個 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體時自動解除安裝。  
  
     如果您想要解除安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的所有元件，您必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [控制台] **的** [程式和功能] **中，手動解除安裝**Browser 元件。  
  
1.  解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會刪除在安裝程序期間所新增的 tempdb 資料檔案。 如果系統資料庫目錄中有名稱模式為 tempdb_mssql_*.ndf 的檔案，則會刪除這些檔案。  
  
### <a name="before-you-uninstall"></a>解除安裝之前  
  
1.  **備份資料。** 雖然這並非必要步驟，不過您可能會擁有要以目前狀態儲存的資料庫， 也可能想要儲存先前對系統資料庫所做的變更。 若符合其中任一情況，請務必在解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前先行備份資料。 或者，您也可以將所有資料和記錄檔的複本儲存在 MSSQL 資料夾以外的資料夾中。 解除安裝期間將會刪除 MSSQL 資料夾。  
  
     您必須儲存的檔案包括下列資料庫檔案：  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   ReportServer[$InstanceName] 這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 預設資料庫。  
  
    -   ReportServer[$InstanceName]TempDB 這是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 預設暫存資料庫。  
  
2.  **刪除本機安全性群組。** 在解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請先刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的本機安全性群組。  
  
3.  **Stop all**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **services.** ：建議您在解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件之前，先停止所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的本機安全性群組。 使用中的連接可能會導致解除安裝無法順利完成。  
  
4.  **使用具有適當權限的帳戶。** 請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶或具有同等權限的帳戶登入伺服器。 例如，您可以使用本機管理員群組成員的帳戶登入伺服器。  
  
### <a name="to-uninstall-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>To Uninstall an Instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  若要開始解除安裝程序，請移至 **[控制台]** ，然後移至 **[程式和功能]**。  
  
2.  以滑鼠右鍵按一下 [SQL Server 2016]，然後選取 [解除安裝]。 然後按一下 **[移除]**。 這樣就會啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈。  
  
     安裝程式支援規則將會執行，以便驗證您的電腦組態。 若要繼續進行，請按 **[下一步]**。  
  
3.  在 [選取執行個體] 頁面上，使用下拉式方塊來指定要移除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或指定僅移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用功能和管理工具的選項。 若要繼續進行，請按 **[下一步]**。  
  
4.  在 [選取功能] 頁面上，指定要從指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中移除的功能。  
  
     移除規則將會執行，以便確認作業可以順利完成。  
  
5.  在 **[準備移除]** 頁面上，檢閱即將解除安裝之元件和功能的清單。 按一下 **[移除]** 開始解除安裝  
  
6.  解除安裝最後一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [程式和功能] **的程式清單中仍會顯示與**相關聯的其他程式。 不過，如果您關閉 **[程式和功能]**，下次再開啟 **[程式和功能]**時，就會重新整理程式清單，只顯示實際上仍安裝的程式。  
  
### <a name="if-the-uninstallation-fails"></a>如果解除安裝失敗  
  
1.  如果解除安裝程序未順利完成，請嘗試解決導致解除安裝失敗的問題。 下列文章可以幫助您了解解除安裝失敗的原因：  
  
    -   [如何在安裝記錄檔中識別 SQL Server 2008 的安裝問題](http://support.microsoft.com/kb/955396/en-us)  
  
    -   [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  如果無法修正解除安裝失敗的原因，您可以連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 支援部門。 在某些情況下，例如不小心刪除重要的檔案，可能需要先重新安裝作業系統，才能在電腦上重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  

