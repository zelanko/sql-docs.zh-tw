---
title: 套件管理 (SSIS 服務) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.dtsserver.importpackage.f1
- sql13.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- SQL Server Integration Services packages, managing
- packages [Integration Services], managing
- Integration Services packages, managing
- storing packages
- Stored Packages folder
- current packages
- Running Packages folder
- status information [Integration Services]
- SSIS packages, managing
- storage [Integration Services]
- monitoring [Integration Services], packages
- Integration Services service, package management
- services [Integration Services], package management
ms.assetid: 0261ed9e-3b01-4e37-a9d4-d039c41029b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 00ed915265b9b3c19e7bafdcf7d6c41208e8319a
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280462"
---
# <a name="package-management-ssis-service"></a>封裝管理 (SSIS 服務)
  套件管理包含監視、管理、匯入和匯出套件。  
 
 ## <a name="package-store"></a>封裝存放區  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供用於存取套件的兩個最上層資料夾： 
 - **[Running Packages]** 
 - **[Stored Packages]**

 **[Running Packages]** 資料夾會列出伺服器上目前正在執行的封裝。 **[Stored Packages]** 資料夾會列出所有儲存在封裝存放區中的封裝。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務只會管理這些封裝。 封裝存放區可以只由 msdb 資料庫組成，或者由該資料庫和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務組態檔中所列之檔案系統資料夾所組成。 組態檔會指定要管理的 msdb 及檔案系統資料夾。 您可能還有不是由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的封裝，而存放在檔案系統的其他位置。  
  
 您儲存至 msdb 的套件會存放在名為 sysssispackages 的資料表中。 當您將套件儲存至 msdb 時，可以將它們群組成邏輯資料夾。 使用邏輯資料夾可以協助您依用途組織套件，或是篩選 sysssispackages 資料表中的套件。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立新邏輯資料夾。 依預設，您加入至 msdb 的任何邏輯資料夾都會自動納入封裝存放區。  
  
 您建立的邏輯資料夾會呈現為 msdb 中 sysssispackagefolders 資料表的資料列。 sysssispackagefolders 中的 folderid 及 parentfolderid 資料行會定義資料夾階層。 msdb 中的根邏輯資料夾是 sysssispackagefolders 的 parentfolderid 資料行中具有 Null 值的資料列。 如需詳細資訊，請參閱 [sysssispackages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysssispackages-transact-sql.md) 和 [sysssispackagefolders (Transact-SQL&)](../../relational-databases/system-tables/sysssispackagefolders-transact-sql.md)。  
  
 當您開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]時，會看到列在 Stored Packages 資料夾中由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的 msdb 資料夾。 如果組態檔指定了根檔案系統資料夾，[Stored Packages] 資料夾也會在這些資料夾及所有子資料夾中列出儲存至檔案系統的封裝。  
  
 您可以將封裝存放在任何檔案系統資料夾中，但這些封裝不會列在 **[Stored Packages]** 資料夾的子資料夾中，除非您在組態檔的封裝存放區資料夾清單中加入這個資料夾。 如需組態檔的詳細資訊，請參閱 [Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/integration-services-service-ssis-service.md)回溯相容。  
  
 **[Running Packages]** 資料夾不包含子資料夾，且不可延伸。  
  
 依預設，[Stored Packages] 資料夾包含兩個資料夾：[File System] 和 [MSDB]。 **[檔案系統]** 資料夾會列出儲存至檔案系統的封裝。 這些檔案的位置是在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的組態檔中指定的。 預設資料夾為 [封裝] 資料夾，位於 %Program Files%\Microsoft SQL Server\100\DTS。 **MSDB** 資料夾會列出已儲存至伺服器上 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] msdb 資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 封裝。 sysssispackages 資料表包含 msdb 中所儲存的封裝。  
  
 若要檢視封裝存放區中的封裝清單，您必須開啟 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 並連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
  
