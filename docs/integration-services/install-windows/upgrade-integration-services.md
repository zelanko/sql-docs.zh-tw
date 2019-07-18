---
title: 升級 Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, upgrading
- SSIS, upgrading
- SQL Server Integration Services, upgrading
- upgrading Integration Services
ms.assetid: 04f9863c-ba0b-47c5-af91-f2d41b078a23
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.openlocfilehash: 1c5e56d0ed0d422770311ba8135992c4254370a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65805402"
---
# <a name="upgrade-integration-services"></a>升級 Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  如果您的電腦上目前安裝有 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 或更新版本，您可以升級到 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]。  
  
 如果您在安裝其中一個舊版 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 的電腦上升級到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，則 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 會與舊版並存安裝。  
  
 有多個版本的 dtexec 公用程式會隨著這個並行安裝一併安裝。 為確保您執行正確的公用程式版本，請在命令提示字元中輸入完整路徑 (\<磁碟機>:\Program Files\Microsoft SQL Server\\<版本\>\DTS\Binn) 來執行公用程式。 如需有關 dtexec 的詳細資訊，請參閱＜ [dtexec Utility](../../integration-services/packages/dtexec-utility.md)＞。  
  
> [!NOTE]  
>  在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，Users 群組中的所有使用者預設都能存取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，使用者則無法存取 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務。 因此，服務預設是安全的。 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員必須執行 DCOM 組態工具 (Dcomcnfg.exe)，授與特定使用者 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務的存取權限。 如需詳細資訊，請參閱 [Integration Services Service &#40;SSIS Service&#41;](../../integration-services/service/integration-services-service-ssis-service.md) (Integration Services 服務 (SSIS 服務))。  
  
## <a name="before-upgrading-integration-services"></a>在升級 Integration Services 之前  
 我們建議您在升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之前，最好先執行 Upgrade Advisor。 Upgrade Advisor 會報告當您將現有的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝移轉至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所使用的新封裝格式時可能會遇到的問題。  
  
> [!NOTE]
>  在 SQL Server 2012 中，已停用為移轉或執行 Data Transformation Services (DTS) 套件所提供的支援。 下列 DTS 功能已停用：  
> 
>  -   DTS 執行階段  
> -   DTS API  
> -   可將 DTS 封裝移轉到下一版 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   DTS 封裝維護的支援 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   執行 DTS 2000 封裝工作  
> -   DTS 封包的 Upgrade Advisor 掃描。  
> 
>  如需其他已停止功能的相關資訊，請參閱 [SQL Server 2016 中已停止的 Integration Services 功能](https://msdn.microsoft.com/library/5ee40ceb-37b9-47a9-b90d-ce1de74b10f7)。  
  
## <a name="upgrading-integration-services"></a>升級 Integration Services  
 您可以使用以下其中一個方法來升級：  
  
-   執行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式，並選取**從 SQL Server 2008、SQL Server 2008 R2、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** 升級的選項。  
  
-   在命令提示字元上執行 **setup.exe**，並指定 **/ACTION=upgrade** 選項。 如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md) 中的＜[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的安裝指令碼＞一節。  
  
 您無法使用升級作業來執行下列動作：  
  
-   重新設定現有的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]安裝。  
  
-   從 32 位元移到 64 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或是從 64 位元版本移到 32 位元版本。  
  
-   將某個當地語系化的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本移到另一個當地語系化的版本。  
  
 當您升級時，可以同時升級 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，或是只升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 如果只升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，雖然 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 或更新版本仍可運作，但是沒有 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]的功能。 如果您只升級 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]，雖然 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 可完整運作，但是除非另一部電腦提供了 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] 的執行個體，否則就只能將封裝儲存在檔案系統中。  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>將 Integration Services 和 Database Engine 都升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 本章節描述執行具有以下準則之升級的作用：  
  
-   您同時將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體位於相同的電腦上。  
  
### <a name="what-the-upgrade-process-does"></a>升級程序執行的工作  
 升級程序會執行以下工作：  
  
-   安裝 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 檔案、服務和工具 ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)])。 如果同一部電腦上有多個 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的執行個體，在您第一次將任何執行個體升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，會安裝 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 檔案、服務和工具。  
  
-   將 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本。  
  
-   將資料從 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 或更新的系統資料表移到 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 系統資料表，如下所示：  
  
    -   將封裝從 msdb.dbo.sysdtspackages90 系統資料表移到 msdb.dbo.sysssispackages 系統資料表，而不變更封裝。  
  
        > [!NOTE]  
        >  雖然資料會移到不同的系統資料表，但是升級程序並不會將封裝移轉至新的格式。  
  
    -   將資料夾中繼資料從 msdb.sysdtsfolders90 系統資料表移到 msdb.sysssisfolders 系統資料表。  
  
    -   將記錄資料從 msdb.sysdtslog90 系統資料表移到 msdb.sysssislog 系統資料表。  
  
