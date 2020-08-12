---
title: 解除安裝現有的執行個體
description: 本文描述如何解除安裝 SQL Server 的獨立執行個體，這也會準備系統，以便您隨時重新安裝 SQL Server。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fd4e3ee094bca1d27543a92a357f705b0e3d82fe
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883733"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>解除安裝現有的 SQL Server 執行個體 (安裝程式)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  本文描述如何解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的獨立執行個體。 遵循本文中的步驟時，您也可以讓系統做好重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的準備。  
  
 > [!NOTE]
 > 若要解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所提供的「移除節點」功能來分別移除每個節點。 如需詳細資訊，請參閱[在 SQL Server 容錯移轉叢集 &#40;Setup&#41; 中加入或移除節點](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)。  

## <a name="considerations"></a>考量

- 若要解除安裝 SQL Server，您必須是具備以服務登入權限的本機管理員。 
- 若您的電腦有「最低」** 實體記憶體需求，請將分頁檔增加至實體記憶體的兩倍。 虛擬記憶體不足可能會造成 SQL Server 移除不完全。 
- 在具備多個 SQL Server 執行個體的系統上，SQL Server 瀏覽器服務只會在移除最後一個 SQL Server 執行個體時解除安裝一次。 SQL Server 瀏覽器服務可以在 [控制台] 中的 [程式和功能] 中手動移除。 
- 解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會刪除在安裝程序期間所新增的 tempdb 資料檔案。 如果系統資料庫目錄中有名稱模式為 tempdb_mssql_*.ndf 的檔案，則會刪除這些檔案。 
  

  
## <a name="prepare"></a>準備  
  
1.  **備份資料。** 建立所有資料庫的[完整備份](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) (包括系統資料庫)，或是手動將 .mdf 和 .ldf 檔案複製到不同的位置。 **master** 資料庫包含伺服器所有的系統層級資訊，例如登入和結構描述。 **msdb** 資料庫包含作業資訊，例如 SQL Server 代理程式作業、備份歷程記錄和維護計劃。 如需系統資料庫的詳細資訊，請參閱[系統資料庫](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。 
  
    您必須儲存的檔案包括下列資料庫檔案：  

    |             |            |           |            |
    | :---------- | :--------- |:--------- | :--------- |
    | Master.mdf  | mastlog.ldf| model.mdf | modellog.ldf| 
    | msdbdata.mdf| msdblog.ldf| Mssqlsystemresource.mdf | Mssqlsustemresource.ldf |
    | Tempdb.mdf | Templog.ldf|  ReportServer[$InstanceName] | ReportServer[$InstanceName]TempDB| 

    > [!NOTE]
    > ReportServer 資料庫包含在 SQL Server Reporting Services 中。   

 
1.  **停止所有** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **服務。** ：建議您在解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件之前，先停止所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的本機安全性群組。 使用中的連接可能會導致解除安裝無法順利完成。  
  
1.  **使用具有適當權限的帳戶。** 請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶或具有同等權限的帳戶登入伺服器。 例如，您可以使用本機管理員群組成員的帳戶登入伺服器。  
  
## <a name="uninstall"></a>解除安裝 

# <a name="windows-10--2016-"></a>[Windows 10 / 2016 以上](#tab/Windows10)

若要從 Windows 10、Windows Server 2016、Windows Server 2019 及更新版本中解除安裝 SQL Server，請遵循下列步驟： 

1. 若要開始移除流程，請從 [開始] 功能表巡覽至 [設定]，然後選擇 [應用程式]。 
1. 在搜尋方塊中搜尋 `sql`。 
1. 選取 **Microsoft SQL Server (版本) (位元)** 。 例如： `Microsoft SQL Server 2017 (64-bit)` 。
1. 選取 [解除安裝]。
 
    ![解除安裝 SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-10.png)

1. 在 SQL Server 對話方塊快顯中選取 [移除] 來啟動 Microsoft SQL Server 安裝精靈。 

    ![移除 SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2017.png)
  
1.  在 [選取執行個體] 頁面上，使用下拉式方塊來指定要移除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或指定僅移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用功能和管理工具的選項。 若要繼續，請選取 [下一步]。  
  
1.  在 [選取功能] 頁面上，指定要從指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中移除的功能。  
  
1.  在 **[準備移除]** 頁面上，檢閱即將解除安裝之元件和功能的清單。 按一下 **[移除]** 開始解除安裝  
 
1. 重新整理 [應用程式與功能]**** 視窗來驗證已成功移除 SQL Server 執行個體，並判斷哪些 SQL Server 元件仍存在 (若有的話)。 若您有進行選擇的話，請也從此視窗移除這些元件。 

# <a name="windows-2008---2012-r2"></a>[Windows 2008 - 2012 R2](#tab/windows2012)

若要從 Windows Server 2008、Windows Server 2012 及 Windows 2012 R2 中解除安裝 SQL Server，請遵循下列步驟： 

1. 若要開始移除流程，請巡覽至 [控制台]，然後選取 [程式和功能]。
1. 以滑鼠右鍵按一下 [Microsoft SQL Server (版本) (位元)]，然後選取 [解除安裝]。 例如： `Microsoft SQL Server 2012 (64-bit)` 。  
  
    ![解除安裝 SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-2012.png)

1. 在 SQL Server 對話方塊快顯中選取 [移除] 來啟動 Microsoft SQL Server 安裝精靈。 

    ![移除 SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2012.png)
  
1.  在 [選取執行個體] 頁面上，使用下拉式方塊來指定要移除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或指定僅移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用功能和管理工具的選項。 若要繼續，請選取 [下一步]。  
  
1.  在 [選取功能] 頁面上，指定要從指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中移除的功能。  
  
1.  在 **[準備移除]** 頁面上，檢閱即將解除安裝之元件和功能的清單。 按一下 **[移除]** 開始解除安裝  
 
1. 重新整理 [程式和功能]**** 視窗來驗證已成功移除 SQL Server 執行個體，並判斷哪些 SQL Server 元件仍存在 (若有的話)。 若您有進行選擇的話，請也從此視窗移除這些元件。 

---

  
## <a name="in-the-event-of-failure"></a>失敗時  

若移除流程失敗，請檢閱 [SQL Server 安裝記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)來判斷根本原因。 

KB 文章[如何找出安裝程式記錄檔中的 SQL Server 安裝問題](https://support.microsoft.com/kb/955396/en-us)可協助進行調查。 雖然它是針對 SQL Server 2008，但文中描述的方法仍然適用每個 SQL Server 版本。 

  
## <a name="see-also"></a>另請參閱  
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