## <a name="monitor-running-packages"></a>監視執行中套件  
 [Running Packages] 資料夾會列出目前正在執行的套件。 若要在 **的** [摘要] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]頁面上檢視有關目前封裝的資訊，請按一下 **Running Packages** 資料夾。 **[摘要]** 頁面上會列出諸如正在執行封裝的執行持續時間等資訊。 選擇性地重新整理資料夾以顯示最新的資訊。  
  
 若要在 **[摘要]** 頁面上檢視有關單一正在執行封裝的資訊，請按一下該封裝。 **[摘要]** 頁面會顯示諸如封裝的版本和描述等資訊。  
  
在 [Running Packages] 資料夾中以滑鼠右鍵按一下套件，然後按一下 [停止]，以停止執行中套件。  
  
## <a name="view-packages-in-ssms"></a>檢視 SSMS 中的套件
    
 此程序描述如何在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，以及檢視 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的封裝清單。  
  
### <a name="to-connect-to-integration-services"></a>連接到 Integration Services  
  
1.  按一下 **[開始]**，依序指向 **[所有程式]** 和 **[Microsoft SQL Server]**，然後按一下 **[SQL Server Management Studio]**。  
  
2.  在 [連接到伺服器] 對話方塊中，選取 [伺服器類型] 清單中的 [Integration Services]，在 [伺服器名稱] 方塊中提供伺服器名稱，然後按一下 [連接]。  
  
    > [!IMPORTANT]  
    >  如果您無法連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務目前可能沒有執行。 若要了解此服務的狀態，請按一下 **[開始]**，依序指向 **[所有程式]**、 **[Microsoft SQL Server]** 和 **[組態工具]**，然後按一下 **[SQL Server 組態管理員]**。 在左窗格中，按一下 **[SQL Server 服務]**。 在右窗格中，尋找 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 如果此服務尚未執行，請將它啟動。  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 隨即開啟。 依預設，[物件總管] 視窗會在 Studio 左下角開啟並定位。 如果 [物件總管] 未開啟，請按一下 **[檢視]** 功能表上的 **[物件總管]** 。  
  
### <a name="to-view-the-packages-that-integration-services-service-manages"></a>若要檢視 Integration Services 服務所管理的封裝  
  
1.  在 [物件總管] 中，展開 [存放的封裝] 資料夾。  
  
2.  展開 [Stored Packages] 的子資料夾以顯示封裝。  

