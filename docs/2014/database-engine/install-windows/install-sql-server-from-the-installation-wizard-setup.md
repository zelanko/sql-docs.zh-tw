---
title: 從安裝精靈 （安裝程式） 安裝 SQL Server 2014 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
caps.latest.revision: 79
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 684a9d837fa08beaf8917a7193edff622aea4cc5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032169"
---
# <a name="install-sql-server-2014-from-the-installation-wizard-setup"></a>從安裝精靈安裝 SQL Server 2014 (安裝程式)
  本主題提供使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式的安裝精靈安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之新執行個體的逐步程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈會針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的安裝提供單一功能樹狀目錄，所以您不需要個別予以安裝。 如需有關可安裝各種元件的詳細資訊，請參閱[安裝 SQL Server 2014](installation-for-sql-server.md)。  如需有關如何安裝[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元件個別，請參閱[安裝 SQL Server 2014](install-sql-server.md)。  
  
 這些額外的主題列出了安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他方式：  
  
-   [從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。  
  
-   [安裝 SQL Server 2014 使用組態檔](install-sql-server-using-a-configuration-file.md)  
  
-   [SysPrep 安裝 SQL Server 2014 使用](install-sql-server-using-sysprep.md)  
  
-   [建立新的 SQL Server 容錯移轉叢集&#40;安裝&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)。  
  
-   [升級為 SQL Server 2014 使用安裝精靈&#40;安裝&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)。  
  
## <a name="prerequisites"></a>必要條件  
 在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請檢閱 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)中的主題。  
  
> [!NOTE]  
>  如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
  
### <a name="to-install-includesscurrentincludessscurrent-mdmd"></a>安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體。 在根資料夾中，按兩下 Setup.exe。 若要從網路共用進行安裝，請找出共用上的根資料夾，然後按兩下 Setup.exe。  
  
2.  安裝精靈會執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心。 若要建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新安裝，請在左側導覽區域中，按一下 **[安裝]**，然後按一下 **新增 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立安裝或將功能加入到現有安裝**。  
  
3.  在 [產品金鑰] 頁面上，選取選項，指出您要安裝免費的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，或具有 PID 金鑰之產品的產品版本。 如需詳細資訊，請參閱[版本和 SQL Server 2014 元件](../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
     若要繼續進行，請按 **[下一步]**。  
  
4.  在 [授權條款] 頁面上，檢閱授權合約，並在同意時，選取 [我接受授權條款]  核取方塊，然後按 [下一步] 。 若要協助提升 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您也可以啟用功能使用方式選項，並傳送報告給 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
5.  在 [全域規則] 視窗中，如果沒有規則錯誤，安裝程序會自動前進到 [產品更新] 視窗。  
  
6.  如果沒有核取控制台\所有控制台項目\Windows Update\變更設定中的 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 核取方塊，則接著會出現 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 頁面。 如果在 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 頁面中核取，會將電腦設定變更為當您掃描 Windows Update 時，包含最新的更新。  
  
7.  最新可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品更新會隨即顯示在 [產品更新] 頁面上。 如果未偵測到任何產品更新， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會顯示此頁面，而會自動前往 **[安裝安裝程式檔案]** 頁面。  
  
8.  安裝程式會在 [安裝安裝程式檔案] 頁面上，顯示下載、擷取及安裝安裝程式檔案的進度。 如有找到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的更新，並指定要包含該更新，將會一併安裝。  
  
9. 在 [安裝程式角色] 頁面上，選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [功能安裝]，然後按 [下一步] 繼續前往 [特徵選取] 頁面。  
  
10. 在 [特徵選取] 頁面上，選取要安裝的元件。 當您選取功能名稱之後，每一個元件群組的描述就會出現在 [功能描述]  窗格中。 您可以選取核取方塊的任何組合。 如需詳細資訊，請參閱[版本和 SQL Server 2014 元件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
     [選取之功能的必要元件]  窗格會顯示選取功能的必要元件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會在這個程序稍後說明的安裝步驟期間安裝尚未安裝的必要條件。  
  
     您也可以使用 [特徵選取] 頁面底部的欄位來指定共用元件的自訂目錄。 若要變更共用元件的安裝路徑，請在對話方塊底部的欄位中更新路徑，或是按一下 [瀏覽]  移至安裝目錄。 預設安裝路徑是 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]。  
  
     共用元件的指定路徑必須是絕對路徑。 資料夾不可以為壓縮或加密資料夾。 不支援使用對應磁碟機。  
  
     如果您在 64 位元的作業系統上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，將會看到下列選項：  
  
    1.  共用功能目錄  
  
    2.  共用功能目錄 (x86)  
  
     針對上述每個選項所指定的路徑必須是不同的。  
  
11. 如果所有規則都通過，[功能規則] 視窗會自動前進。  
  
12. 在 [執行個體組態] 頁面上，請指定要安裝預設執行個體還是具名執行個體。 如需詳細資訊，請參閱＜ [Instance Configuration](../../sql-server/install/instance-configuration.md)＞。  
  
     **執行個體識別碼** ：根據預設，此執行個體名稱會當做執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請為 [執行個體識別碼]  文字方塊指定其他值。  
  
    > [!NOTE]  
    >  標準的獨立 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體 (不論是預設還是具名執行個體) 都不會針對 [執行個體識別碼] 使用非預設的值。  
  
     所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升級項目都會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的每一個元件。  
  
     **安裝的執行個體** ：此方格會顯示執行安裝程式之電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果預設執行個體已經安裝在電腦上，您就必須安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的具名執行個體。  
  
     其餘的安裝工作流程會因您對安裝所指定的功能而不同。 您可能不會看到所有頁面，端視您的選取項目而定。  
  
13. 使用 [伺服器組態 - 服務帳戶] 頁面指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的登入帳戶。 在這個頁面上所設定的實際服務隨著您選取要安裝的功能而不同。  
  
     您可以將相同登入帳戶指派給所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，或個別設定每一個服務帳戶。 此外，您也可以指定要自動啟動服務、手動啟動服務或停用服務。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您個別設定服務帳戶，以針對各項服務提供最低權限，其中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會授與必須完成工作的最小權限。 如需詳細資訊，請參閱 [伺服器組態 - 服務帳戶](../../sql-server/install/server-configuration-service-accounts.md) 和 [設定 Windows 服務帳戶與權限](../configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
     若要針對此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的所有服務帳戶指定相同的登入帳戶，請在頁面底部的欄位中提供認證。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
     使用 [伺服器組態 - 定序] 頁面，為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指定非預設的定序。 如需詳細資訊，請參閱[伺服器組態 - 定序](../../sql-server/install/server-configuration-collation.md)。  
  
14. 使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - 伺服器組態] 頁面指定以下項目：  
  
    -   安全性模式 - 為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體選取 Windows 驗證或混合模式驗證。 如果您選取混合模式驗證，就必須為內建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員帳戶提供增強式密碼。  
  
         當裝置與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立成功的連接之後，Windows 驗證和混合模式的安全性機制是相同的。 如需詳細資訊，請參閱[Database Engine 組態-帳戶提供](../../sql-server/install/database-engine-configuration-account-provisioning.md)。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員 - 您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上至少必須指定一個系統管理員。 若要加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式執行所用的帳戶，請按一下 **[加入目前使用者]**。 若要從系統管理員清單中加入或移除帳戶，請按一下 **[加入]** 或 **[移除]**，然後編輯在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中將會有管理員權限的使用者、群組或電腦清單。  
  
     使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - 資料目錄] 頁面來指定非預設的安裝目錄。 若要安裝到預設目錄，請按 **[下一步]**。  
  
    > [!IMPORTANT]  
    >  如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的目錄共用。 此外，使用磁碟機或掛接點之根資料夾的資料目錄來安裝 SQL Server，將會失敗。 如需詳細資訊，請檢閱[掛接的磁碟區的 SQL Server 支援。](http://support.microsoft.com/kb/819546/en-us)  
  
     如需詳細資訊，請參閱 [Database Engine 組態 - 資料目錄](../../sql-server/install/database-engine-configuration-data-directories.md)。  
  
     使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - FILESTREAM] 頁面來針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體啟用 FILESTREAM。 如需詳細資訊，請參閱 [Database Engine 組態 - Filestream](../../sql-server/install/database-engine-configuration-filestream.md)。  
  
15. 您可以使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態 - 帳戶提供] 頁面指定伺服器模式以及要擁有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之管理員權限的使用者或帳戶。 伺服器模式會決定在伺服器上所要使用的記憶體及儲存體子系統。 不同方案類型會在不同的伺服器模式中執行。 如果要在伺服器上執行多維度 Cube 資料庫，請選擇預設選項 [多維度及資料採礦伺服器模式]。 無論系統管理員權限為何，至少須為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定一名系統管理員。 如果要加入執行 SQL Server 安裝程式的帳戶，請按一下 [加入目前使用者] 。 若要在系統管理員清單中加入或移除帳戶，請按一下 **[加入]** 或 **[移除]**，然後編輯在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中將會有管理員權限的使用者、群組或電腦清單。 如需伺服器模式及系統管理員權限的詳細資訊，請參閱 [Analysis Services 組態 - 帳戶提供](../../sql-server/install/analysis-services-configuration-account-provisioning.md)。  
  
     當您完成清單的編輯之後，請按一下 **[確定]**。 然後，在組態對話方塊中確認管理員的清單。 當此清單完成時，請按 **[下一步]**。  
  
     使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態 - 資料目錄] 頁面來指定非預設的安裝目錄。 若要安裝到預設目錄，請按 **[下一步]**。  
  
    > [!IMPORTANT]  
    >  如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的目錄共用。 此外，使用磁碟機或掛接點之根資料夾的資料目錄來安裝 SQL Server，將會失敗。 如需詳細資訊，請檢閱[掛接的磁碟區的 SQL Server 支援。](http://support.microsoft.com/kb/819546/en-us)  
  
     如需詳細資訊，請參閱 [Analysis Services 組態 - 資料目錄](../../sql-server/install/analysis-services-configuration-data-directories.md)。  
  
16. 使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態 頁面來指定要建立的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝類型。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態模式和選項的詳細資訊，請參閱 [Reporting Services 組態選項 &#40;SSRS&#41;](../../sql-server/install/reporting-services-configuration-options-ssrs.md)。  
  
     選擇選項之後，請按一下 [下一步] 繼續進行。  
  
17. 您可以使用 [Distributed Replay Controller 組態] 頁面，指定要授與 Distributed Replay Controller 服務之管理權限的使用者。 擁有管理權限的使用者將可不受限制地存取 Distributed Replay Controller 服務。  
  
     按一下 [加入目前使用者]  按鈕，可加入要授與 Distributed Replay Controller 服務之存取權限的使用者。 按一下 [加入]  按鈕，可加入 Distributed Replay Controller 服務的存取權限。 按一下 [移除]  按鈕，可移除 Distributed Replay Controller 服務的存取權限。  
  
     若要繼續進行，請按 **[下一步]**。  
  
18. 您可以使用 [Distributed Replay Client 組態] 頁面，指定要授與 Distributed Replay Client 服務之管理權限的使用者。 擁有管理權限的使用者將可不受限制地存取 Distributed Replay Client 服務。  
  
     [控制器名稱] 是選擇性參數，預設值為 \<空白>。 針對 Distributed Replay Client 服務，輸入將與用戶端電腦進行通訊之控制器的名稱。 請注意下列事項：  
  
    -   如果您已經設定了控制器，請在設定每個用戶端時輸入該控制器的名稱。  
  
    -   如果您尚未設定控制器，則可以將控制器名稱留白。 不過，您必須在 [用戶端組態]  檔中，手動輸入控制器名稱。  
  
     指定 Distributed Replay Client 服務的 **工作目錄** 。 預設工作目錄為 \<磁碟機代號>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\WorkingDir\\。  
  
     指定 Distributed Replay Client 服務的 **結果目錄** 。 預設工作目錄為 \<磁碟機代號>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\DReplayClient\ResultDir\\。  
  
     若要繼續進行，請按 **[下一步]**。  
  
19. [準備安裝] 頁面會顯示在安裝期間指定之安裝選項的樹狀檢視。 在此頁面上，安裝程式會指出產品更新功能為啟用或停用，以及最後的更新版本。  
  
     若要繼續，請按一下 **[安裝]**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會先安裝選取功能所需的必要條件，之後再進行功能安裝。  
  
20. 在安裝期間，[安裝進度] 頁面會提供狀態，好讓您可以在安裝程式進行時監視安裝進度。  
  
21. 安裝之後，[完成] 頁面會提供安裝和其他重要注意事項之摘要記錄檔的連結。 若要完成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序，請按一下 **[關閉]**。  
  
22. 如果指示您重新啟動電腦，請立刻執行。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](view-and-read-sql-server-setup-log-files.md)＞。  
  
## <a name="next-steps"></a>後續步驟  
 設定新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝。  
  
 為了減少系統的可攻擊介面區， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以選擇性地安裝和啟用主要服務和功能。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [驗證 SQL Server 安裝](validate-a-sql-server-installation.md)   
 [卸除 SQL Server 2014 安裝](repair-a-failed-sql-server-installation.md)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](view-and-read-sql-server-setup-log-files.md)   
 [升級為 SQL Server 2014 使用安裝精靈&#40;安裝程式&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)  
  
  