---
title: 升級為 SQL Server 2014 使用安裝精靈 （安裝程式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- upgrading Database Engine
- Database Engine [SQL Server], upgrading
ms.assetid: cef118a5-a7ce-4bfa-8b9d-c81996284cfc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8330702d8c886cc9197dcd944878c3f794780205
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775392"
---
# <a name="upgrade-to-sql-server-2014-using-the-installation-wizard-setup"></a>使用安裝精靈升級為 SQL Server 2014 (安裝程式)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈提供了升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的單一功能樹狀目錄。 您也可以將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 與舊版並存安裝，或是從舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉現有的資料庫和組態設定，然後將它們套用至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的執行個體。  
  
 如需詳細資訊，請參閱下列主題：  
  
-   [支援的版本與版本升級](supported-version-and-edition-upgrades.md)  
  
-   [使用 SQL Server 的多個版本和執行個體](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
  
-   [升級 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
-   [從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)  
  
-   [使用複製資料庫精靈](../../relational-databases/databases/use-the-copy-database-wizard.md)  
  
> [!NOTE]  
>  在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Core SP1 的電腦上，不支援將舊版 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升級為 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]。 如需有關 Server Core 安裝的詳細資訊，請參閱[在 Server Core 上安裝 SQL Server 2014](install-sql-server-on-server-core.md)。  
  
## <a name="prerequisites"></a>先決條件  
 您必須以系統管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則必須使用對遠端共用位置具有讀取和執行權限並且為本機系統管理員的網域帳戶。  
  
 在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之前，請檢閱下列主題：  
  
-   [升級到 SQL Server 2014](upgrade-sql-server.md)  
  
-   [安裝 SQL Server 2014 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [檢查 System Configuration Checker 的參數](check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [SQL Server Database Engine 回溯相容性](../sql-server-database-engine-backward-compatibility.md)  
  
> [!WARNING]  
>  請注意，您無法變更要升級的功能，而且您無法在升級作業期間加入功能。 如需有關如何將功能加入至升級的執行個體[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升級作業完成之後，請參閱[將功能加入至執行個體 SQL Server 2014 的&#40;安裝&#41;](add-features-to-an-instance-of-sql-server-setup.md)。  
  
## <a name="procedure"></a>程序  
  
#### <a name="to-upgrade-to-includesscurrentincludessscurrent-mdmd"></a>升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體，然後在根資料夾中，按兩下 Setup.exe。 若要從網路共用區進行安裝，請移到共用區上的根資料夾，然後按兩下 Setup.exe。  
  
2.  安裝精靈會啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心。 若要升級現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，請按一下左側導覽區域中的 [安裝]  ，然後再按一下 [從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 升級]  。  
  
3.  在 [產品金鑰] 頁面上，按一下選項，指出您要升級為免費的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本，還是您擁有產品之產品版本的 PID 金鑰。 如需詳細資訊，請參閱 <<c0> [ 版本和 SQL Server 2014 元件](../../sql-server/editions-and-components-of-sql-server-2016.md)並[Supported Version and Edition Upgrades](supported-version-and-edition-upgrades.md)。  
  
4.  在 [授權條款] 頁面上，檢閱授權合約，並在同意時，選取 [我接受授權條款]  核取方塊，然後按 [下一步]  。 若要協助提升 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您也可以啟用功能使用方式選項，並傳送報告給 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
5.  在 [全域規則] 視窗中，如果沒有規則錯誤，安裝程序會自動前進到 [產品更新] 視窗。  
  
6.  如果沒有核取控制台\所有控制台項目\Windows Update\變更設定中的 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 核取方塊，則接著會出現 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 頁面。 如果在 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 頁面中核取，會將電腦設定變更為當您掃描 Windows Update 時，包含最新的更新。  
  
7.  最新可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品更新會隨即顯示在 [產品更新] 頁面上。 如果不想包含更新，請清除 包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品更新程式  核取方塊。 如果未偵測到任何產品更新， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會顯示此頁面，而會自動前往 **[安裝安裝程式檔案]** 頁面。  
  
8.  安裝程式會在 [安裝安裝檔案] 頁面上，顯示下載、擷取及安裝安裝檔案的進度。 如有找到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的更新，並指定要包含該更新，將會一併安裝。  
  
9. 在 [升級規則] 視窗中，如果沒有規則錯誤，安裝程序會自動前進到 [選取執行個體] 視窗。  
  
10. 在 [選取執行個體] 頁面中，指定要升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 若要升級管理工具和共用功能，請選取 [僅升級共用功能]  。  
  
11. 在 [選取功能] 頁面上，系統會預先選取要升級的功能。 當您選取功能名稱之後，每一個元件群組的描述就會出現在右窗格中。  
  
     右窗格會顯示選取功能的必要條件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會在這個程序稍後說明的安裝步驟期間安裝尚未安裝的必要條件。  
  
    > [!NOTE]  
    >  如果您在 [選取執行個體]  頁面上選取 [\<僅升級共用功能>]  來選擇升級共用功能，則 [功能選取] 頁面上會預先選取所有共用功能。 所有共用元件都會同時升級。  
  
12. 在 [執行個體組態] 頁面上，指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的執行個體識別碼。  
  
     **執行個體識別碼** ：依預設，此執行個體名稱會當作執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請提供 [執行個體識別碼]  文字方塊的值。  
  
     所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升級項目都會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的每一個元件。  
  
     **安裝的執行個體**：此方格會顯示執行安裝程式之電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果預設執行個體已經安裝在電腦上，您就必須安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的具名執行個體。  
  
13. 本主題其餘部分的工作流程會因您針對安裝所指定的功能而不同。 您可能不會看到所有頁面，端視您的選取項目而定。  
  
14. [伺服器組態 - 服務帳戶] 頁面上會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的預設服務帳戶。 在這個頁面上所設定的實際服務隨著您要升級的功能而不同。  
  
     驗證和登入資訊將來自先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 您可以將相同登入帳戶指派給所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，或個別設定每一個服務帳戶。 此外，您也可以指定要自動啟動服務、手動啟動服務或停用服務。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您個別設定服務帳戶，以便 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會授與必須完成工作的最小權限。 如需詳細資訊，請參閱 [設定 Windows 服務帳戶與權限](../configure-windows/configure-windows-service-accounts-and-permissions.md)預覽版本升級問題的解答。  
  
     若要針對此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的所有服務帳戶指定相同的登入帳戶，請在頁面底部的欄位中提供認證。  
  
     **安全性注意事項** [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     當您完成針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務指定登入資訊之後，請按 **[下一步]** 。  
  
15. 在 [全文檢索搜尋升級選項] 頁面上，針對升級的資料庫指定升級選項。 如需詳細資訊，請參閱 [全文檢索搜尋升級選項](../../sql-server/install/full-text-search-upgrade-options.md)。  
  
16. 如果所有規則都通過，[功能規則] 視窗會自動前進。  
  
17. [準備升級] 頁面會顯示在安裝期間指定之安裝選項的樹狀檢視。 若要繼續，請按一下 **[安裝]** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會先安裝選取功能所需的必要條件，之後再進行功能安裝。  
  
18. 在安裝期間，進度頁面會提供狀態，好讓您可以在安裝程式進行時監視安裝進度。  
  
19. 安裝之後，[完成] 頁面會提供安裝和其他重要注意事項之摘要記錄檔的連結。 若要完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序，請按一下 **[關閉]** 。  
  
20. 如果指示您重新啟動電腦，請立刻執行。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需安裝程式記錄檔的詳細資訊，請參閱 [檢視與讀取 SQL Server 安裝程式記錄檔](view-and-read-sql-server-setup-log-files.md)。  
  
## <a name="next-steps"></a>後續步驟  
 在升級為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後，請完成下列工作：  
  
-   **註冊伺服器**：升級會移除先前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的登錄設定。 在升級之後，您必須重新註冊伺服器。  
  
-   **更新統計資料**：若要協助最佳化查詢效能，我們建議您在升級之後，更新所有資料庫的統計資料。 請使用 `sp_updatestats` 預存程序更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中使用者定義資料表的統計資料。  
  
-   **設定新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝**：為了減少系統的可攻擊介面區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會選擇性地安裝及啟用主要服務和功能。 如需有關介面區組態的詳細資訊，請參閱這一版的讀我檔案。  
  
## <a name="see-also"></a>另請參閱  
 [升級到 SQL Server 2014](upgrade-sql-server.md)   
 [回溯相容性](../../getting-started/backward-compatibility.md)  
  
  