## <a name="import-and-export-packages"></a>匯入和匯出套件
 
 封裝可以儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 資料庫的 sysssispackages 資料表中，也可以儲存在檔案系統中。  
  
 封裝存放區 ( [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所監視和管理的邏輯儲存體) 可以同時包含在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務之組態檔中指定的 msdb 資料庫和檔案系統資料夾。  
  
 您可以在下列儲存體類型之間匯入和匯出封裝：  
  
-   檔案系統中任意位置的檔案系統資料夾。  
  
-   「SSIS 封裝存放區」中的資料夾。 兩個預設資料夾名為 File System 和 MSDB。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 資料庫。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可讓您匯入和匯出封裝，並藉此變更封裝的儲存格式和位置。 使用匯入和匯出功能，可以將封裝加入檔案系統、封裝存放區或 msdb 資料庫，並將封裝從一個儲存體複製到另一個儲存體。 例如，可以將 msdb 中儲存的封裝複製到檔案系統，反之亦然。  
  
 您也可以使用 **dtutil** 命令提示公用程式 (dtutil.exe)，將封裝複製成其他格式。 如需詳細資訊，請參閱 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
 您可以在下列位置之間匯入或匯出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝：  
  
-   您可以匯入儲存在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體、檔案系統或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區內的封裝。 匯入的封裝將儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區內的資料夾中。  
  
-   您可以將儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體、檔案系統或 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區內的封裝匯出至不同的儲存格式和位置。  
  
 不過，在不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本之間匯入和匯出封裝有一些限制：  
  
-   在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的執行個體上，雖然您可以從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的執行個體匯入封裝，但是無法將封裝匯出至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的執行個體。  
  
-   在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的執行個體上，您無法在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的執行個體之間匯入封裝或匯出封裝。  
  
 下列程序將描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來匯入或匯出封裝。  
  
### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來匯入封裝  
  
1.  按一下 [開始]、指向 [Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]，然後按一下 [SQL Server Management Studio]。  
  
2.  在 [連接到伺服器] 對話方塊上，設定下列選項：  
  
    -   在 [伺服器類型] 方塊中，選取 [Integration Services]。  
  
    -   在 [伺服器名稱] 方塊中提供伺服器名稱，或按一下 [\<瀏覽其他...>]，並尋找要使用的伺服器。  
  
3.  如果物件總管尚未開啟，請在 [檢視] 功能表上，按一下物件總管。  
  
4.  在物件總管中，展開 [存放的封裝] 資料夾。  
  
5.  展開子資料夾以尋找您要匯入封裝的資料夾。  
  
6.  以滑鼠右鍵按一下資料夾，然後按一下 [匯入封裝]。 然後執行下列其中之一：  
  
    -   若要從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體匯入，請選取 [SQL Server] 選項，然後指定伺服器並選取驗證模式。 如果選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱和密碼。  
  
         按一下瀏覽按鈕 ([...])，選取要匯入的封裝，然後按一下 [確定]。  
  
    -   若要從檔案系統匯入，請選取 [檔案系統] 選項。  
  
         按一下瀏覽按鈕 ([...])，選取要匯入的封裝，然後按一下 [開啟]。  
  
    -   若要從 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區匯入，請選取 [SSIS 封裝存放區] 選項並指定伺服器。  
  
         按一下瀏覽按鈕 ([...])，選取要匯入的封裝，然後按一下 [確定]。  
  
7.  (選擇性) 更新封裝名稱。  
  
8.  若要更新封裝的保護等級，請按一下瀏覽按鈕 ([...])，並使用 [封裝保護等級] 對話方塊選擇其他保護等級。 如果選取 [機密資料以密碼加密] 或 [所有資料以密碼加密] 選項，請鍵入並確認密碼。  
  
9. 按一下 [確定] 以完成匯入。  
  
### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來匯出封裝  
  
1.  按一下 [開始]、指向 [Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]，然後按一下 [SQL Server Management Studio]。  
  
2.  在 [連接到伺服器] 對話方塊上，設定下列選項：  
  
    -   在 [伺服器類型] 方塊中，選取 [Integration Services]。  
  
    -   在 [伺服器名稱] 方塊中提供伺服器名稱，或按一下 [\<瀏覽其他...>]，並尋找要使用的伺服器。  
  
3.  如果物件總管尚未開啟，請在 [檢視] 功能表上，按一下物件總管。  
  
4.  在物件總管中，展開 [存放的封裝] 資料夾。  
  
5.  展開子資料夾，以找出您要匯出的封裝。  
  
6.  以滑鼠右鍵按一下封裝，再按一下 [匯出]，然後執行下列其中之一：  
  
    -   若要匯出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，請選取 [SQL Server] 選項，然後指定伺服器並選取驗證模式。 如果選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱和密碼。  
  
         按一下瀏覽按鈕 ([...]) 並展開 [SSIS 封裝] 資料夾，以找出您要儲存封裝的資料夾。 (選擇性) 更新封裝的預設名稱並按一下 [確定]。  
  
    -   若要匯出至檔案系統，請選取 [檔案系統] 選項。  
  
         按一下瀏覽按鈕 ([...]) 找出您要匯出封裝的目標資料夾、輸入封裝檔案的名稱，然後按一下 [儲存]。  
  
    -   若要匯出至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區，請選取 [SSIS 封裝存放區] 選項，並指定伺服器。  
  
         按一下瀏覽按鈕 ([...])，展開 [SSIS 封裝] 資料夾，並選取您要儲存封裝的資料夾。 (選擇性) 在 [封裝名稱] 文字方塊中輸入封裝的新名稱。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  若要更新封裝的保護等級，請按一下瀏覽按鈕 ([...])，並使用 [封裝保護等級] 對話方塊選擇其他保護等級。 如果選取 [機密資料以密碼加密] 或 [所有資料以密碼加密] 選項，請鍵入並確認密碼。  
  
8.  按一下 [確定] 以完成匯出。  

## <a name="import-package-dialog-box-ui-reference"></a>匯入封裝對話方塊 UI 參考
  使用 **[匯入封裝]** 對話方塊 (可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]存取)，即可匯入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，並設定或修改封裝的保護等級。  
  
