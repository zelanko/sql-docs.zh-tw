---
title: 升級報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c8330266babdb260f80843213ddb892021eb8c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63064084"
---
# <a name="upgrade-reports"></a>Upgrade Reports
  報表定義 (.rdl) 檔案會藉由下列方式自動升級：  
  
-   當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的報表設計師中開啟報表時，報表定義將會升級為目前支援的 RDL 結構描述。 在專案屬性中指定 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 報表伺服器時，報表定義會儲存在與目標伺服器相容的結構描述中。  
  
-   將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝升級為 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 安裝時，已經發行到報表伺服器的現有報表和快照集會在初次處理時，編譯並自動升級為新的結構描述。 如果無法自動升級報表，則會使用回溯相容性模式來處理報表。 報表定義會保留在原本的結構描述中。  
  
 當您直接將報表定義檔案上傳到報表伺服器或 SharePoint 網站時，報表並不會升級。 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中升級報表定義是升級 .rdl 檔的唯一方式。  
  
 在本機或報表伺服器上升級報表之後，您可能會發現其他錯誤、警告和訊息。 這是內部報表物件模型的變更和處理元件的結果，造成偵測到報表中的根本問題時出現訊息。 如需詳細資訊，請參閱 [Reporting Services Backward Compatibility](../reporting-services-backward-compatibility.md)。  
  
 如需有關新功能[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]，請參閱 <<c2> [ 的新&#40;Reporting Services&#41;](../what-s-new-reporting-services.md)。</c2>  
  
 本主題內容：  
  
-   [升級支援的版本](#bkmk_versionsupported)  
  
-   [報表定義檔 (.rdl) 和報表設計師](#bkmk_rdlfiles)  
  
-   [已發行的報表和報表快照集](#bkmk_publishedreports_and_snapshots)  
  
-   [回溯相容性模式](#bkmk_backcompat)  
  
-   [升級具有子報表的報表](#bkmk_subreports)  
  
-   [升級具有自訂報表項目的報表](#bkmk_CRIs)  
  
-   [轉換 CRI 對話方塊](#bkmk_convertCRIdialog)  
  
##  <a name="bkmk_versionsupported"></a> 升級支援的版本  
 在任何舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中建立的報表都可以升級。 這包括以下版本：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 Service Pack 1  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 Service Pack 2  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> 報表定義檔 (.rdl) 和報表設計師  
 報表定義檔案包含 RDL 命名空間的參考，其中指定了用來驗證 .rdl 檔的報表定義結構描述版本。  
  
 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的報表設計師中開啟 .rdl 檔時，如果此報表是針對先前的命名空間所建立，報表設計師就會自動建立備份檔案，並且將此報表升級至目前的命名空間。 這是升級報表定義檔案的唯一方式。  
  
 您設定的部署屬性會影響儲存報表定義檔案的結構描述。 如需詳細資訊，請參閱 [SQL Server Data Tools 中的部署和版本支援 &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
 您可以將舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中建立的 .rdl 檔案上傳到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器，而且第一次使用檔案時就會自動升級。 報表伺服器會使用原始格式儲存報表定義檔案。 初次檢視報表時會自動升級報表，但是已儲存的報表定義檔案則維持不變。  
  
> [!NOTE]  
>  您無法將具有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表定義命名空間的報表發行或上傳到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 報表伺服器。  
  
 若要針對報表、報表伺服器或報表設計師識別目前的 RDL 結構描述，請參閱[尋找報表定義結構描述版本 &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md)。  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> 已發行的報表和報表快照集  
 在初次使用時，報表伺服器會嘗試將現有已發行的報表和報表快照集升級到新的報表定義結構描述，您不需要執行任何特定動作。 當使用者檢視報表或報表快照集，或是報表伺服器處理訂閱時，就會嘗試進行升級。 報表定義不會被取代，而是繼續儲存在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 報表伺服器上的原始結構描述中。 如果無法升級報表，則會使用回溯相容性模式來執行報表。  
  
##  <a name="bkmk_backcompat"></a> 回溯相容性模式  
 已成功升級的報表會由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理。 會處理無法升級報表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]報表處理器在回溯相容性模式。 不能同時使用這兩種報表處理器來處理報表。 初次使用時會成功升級報表，或是將報表標示為可提供回溯相容性。  
  
 只有 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表器才支援新功能。 如果無法升級報表，您仍然可以檢視轉譯的報表，但是無法使用新的功能。 若要充分利用新的功能，則必須成功升級報表。  
  
##  <a name="bkmk_subreports"></a> 升級具有子報表的報表  
 當報表包含子報表時，升級期間會發生以下四種可能狀態的其中一種：  
  
-   可以成功升級主報表和所有子報表。 它們是由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理。  
  
-   無法升級主報表和所有子報表。 它們是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器所處理。  
  
-   可以升級主報表，但是無法升級其中一或多個子報表。 主報表由處理[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]報表處理器，但是轉譯的報表會顯示訊息 「 錯誤：子報表無法處理 」 中會顯示無法升級子報表的位置。  
  
-   無法升級主報表，但是可以升級其中一或多個子報表。 主報表由處理[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]報表處理器，但是轉譯的報表會顯示訊息 「 錯誤：子報表無法處理 」 中會顯示子報表的位置。  
  
 如果您看到錯誤 「 錯誤：無法處理子報表 」，您必須變更主報表或子報表的定義，使報表可由相同的報表處理器版本處理。  
  
 鑽研報表沒有這項限制，因為鑽研報表會當做獨立報表來處理。  
  
##  <a name="bkmk_CRIs"></a> 升級具有自訂報表項目的報表  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表可能包含軟體協力廠商所提供以及系統管理員針對報表撰寫電腦和報表伺服器所安裝的自訂報表項目 (CRI)。 包含 CRI 的報表可透過以下方式來升級：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器會升級到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器。 報表伺服器上已發行的報表會在第一次使用時自動升級。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表會上傳到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器。 報表會在第一次使用時自動升級。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的報表設計師中開啟 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]報表。 隨即建立原始報表的備份副本。 而且會發生以下兩種情況的其中一種：  
  
    1.  報表中的所有 CRI 都沒有任何不支援的功能。 CRI 會轉換成新報表定義結構描述內的報表項目，好讓整個報表可以升級。 如果您儲存檔案，它就會儲存在目前的 RDL 命名空間中。  
  
    2.  報表中的一或多個 CRI 具有不支援的功能。 隨即出現一個對話方塊，提示使用者是要轉換 CRI 還是將其維持不變。  
  
     如需詳細資訊，請參閱本主題稍後的「 [在報表設計師中開啟報表](#OpeningaReport) 」。  
  
 如需針對報表伺服器、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或報表識別目前 RDL 命名空間的資訊，請參閱[尋找報表定義結構描述版本 &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md)。  
  
### <a name="upgrading-reports-on-a-report-server"></a>升級報表伺服器上的報表  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表第一次在已經升級至 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器的報表伺服器上執行時，此報表會自動升級到目前報表伺服器所支援的報表定義命名空間。 報表在升級之前可能已經存在於報表伺服器上，或者報表可能已經透過報表管理員上傳，或是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中從報表設計師發行到報表伺服器。  
  
 下表列出報表伺服器針對報表中特定類型的 CRI 所執行的升級動作。  
  
|CRI 類型|報表伺服器升級動作|  
|--------------|----------------------------------|  
|協力廠商 CRI|未執行升級。<br /><br /> 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器所處理。|  
|沒有不支援之功能的 Dundas 2005 圖表 CRI|升級至最新的 RDL 結構描述。 所有 Dundas 2005 圖表 CRI 都會轉換成與 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]相容的圖表資料區域。<br /><br /> 由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理。|  
|沒有不支援之功能的 Dundas 2005 量測計 CRI|升級至最新的 RDL 結構描述。 所有 Dundas 2005 量測計 CRI 都會轉換成與 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 相容的量測計資料區域。<br /><br /> 由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理。|  
|具有不支援之功能的 Dundas 2005 圖表 CRI|未執行升級。<br /><br /> 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器所處理。|  
|具有不支援之功能的 Dundas 2005 量測計 CRI|未執行升級。<br /><br /> 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器所處理。|  
  
###  <a name="OpeningaReport"></a> 使用報表設計師開啟具有 CRI 的報表  
 當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的報表設計師中開啟具有 CRI 的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]報表時，該報表將會升級到新的報表定義結構描述。 根據報表中所包含的 CRI 而異，將會發生以下其中一個動作：  
  
-   偵測到協力廠商 CRI。 如果安裝於報表撰寫電腦上的 CRI 版本與新的 RDL 結構描述不相容，則設計介面會顯示一個有紅色 X 的文字方塊。您必須聯繫系統管理員，才能安裝協力廠商所提供而且與新 RDL 結構描述相容的新版 CRI。  
  
-   偵測到 Dundas 2005 圖表或量測計 CRI 且所有執行個體都包含支援的功能。 所有 Dundas 2005 圖表和量測計 CRI 都會轉換成您在工具箱上看到的 Reporting Services 圖表和量測計報表項目。 這些稱為原生報表和量測計報表項目。  
  
-   偵測到 2005 圖表或量測計 CRI，而且任何執行個體都有不支援的功能。 本章節之後將會描述不支援的功能。 您可以選擇是否要將所有 CRI 轉換成原生報表項目。  
  
    -   如果您要轉換，此報表會升級到新的 RDL 結構描述，而且 Dundas 2005 圖表和量測計 CRI 會轉換成對應的原生報表和量測計報表項目，但是會移除不支援的功能。 在轉譯的報表中，您可能會看到 CRI 顯示的方式有些差異。  
  
    -   如果您選擇不要轉換，報表會升級到新的 RDL 結構描述，但是 CRI 會視為協力廠商 CRI。 您必須與系統管理員和協力廠商一起合作，才能安裝與新報表結構描述相容的新 CRI。 如果無法使用新的 CRI，報表會在報表設計師中顯示一個有紅色 X 的文字方塊。  
  
 在報表撰寫環境中升級報表之後加以儲存是將現有報表升級到新報表定義結構描述的唯一方式。  
  
### <a name="unsupported-dundas-2005-chart-custom-report-item-functionality"></a>不支援的 Dundas 2005 圖表自訂報表項目功能  
 Dundas 2005 圖表 CRI 不支援的功能包括以下項目：  
  
-   註解。  
  
-   自訂圖例項目。  
  
-   具有以下名稱的自訂屬性：  
  
    -   CUSTOM_CODE_CS  
  
    -   CUSTOM_CODE_VB  
  
    -   CUSTOM_CODE_COMPILED_ASSEMBLY  
  
         例如，如果 .rdl 檔案包含以下區段，您就需要在升級之前加以移除：  
  
        ```  
        <CustomProperty>  
         <Name>CUSTOM_CODE_CS</Name>  
         <Value>dXNpWERwegfdfgiobxxl3bmc... </Value>  
        </CustomProperty>  
        ```  
  
### <a name="unsupported-dundas-2005-gauge-custom-report-item-functionality"></a>不支援的 Dundas 2005 量測計自訂報表項目功能  
 Dundas 2005 量測計 CRI 不支援的功能包括以下項目：  
  
-   數值指標。  
  
-   狀態指標。  
  
-   自訂影像。  
  
###  <a name="bkmk_convertCRIdialog"></a> 轉換 CRI 對話方塊  
 此報表包含自訂報表項目 (CRI) 與不支援的功能。 CRI 是報表定義語言 (RDL) 的延伸模組，支援在報表中顯示資料的自訂物件。 CRI 包括軟體協力廠商所提供的設計階段和執行階段元件。  
  
> [!NOTE]  
>  選擇在報表伺服器上支援自訂報表項目是由系統管理員所做的決定。 若要檢視報表中的 CRI，必須在報表撰寫用戶端上安裝 CRI 元件才能預覽報表，並在報表伺服器上檢視已發行或已上傳的報表。 如需詳細資訊，請參閱 [自訂報表項目](../custom-report-items/custom-report-items.md) 以及軟體協力廠商的文件。  
  
 某些 CRI 可以轉換成新報表定義格式的報表項目。 如需可以轉換之 CRI 的清單，請參閱＜ [Upgrading Reports](upgrade-reports.md)＞。 利用下列清單，決定是否轉換此報表中的 CRI。  
  
-   **是** ：選擇 **[是]** ，在可能的情況下轉換報表中的所有 CRI。 在 CRI 中不支援的功能無法升級，而且會從報表定義檔案中移除。 如需不支援之功能的清單，請參閱＜ [Upgrading Reports](upgrade-reports.md)＞。 檢視報表時，您可能會看到 CRI 在報表中顯示的方式有些差異。  
  
-   **否** ：當您不要轉換報表中的 CRI 時，選擇 **[否]** 。 這些 CRI 無法透過報表處理器顯示在其目前的版本中。 如果您的系統管理員打算安裝軟體協力廠商所提供，而且與新報表定義格式相容的新版 CRI，您應該選擇 **[否]**。 在新版本提供之前，CRI 會在報表中顯示為一個有紅色 X 的空文字方塊。  
  
 在任一種情況下，報表會升級到新的報表定義格式，並將原始報表的備份複本儲存為 *\<報表名稱>* `-` Backup.rdl。 如果您以報表撰寫工具儲存報表，您就是以新的報表定義格式儲存升級的報表。 如果您發行報表，此報表會先儲存在您的電腦中，然後再發行到報表伺服器。 您會將升級版本的報表發行至報表伺服器。  
  
 如果您沒有儲存報表，原始報表就會維持不變。 不過，您無法在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，或使用較新版本報表定義格式的報表撰寫環境中編輯此報表。 您可以使用報表管理員將原始版本的報表上傳到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器，藉此執行該報表。 如需詳細資訊，請參閱[上傳檔案或報表 &#40;報表管理員&#41;](../reports/upload-a-file-or-report-report-manager.md)。  
  
 對於您上傳 (而非發行) 到報表伺服器的報表，報表處理器會決定是否可以在第一次使用時升級報表。 無法升級的報表會在回溯相容性模式下處理，而且會如同在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中繼續顯示。  
  
## <a name="see-also"></a>另請參閱  
 [升級和移轉 Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [SQL Server Reporting Services SQL Server 2014 中的重大變更](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server Reporting Services SQL Server 2014 中的行為變更](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [SQL Server Reporting Services SQL Server 2014 中已停止的功能](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [自訂報表項目](../custom-report-items/custom-report-items.md)   
 [升級報表伺服器資料庫](upgrade-a-report-server-database.md)  
  
  
