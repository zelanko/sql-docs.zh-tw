---
title: 從安裝精靈安裝 SQL Server 2016 (安裝程式) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, steps
- Setup [SQL Server], steps
- SQL Server, installing
ms.assetid: 6ad23de1-2bab-4933-9122-c09f5565028d
caps.latest.revision: 91
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 03a3e40c8e3fd9fdcb1a40cc5da19ea3779a8e0c
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40412728"
---
# <a name="install-sql-server-from-the-installation-wizard-setup"></a>從安裝精靈安裝 SQL Server 2016 (安裝程式)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
本文說明如何使用安裝精靈安裝 SQL Server。 它會套用至 [!INCLUDE[SQLServer2016](../../includes/sssql15-md.md)] 和 [!INCLUDE[SQLServer2017](../../includes/sssqlv14-md.md)]。 如需舊版 SQL Server 的相關內容，請參閱[從安裝精靈安裝 SQL Server 2014 (安裝程式)](http://msdn.microsoft.com/library/ms143219(SQL.120).aspx)。

本文提供的逐步程序，可讓您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的安裝精靈來進行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新執行個體安裝。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈會針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的安裝提供單一功能樹狀目錄，所以您不需要個別予以安裝。 如需如何個別安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的詳細資訊，請參閱[安裝 SQL Server](../../database-engine/install-windows/install-sql-server.md#how-to-install-individual-components)。  

 這些額外的文章記載安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的其他方式：  

-   [從命令提示字元安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
-   [使用設定檔安裝 SQL Server](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)  
  
-   [使用 SysPrep 安裝 SQL Server](../../database-engine/install-windows/install-sql-server-using-sysprep.md)  
  
-   [建立新的 SQL Server 容錯移轉叢集 &#40;安裝程式&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)  
  
-   [使用安裝精靈升級 SQL Server &#40;安裝程式&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) 

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]
  
## <a name="prerequisites"></a>Prerequisites  
 在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前，請檢閱[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)中的文章。  
  
> [!NOTE]  
> 如果是本機安裝，您必須以管理員身分執行安裝程式。 如果您是從遠端共用位置安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須使用對遠端共用位置具有讀取和執行權限的網域帳戶。  
 
 ###  <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 

Microsoft 發現特定版本的 Microsoft VC++ 2013 Runtime 二進位檔問題，SQL Server 必須安裝這些二進位檔。 如果未安裝 VC Runtime 二進位檔的這項更新，SQL Server 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 之前，請先遵循 [SQL Server 版本資訊](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)的指示，查看您的電腦是否需要 VC Runtime 二進位檔的修補程式。  
  
## <a name="to-install-includessnoversionincludesssnoversion-mdmd"></a>安裝 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]  
  
1.  插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體。 在根資料夾中，按兩下 Setup.exe。 若要從網路共用進行安裝，請找出共用上的根資料夾，然後按兩下 Setup.exe。  
  
2.  安裝精靈會執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝中心。 若要建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新安裝，請在左側導覽區域中，按一下 **[安裝]**，然後按一下 **新增 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立安裝或將功能加入到現有安裝**。  

3.  在 [產品金鑰] 頁面上，選取選項，指出您要安裝免費的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，或具有 PID 金鑰之產品的產品版本。 如需詳細資訊，請參閱 [SQL Server 2017 的版本及支援功能](../../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
     若要繼續進行，請按 **[下一步]**。  

4.  在 [授權條款] 頁面上，檢閱授權合約，並在同意時，選取 [我接受授權條款]  核取方塊，然後按 [下一步] 。  

  >[!NOTE]
  > SQL Server 會將您的安裝經驗及其他使用方式與效能資料的相關資訊傳送給 Microsoft，以協助改進產品。 若要深入了解 SQL Server 資料處理與隱私權控制，請參閱[隱私權聲明](https://privacy.microsoft.com/en-us/privacystatement)和[設定 SQL Server 將意見反應傳送給 Microsoft](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-customer-feedback?view=sql-server-2016)。 
  
5.  在 [全域規則] 視窗中，如果沒有規則錯誤，安裝程序會自動前進到 [產品更新] 視窗。  
  
6.  如果沒有核取控制台\所有控制台項目\Windows Update\變更設定中的 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 核取方塊，則接著會出現 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 頁面。 如果在 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)] 更新] 頁面中核取，會將電腦設定變更為當您掃描 Windows Update 時，包含最新的更新。  

7.  最新可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品更新會隨即顯示在 [產品更新] 頁面上。 如果未偵測到任何產品更新， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會顯示此頁面，而會自動前往 **[安裝安裝程式檔案]** 頁面。  

8.  安裝程式會在 [安裝安裝程式檔案] 頁面上，顯示下載、擷取及安裝安裝程式檔案的進度。 如有找到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式的更新，並指定要包含該更新，將會一併安裝。 如果找不到任何更新，則安裝程式會自動繼續。 
  
9. 在 [安裝規則] 上，SQL Server 安裝程式會檢查以識別執行安裝程式時可能發生的潛在問題。 如果失敗，請按一下 [狀態] 資料行以取得詳細資訊。 否則，請按一下 [下一步]。 

10. 如果這是您第一次在電腦上安裝 SQL Server，會略過 [安裝類型]頁面，安裝作業會直接前往 [特徵選取]頁面。 但是，如果系統上已經安裝 SQL Server，請在 [安裝類型] 上，選擇執行新安裝，或將功能新增至現有安裝。 按 [下一步] 。 
  
11. 在 [特徵選取] 頁面上，選取要安裝的元件。 例如，若要安裝 SQL Server 資料庫引擎的新執行個體，請檢查 [資料庫引擎服務]。

    當您選取功能名稱之後，每一個元件群組的描述就會出現在 [功能描述]  窗格中。 您可以選取核取方塊的任何組合。 如需詳細資訊，請參閱 [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)和 [SQL Server 2016 的版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。
  
     [選取之功能的必要元件]  窗格會顯示選取功能的必要元件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會在這個程序稍後說明的安裝步驟期間安裝尚未安裝的必要條件。  
  
     您也可以使用 [特徵選取] 頁面底部的欄位來指定共用元件的自訂目錄。 若要變更共用元件的安裝路徑，請在對話方塊底部的欄位中更新路徑，或是按一下 [瀏覽]  移至安裝目錄。 預設安裝路徑是 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]。  
  
     共用元件的指定路徑必須是絕對路徑。 資料夾不可以為壓縮或加密資料夾。 不支援使用對應磁碟機。  
  
     SQL Server 使用兩個共用功能目錄：
  
     * 共用功能目錄  
  
     * 共用功能目錄 (x86)  
  
     針對上述每個選項所指定的路徑必須是不同的。  
  
12. 如果所有規則都通過，[功能規則] 視窗會自動前進。  
  
13. 在 [執行個體組態] 頁面上，請指定要安裝預設執行個體還是具名執行個體。 如需詳細資訊，請參閱＜ [Instance Configuration](../../sql-server/install/instance-configuration.md#instance-configuration)＞。  
  
     **執行個體識別碼** ：根據預設，此執行個體名稱會當做執行個體識別碼使用。 這是用來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的安裝目錄和登錄機碼。 這是預設執行個體和具名執行個體的狀況。 如果是預設執行個體，執行個體名稱和執行個體識別碼將會是 MSSQLSERVER。 若要使用非預設的執行個體識別碼，請為 [執行個體識別碼]  文字方塊指定其他值。  
  
    > [!NOTE]  
    >  標準的獨立 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]執行個體 (不論是預設還是具名執行個體) 都不會針對 [執行個體識別碼] 使用非預設的值。  
  
     所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升級項目都會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的每一個元件。  
  
     **安裝的執行個體** ：此方格會顯示執行安裝程式之電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果預設執行個體已經安裝在電腦上，您就必須安裝 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]的具名執行個體。  
  
     其餘的安裝工作流程會因您對安裝所指定的功能而不同。 您可能不會看到所有頁面，端視您的選取項目而定。  
  
14. 使用 [伺服器組態 - 服務帳戶] 頁面指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的登入帳戶。 在這個頁面上所設定的實際服務隨著您選取要安裝的功能而不同。  
  
     您可以將相同登入帳戶指派給所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，或個別設定每一個服務帳戶。 此外，您也可以指定要自動啟動服務、手動啟動服務或停用服務。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您個別設定服務帳戶，以針對各項服務提供最低權限，其中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會授與必須完成工作的最小權限。 如需詳細資訊，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
     若要針對此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的所有服務帳戶指定相同的登入帳戶，請在頁面底部的欄位中提供認證。  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
    
    > [!NOTE]
    > 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，核取 [對 SQL Server Database Engine 服務授與「執行磁碟區維護工作」權限] 方塊，以允許 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務帳戶使用[資料庫檔案立即初始化](../../relational-databases/databases/database-instant-file-initialization.md)。
  
     使用 [伺服器組態 - 定序] 頁面，為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定非預設的定序。 如需詳細資訊，請參閱[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
15. 使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - 伺服器組態] 頁面指定以下項目：  
  
    -   安全性模式 - 為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體選取 Windows 驗證或混合模式驗證。 如果您選取混合模式驗證，就必須為內建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員帳戶提供增強式密碼。  
  
         當裝置與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立成功的連接之後，Windows 驗證和混合模式的安全性機制是相同的。 如需詳細資訊，請參閱 [Database Engine 組態 - 伺服器組態](../../sql-server/install/instance-configuration.md#database-engine-configuration---server-configuration)。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員 - 您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上至少必須指定一個系統管理員。 若要加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式執行所用的帳戶，請按一下 **[加入目前使用者]**。 若要從系統管理員清單中加入或移除帳戶，請按一下 **[加入]** 或 **[移除]**，然後編輯在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中將會有管理員權限的使用者、群組或電腦清單。  
  
     使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - 資料目錄] 頁面來指定非預設的安裝目錄。 若要安裝到預設目錄，請按 **[下一步]**。  
  
    > [!IMPORTANT]  
    > 如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的目錄共用。  
  
     如需詳細資訊，請參閱 [Database Engine 組態 - 資料目錄](../../sql-server/install/instance-configuration.md#database-engine-configuration---data-directories)。  
  
     使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - FILESTREAM] 頁面來針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體啟用 FILESTREAM。 如需詳細資訊，請參閱 [Database Engine 組態 - Filestream](../../sql-server/install/instance-configuration.md#database-engine-configuration---filestream)。  
  
     使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] [組態 - TempDB] 頁面來設定 TempDB 的檔案大小、檔案數目、非預設安裝目錄和檔案成長設定。 如需詳細資訊，請參閱 [Database Engine 組態 - TempDB](../../sql-server/install/instance-configuration.md#database-engine-configuration---tempdb)。  
  
16. 您可以使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態 - 帳戶提供] 頁面指定伺服器模式以及要擁有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之管理員權限的使用者或帳戶。 伺服器模式會決定在伺服器上所要使用的記憶體及儲存體子系統。 不同方案類型會在不同的伺服器模式中執行。 如果要在伺服器上執行多維度 Cube 資料庫，請選擇預設選項 [多維度及資料採礦伺服器模式]。 無論系統管理員權限為何，至少須為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]指定一名系統管理員。 如果要加入執行 SQL Server 安裝程式的帳戶，請按一下 [加入目前使用者] 。 若要在系統管理員清單中加入或移除帳戶，請按一下 **[加入]** 或 **[移除]**，然後編輯在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中將會有管理員權限的使用者、群組或電腦清單。 如需伺服器模式及系統管理員權限的詳細資訊，請參閱 [Analysis Services 組態 - 帳戶提供](../../sql-server/install/instance-configuration.md#analysis-services-configuration---account-provisioning)。  

   當您完成清單的編輯之後，請按一下 **[確定]**。 然後，在組態對話方塊中確認管理員的清單。 當此清單完成時，請按 **[下一步]**。
   
   使用 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 組態 - 資料目錄] 頁面來指定非預設的安裝目錄。 若要安裝到預設目錄，請按 **[下一步]**。  
   
   > [!IMPORTANT]  
   > 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，若您為 INSTANCEDIR 和 SQLUSERDBDIR 指定相同的目錄路徑，SQL Server Agent 和全文檢索搜尋會因為遺漏權限而無法啟動。  
   >  
   > 如果您要指定非預設的安裝目錄，請確定安裝資料夾對於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體是唯一的。 此對話方塊上的任何目錄都不應該與其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的目錄共用。  
   
   如需詳細資訊，請參閱 [Analysis Services 組態 - 資料目錄](../../sql-server/install/instance-configuration.md#analysis-services-configuration---data-directories)。  
   
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
  
22. 如果指示您重新啟動電腦，請立刻執行。 當您完成安裝時，請務必閱讀安裝精靈所提供的訊息。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)＞。  
  
## <a name="next-steps"></a>後續步驟  
 設定新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝。  
  
 為了減少系統的可攻擊介面區， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以選擇性地安裝和啟用主要服務和功能。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [驗證 SQL Server 安裝](../../database-engine/install-windows/validate-a-sql-server-installation.md)   
 [修復失敗的 SQL Server 2016 安裝](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [使用安裝精靈升級為 SQL Server 2016 &#40;安裝程式&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