### <a name="options"></a>選項。  
 **封裝位置**  
 選取要匯入封裝之儲存位置的類型。 下列是可以使用的選項：  
  
 **SQL Server**  
  
 **檔案系統**  
  
 **SSIS 封裝存放區**  
  
 **Server**  
 輸入伺服器名稱，或者從清單中選取一個伺服器。  
  
 **驗證**  
 選取 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 唯有儲存位置是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
> [!IMPORTANT]  
>  可能的話，請使用 Windows 驗證。  
  
 **驗證類型**  
 選取驗證類型。  
  
 **User name**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱。  
  
 **密碼**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供密碼。  
  
 **封裝路徑**  
 輸入封裝路徑，或按一下瀏覽按鈕 ([...])，然後找出封裝。  
  
 **封裝名稱**  
 選擇性地重新命名封裝。 預設名稱是要匯入的封裝名稱。  
  
 **保護等級**  
 按一下瀏覽按鈕 ([...]) 並更新 [封裝保護等級] 對話方塊中的保護等級。 如需詳細資訊，請參閱 [封裝與專案保護等級對話方塊](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)。  

## <a name="export-package-dialog-box-ui-reference"></a>匯出封裝對話方塊 UI 參考
  使用 **[匯出封裝]** 對話方塊 (可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中存取)，即可匯出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝到不同的位置，並選擇性地修改封裝的保護等級。  
  
### <a name="options"></a>選項。  
 **封裝位置**  
 選取要用來儲存所匯出之封裝的儲存體類型。 下列是可以使用的選項：  
  
 **SQL Server**  
  
 **[File System]**  
  
 **SSIS 封裝儲存體**  
  
 **Server**  
 輸入伺服器名稱，或者從清單中選取一個伺服器。  
  
 **驗證**  
 選取 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 唯有儲存位置是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
> [!IMPORTANT]  
>  可能的話，請使用 Windows 驗證。  
  
 **驗證類型**  
 選取驗證類型。  
  
 **User name**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱。  
  
 **密碼**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請提供密碼。  
  
 **封裝路徑**  
 輸入封裝路徑，或按一下瀏覽按鈕 ([...])，並找出要儲存封裝的資料夾。  
  
 **保護等級**  
 按一下瀏覽按鈕 ([...]) 並更新 [封裝保護等級] 對話方塊中的保護等級。 如需詳細資訊，請參閱 [封裝與專案保護等級對話方塊](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#protection_dialog)。  

## <a name="back-up-and-restore-packages"></a>備份和還原套件
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝可以儲存至檔案系統或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫 msdb。 儲存至 msdb 的封裝可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份和還原功能進行備份和還原。  
  
 如需備份和還原 msdb 資料庫的詳細資訊，請按一下下列主題之一：  
  
-   [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [系統資料庫的備份與還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含可用來管理封裝的 **dtutil** 命令提示公用程式 (dtutil.exec)。 如需詳細資訊，請參閱 [dtutil Utility](../../integration-services/dtutil-utility.md)。  
  
### <a name="configuration-files"></a>組態檔  
 封存包含的所有組態檔都儲存在檔案系統中。 備份 msdb 資料庫時並不會備份這些檔案；因此，作為儲存至 msdb 之封裝保護計畫的一部份，您應確保定期備份組態檔。 若要在 msdb 資料庫的備份中包含組態，應考慮使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態類型而不是以檔案為基礎的組態。  
  
### <a name="packages-stored-in-the-file-system"></a>儲存在檔案系統中的封裝  
 儲存至檔案系統之封裝的備份應納入備份伺服器檔案系統的計畫中。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務組態檔 (預設名稱為 MsDtsSrvr.ini.xml) 會列出服務監視之伺服器上的資料夾。 您應確定已備份這些資料夾。 另外，封裝也可能儲存在伺服器上的其他資料夾中，您應確保在備份中包含這些資料夾。  

## <a name="see-also"></a>另請參閱  
 [Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/integration-services-service-ssis-service.md)  
  
  
