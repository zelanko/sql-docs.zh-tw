---
title: "Analysis Services 資料庫的備份和還原 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.Restore.f1
- sql13.asvs.ssmsimbi.Backup.f1
helpviewer_keywords:
- backing up databases [Analysis Services]
- encryption [Analysis Services]
- databases [Analysis Services], restoring
- cryptography [Analysis Services]
- databases [Analysis Services], backing up
- restoring databases [Analysis Services]
- recovery [Analysis Services]
ms.assetid: 947eebd2-3622-479e-8aa6-57c11836e4ec
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: a3ca95b34e684fa5ec67d0dab4720020a0e4e883
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="backup-and-restore-of-analysis-services-databases"></a>備份與還原 Analysis Services 資料庫
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包括備份與還原，讓您可以從特定時間點復原資料庫及其物件。 備份與還原也是一種有效的技術，可將資料庫移轉到升級的伺服器、在伺服器之間移動資料庫，或是將資料庫部署到實際伺服器。 如果您還沒有備份計畫，但是您有很重要的資料，就應該盡快設計及實作計畫，以供資料復原之用。  
  
 備份與還原命令是在已部署的 Analysis Services 資料庫上執行。 針對您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的專案和方案，您應該使用原始檔控制來確保您可以復原特定版本的來源檔案，然後為您要使用之原始檔控制系統的儲存機制，建立資料復原計畫。  
  
 針對包含來源資料的完整備份，您必須備份包含詳細資料的資料庫。 更明確地說，如果您使用 ROLAP 或 DirectQuery 資料庫儲存，詳細資料會儲存在與 Analysis Services 資料庫分開的外部 SQL Server 關聯式資料庫中。 否則，如果所有物件都是表格式或多維度，Analysis Services 備份就會包含中繼資料和來源資料。  
  
 自動備份的一個明顯好處，就是資料快照集可以按照自動備份頻率，保持在最新的狀態。 自動排程器可確保不會忘記備份。 還原資料庫也可以自動化，且是複寫資料的好方法，但一定要在您複寫至的執行個體上備份加密金鑰檔案。 同步處理功能是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的複寫專用，但僅針對過期的資料。 此處提到的所有功能可以透過使用者介面、利用 XML/A 命令或透過 AMO 以程式設計方式執行來實作。 如需備份策略的詳細資訊，請參閱 [SQL Server 2005 Analysis Services 的備份策略](http://go.microsoft.com/fwlink/?LinkId=81888)。  
  
 本主題包含下列各節：  
  
-   [準備備份](#bkmk_prep)  
  
-   [備份多維度或表格式資料庫](#bkmk_cube)  
  
-   [還原 Analysis Services 資料庫](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> 必要條件  
 您必須具有 Analysis Services 執行個體的管理權限，或在要備份的資料庫上擁有「完整控制權 (管理員)」權限。  
  
 還原位置相較於取得備份的來源執行個體而言，必須是相同版本或更新版本的 Analysis Services 執行個體。 雖然您無法將 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體中的資料庫還原到舊版的 Analysis Services，但是在較新的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體上還原舊版資料庫 (例如 SQL Server 2012) 是常見的做法。  
  
 還原位置必須具有相同的伺服器類型。 表格式資料庫只能還原到以表格式模式執行的 Analysis Services。 多維度資料庫需要在多維度模式下執行的執行個體。  
  
##  <a name="bkmk_prep"></a> 準備備份  
 請使用下列檢查清單來準備備份：  
  
-   檢查將儲存備份檔案的位置。 如果您使用遠端位置，必須將它指定為 UNC 資料夾。 確認您可以存取此 UNC 路徑。  
  
-   檢查資料夾的權限，以確保 Analysis Services 服務帳戶有資料夾的讀取/寫入權限。  
  
-   檢查目標伺服器上是否有足夠的磁碟空間。  
  
-   檢查現有檔案是否有相同名稱。 如果同名的檔案已經存在，備份將會失敗，除非您指定覆寫檔案的選項。  
  
##  <a name="bkmk_cube"></a> 備份多維度或表格式資料庫  
 系統管理員可以將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫備份至單一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 備份檔 (.abf)，而不用考慮資料庫的大小。 如需逐步指示，請參閱 [如何備份 Analysis Services 資料庫 (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) 和 [自動備份 Analysis Services 資料庫 (TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html)。  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)](用來在 SharePoint 環境中載入和查詢 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料模型) 會從 SharePoint 內容資料庫載入其模型。 這些內容資料庫為關聯式，而且會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫引擎上執行。 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料模型沒有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 備份和還原策略。 如果您已經針對 SharePoint 內容設定災害復原計畫，此計畫會包含內容資料庫中所儲存的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料模型。  
  
 **遠端資料分割**  
  
 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫包含遠端資料分割，也應該備份遠端資料分割。 備份含有遠端資料分割的資料庫時，每一個遠端伺服器上的所有遠端資料分割都會分別備份到每一個遠端伺服器上的單一檔案。 因此，如果您想要從個別的主機電腦上建立那些遠端備份，就必須手動將那些檔案複製到指定的儲存區。  
  
 **備份檔案的內容**  
  
 備份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫會產生備份檔案，其內容因資料庫物件所使用的儲存模式而異。 備份內容的差異肇因於這樣的事實：每一個儲存模式實際上在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫內儲存不同的資訊集。 例如，多維度混合式 OLAP (HOLAP) 資料分割和維度會將彙總和中繼資料儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中，而關聯式 OLAP (ROLAP) 資料分割和維度只會將中繼資料儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。 因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的實際內容根據每一個資料分割的儲存模式而有所不同，所以備份檔案的內容也不一樣。 下表使備份檔案的內容與物件所使用的儲存模式產生關聯。  
  
|儲存模式|備份檔案的內容|  
|------------------|-----------------------------|  
|多維度 MOLAP 分割區和維度|中繼資料、來源資料和彙總|  
|多維度 HOLAP 分割區和維度|中繼資料和彙總|  
|多維度 ROLAP 分割區和維度|中繼資料|  
|表格式記憶體中模型|中繼資料和來源資料|  
|表格式 DirectQuery 模型|僅限中繼資料|  
  
> [!NOTE]  
>  備份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫不會備份基礎資料來源中的資料，例如關聯式資料庫。 只備份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的內容。  
  
 當您備份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，可以從下列選項中選擇：  
  
-   是否壓縮所有資料庫備份。 預設為壓縮備份。  
  
-   是否要加密備份檔案的內容以及在解密和還原檔案之前要求密碼。 根據預設，不加密備份資料。  
  
    > [!IMPORTANT]  
    >  對於每個備份檔案，執行備份命令的使用者必須擁有寫入針對每個檔案所指定之備份位置的權限。 此外，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將備份之資料庫上擁有「完整控制 (系統管理員)」權限的資料庫角色成員。  
  
 如需備份 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的詳細資訊，請參閱 [備份選項](../../analysis-services/multidimensional-models/backup-options.md)。  
  
##  <a name="bkmk_restore"></a> 還原 Analysis Services 資料庫  
 管理員可以從一個或多個備份檔案還原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
> [!NOTE]  
>  如果有加密備份檔案，在您使用該檔案來還原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫之前，必須提供備份期間所指定的密碼。  
  
 在還原期間，您有下列選項：  
  
-   您可以使用原始資料庫名稱來還原資料庫，或指定新的資料庫名稱。  
  
-   您可以覆寫現有的資料庫。 如果您選擇要覆寫資料庫，則必須明確指定您要覆寫現有的資料庫。  
  
-   您可以選擇是否要還原現有的安全性資訊，或略過安全性成員資格資訊。  
  
-   您可以選擇由還原命令變更每一個要還原之分割區的還原資料夾。 本機資料分割可以還原至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的任何本機資料夾位置，資料庫即還原至此處。 遠端分割區可以還原至本機伺服器以外之任何伺服器上的任何資料夾；遠端分割區無法變成本機式。  
  
    > [!IMPORTANT]  
    >  對於每個備份檔案，執行還原命令的使用者必須擁有從針對每個檔案所指定之備份位置讀取的權限。 若要還原沒有安裝在伺服器上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，使用者也必須是該 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員。 若要覆寫 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，使用者必須具有下列其中一個角色： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體之伺服器角色的成員，或在即將還原之資料庫上擁有完整控制權 (管理員) 權限的資料庫角色成員。  
  
    > [!NOTE]  
    >  還原現有的資料庫之後，還原資料庫的使用者可能會喪失已還原資料庫的存取權。 如果在執行備份時，使用者不是伺服器角色的成員，也不是擁有完整控制權 (管理員) 權限的資料庫角色成員，就可能會發生存取權喪失的情況。  
  
 如需還原 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的詳細資訊，請參閱 [還原選項](../../analysis-services/multidimensional-models/restore-options.md)。  
  
## <a name="see-also"></a>另請參閱  
 [備份、還原和同步處理資料庫 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   

  
  