-   將資料移到新的 msdb.sysssis\* 資料表之後，移除 msdb.sysdts*90 系統資料表以及用於存取這些資料表的預存程序。 不過，升級會將 sysdtslog90 資料表取代成也名為 sysdtslog90 的檢視表。 這個新的 sysdtslog90 檢視表會公開新的 msdb.sysssislog 系統資料表。 這樣可確保以記錄資料表為基礎的報表會繼續執行而不中斷。  
  
-   為了控制封裝的存取權，建立三個新的固定資料庫層級角色：db_ssisadmin、db_ssisltduser 和 db_ssisoperator。 雖然不會移除 db_dtsadmin、db_dtsltduser 和 db_dtsoperator 的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 角色，但是它們會成為對應新角色的成員。  
  
-   如果 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝存放區 (也就是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務所管理的檔案系統位置) 是 **\SQL Server\90**、 **\SQL Server\100**、 **\SQL Server\110**或 **\SQL Server\120** 下的預設位置，請將這些封裝移到 **\SQL Server\130**下的新預設位置。  
  
-   將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服務組態檔更新為指向升級的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體。  
  
### <a name="what-the-upgrade-process-does-not-do"></a>升級程序不會執行的工作  
 升級程序不會執行以下工作：  
  
-   **不會** 移除 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 或更新的服務。  
  
-   不會將現有的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝移轉至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所使用的新封裝格式。 如需如何移轉封裝的相關資訊，請參閱 [升級 Integration Services 封裝](../../integration-services/install-windows/upgrade-integration-services-packages.md)。  
  
-   不會移動已經加入至服務組態檔之檔案系統位置 (預設位置除外) 中的封裝。 如果您先前已經編輯了系統組態檔以加入其他檔案系統資料夾，儲存在這些資料夾中的封裝將不會移至新的位置。  
  
-   在直接呼叫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dtexec **公用程式 (dtexec.exe) 的** 代理程式作業步驟中，不會更新 **dtexec** 公用程式的檔案系統路徑。 您必須手動編輯這些作業步驟來更新檔案系統路徑，以便指定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dtexec **公用程式的** 位置。  
  
### <a name="what-you-can-do-after-upgrading"></a>升級之後可以執行的工作  
 當升級程序完成之後，您可以執行以下工作：  
  
-   執行可執行封裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。  
  
-   使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來管理儲存於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]執行個體中的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]封裝。 您必須修改服務設定檔，才可將 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體加入此服務所管理的位置清單。  
  
    > [!NOTE]  
    >  舊版 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 無法連接到 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 服務。  
  
-   檢查 packageformat 資料行中的值，以識別 msdb.dbo.sysssispackages 系統資料表中的封裝版本。 此資料表有一個 packageformat 資料行可識別每一個封裝的版本。 值為 3 表示 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 封裝。 在您將封裝移轉至新的封裝格式之前，packageformat 資料行中的值都不會變更。  
  
-   您無法使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 工具設計、執行或管理 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 工具包含各自對應的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]版本、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈，以及封裝執行公用程式 (dtexecui.exe)。 升級程序並不會移除 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]工具。 不過，您無法在已經升級的伺服器上使用這些工具來繼續使用 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 或更新的封裝。  
  
-   依預設，在升級安裝中， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會設定為將與封裝執行相關的事件記錄至應用程式事件記錄檔。 當您使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的資料收集器功能時，這個設定可能會產生過多的事件記錄項目。 記錄的事件包括 EventID 12288 "封裝已啟動" 和 EventID 12289 "封裝已成功完成"。 若要停止將這兩個事件記錄到應用程式事件記錄檔，請開啟登錄進行編輯。 在登錄中找出 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS 節點，然後將 LogPackageExecutionToEventLog setting 設定的 DWORD 值從 1 變更為 0。  
  
## <a name="upgrading-only-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>只將 Database Engine 升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 本章節描述執行具有以下準則之升級的作用：  
  
-   您只要升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。 也就是說， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體現在是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的執行個體，但是 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的執行個體和用戶端工具是來自 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體位於某部電腦上，而 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和用戶端工具則位於另一部電腦上。  
  
### <a name="what-you-can-do-after-upgrading"></a>升級之後可以執行的工作  
 將封裝儲存於已升級之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中的系統資料表，與 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中所用的系統資料表不同。 因此， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 無法在已升級之 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體上的系統資料表內找到封裝。 由於找不到這些封裝，所以可以對這些封裝處理的動作也會受到限制：  
  
-   您無法使用其他電腦上的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 工具 ( [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)])，從已升級的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體載入或管理封裝。  
  
    > [!NOTE]  
    >  雖然已升級之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中的封裝尚未移轉成新的封裝格式，但是 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 工具還是無法找到這些封裝。 因此， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 工具無法使用這些封裝。  
  
-   您無法使用其他電腦上的 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 來執行已升級之 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體上的 msdb 內所儲存的封裝。  
  
-   您無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 代理程式作業來執行已升級之 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 執行個體中所儲存的 [!INCLUDE[ssDE](../../includes/ssde-md.md)]封裝。  
  
## <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章： [在 Denali 中製作現有的自訂 SSIS 延伸模組和應用程式工作](https://go.microsoft.com/fwlink/?LinkId=238157)。  
  
  
