---
title: 升級報表 | Microsoft Docs
ms.date: 06/04/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
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
ms.openlocfilehash: bae0cffce8cfacd56feaab289d75b7c70d509ce7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082279"
---
# <a name="upgrade-reports-ssrs"></a>升級報表 (SSRS)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

報表定義 (.rdl) 檔案會藉由下列方式自動升級：  
  
-   當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的報表設計師中開啟分頁報表時，報表定義將會升級為目前支援的 RDL 結構描述。 在專案屬性中指定 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 報表伺服器時，報表定義會儲存在與目標伺服器相容的結構描述中。  
  
-   將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝升級為 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 安裝時，已經發行到報表伺服器的現有報表和快照集會在初次處理時，編譯並自動升級為新的結構描述。 如果無法自動升級報表，則會使用回溯相容性模式來處理報表。 報表定義會保留在原本的結構描述中。  
  
 在本機或報表伺服器上升級報表之後，您可能會發現其他錯誤、警告和訊息。 這是內部報表物件模型的變更和處理元件的結果，造成偵測到報表中的根本問題時出現訊息。 如需詳細資訊，請參閱 [Reporting Services Backward Compatibility](../../reporting-services/reporting-services-backward-compatibility.md)。  
  
 如需 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 新功能的詳細資訊，請參閱 [SQL Server Reporting Services (SSRS) 的新功能](../what-s-new-in-sql-server-reporting-services-ssrs.md)。  

##  <a name="versions-supported-by-upgrade"></a><a name="bkmk_versionsupported"></a> 升級支援的版本  
 在任何舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中建立的報表都可以升級。 這包括以下版本：  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
##  <a name="report-definition-rdl-files-and-report-designer"></a><a name="bkmk_rdlfiles"></a> 報表定義檔 (.rdl) 和報表設計師  
 報表定義檔案包含 RDL 命名空間的參考，其中指定了用來驗證 .rdl 檔的報表定義結構描述版本。  
  
 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的報表設計師中開啟 .rdl 檔時，如果此報表是針對先前的命名空間所建立，報表設計師就會自動建立備份檔案，並且將此報表升級至目前的命名空間。 這是升級報表定義檔案的唯一方式。  
  
 您設定的部署屬性會影響儲存報表定義檔案的結構描述。 如需詳細資訊，請參閱 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
 您可以將舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中建立的 .rdl 檔案上傳到新版本，而且第一次使用檔案時就會自動升級。 報表伺服器會使用原始格式儲存報表定義檔案。 初次檢視報表時會自動升級報表，但是已儲存的報表定義檔案則維持不變。  
  
 若要針對報表、報表伺服器或報表設計師識別目前的 RDL 結構描述，請參閱[尋找報表定義結構描述版本 &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)。  
  
##  <a name="published-reports-and-report-snapshots"></a><a name="bkmk_publishedreports_and_snapshots"></a> 已發行的報表和報表快照集  
 在初次使用時，報表伺服器會嘗試將現有已發行的報表和報表快照集升級到新的報表定義結構描述，您不需要執行任何特定動作。 當使用者檢視報表或報表快照集，或是報表伺服器處理訂閱時，就會嘗試進行升級。 報表定義不會被取代，而是繼續儲存在報表伺服器上的原始結構描述中。 如果無法升級報表，則會使用回溯相容性模式來執行報表。  
  
##  <a name="backward-compatibility-mode"></a><a name="bkmk_backcompat"></a> 回溯相容性模式  
 已成功升級的報表會由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理。 無法升級的報表會由 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器在回溯相容性模式下處理。 不能同時使用這兩種報表處理器來處理報表。 初次使用時會成功升級報表，或是將報表標示為可提供回溯相容性。  
  
 只有 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表器才支援新功能。 如果無法升級報表，您仍然可以檢視轉譯的報表，但是無法使用新的功能。 若要充分利用新的功能，則必須成功升級報表。  
  
##  <a name="upgrading-a-report-with-subreports"></a><a name="bkmk_subreports"></a> 升級具有子報表的報表  
 當報表包含子報表時，升級期間會發生以下四種可能狀態的其中一種：  
  
-   可以成功升級主報表和所有子報表。 它們是由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理。  
  
-   無法升級主報表和所有子報表。 這些報表是由 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器處理。  
  
-   可以升級主報表，但是無法升級其中一或多個子報表。 主報表是由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理，但是會在無法升級子報表的位置中出現「錯誤: 無法處理子報表」訊息。  
  
-   無法升級主報表，但是可以升級其中一或多個子報表。 主報表是由 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表處理器所處理，但是會在子報表的位置中出現「錯誤: 無法處理子報表」訊息。  
  
 如果您看到「錯誤: 無法處理子報表」錯誤，您必須變更主報表或子報表的定義，好讓報表可由相同版本的報表處理器來處理。  
  
 鑽研報表沒有這項限制，因為鑽研報表會當做獨立報表來處理。  
  
##  <a name="upgrading-a-report-with-custom-report-items"></a><a name="bkmk_CRIs"></a> 升級具有自訂報表項目的報表  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表可能包含軟體協力廠商所提供以及系統管理員針對報表撰寫電腦和報表伺服器所安裝的自訂報表項目 (CRI)。 包含 CRI 的報表可透過以下方式來升級：  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器會升級到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器。 報表伺服器上已發行的報表會在第一次使用時自動升級。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表會上傳到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器。 報表會在第一次使用時自動升級。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表會在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的報表設計師中開啟。 隨即建立原始報表的備份副本。 而且會發生以下兩種情況的其中一種：  
  
    1.  報表中的所有 CRI 都沒有任何不支援的功能。 CRI 會轉換成新報表定義結構描述內的報表項目，好讓整個報表可以升級。 如果您儲存檔案，它就會儲存在目前的 RDL 命名空間中。  
  
    2.  報表中的一或多個 CRI 具有不支援的功能。 隨即出現一個對話方塊，提示使用者是要轉換 CRI 還是將其維持不變。  
  
     如需詳細資訊，請參閱本主題稍後的「 [在報表設計師中開啟報表](#OpeningaReport) 」。  
  
 如需針對報表伺服器、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或報表識別目前 RDL 命名空間的資訊，請參閱[尋找報表定義結構描述版本 &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)。  
  
### <a name="upgrading-reports-on-a-report-server"></a>升級報表伺服器上的報表  
 當 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表第一次在已經升級為 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器的報表伺服器上執行時，此報表會自動升級為目前報表伺服器所支援的報表定義命名空間。 報表在升級之前可能已經存在於報表伺服器上，或報表可能已經透過入口網站上傳，或是在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中從報表設計師發行到報表伺服器。  
  
 下表列出報表伺服器針對報表中特定類型的 CRI 所執行的升級動作。  
  
|CRI 類型|報表伺服器升級動作|  
|--------------|----------------------------------|  
|協力廠商 CRI|未執行升級。<br /><br /> 由 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表處理器所處理。|  
  
###  <a name="opening-a-report-with-cris-in-report-designer"></a><a name="OpeningaReport"></a> 使用報表設計師開啟具有 CRI 的報表  
 當您在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]報表時，該報表將會升級到新的報表定義結構描述。 根據報表中所包含的 CRI 而異，將會發生以下其中一個動作：  
  
-   偵測到協力廠商 CRI。 如果安裝於報表撰寫電腦上的 CRI 版本與新的 RDL 結構描述不相容，則設計介面會顯示一個有紅色 X 的文字方塊。您必須聯繫系統管理員，才能安裝協力廠商所提供而且與新 RDL 結構描述相容的新版 CRI。  
  
 在報表撰寫環境中升級報表之後加以儲存是將現有報表升級到新報表定義結構描述的唯一方式。  
  
###  <a name="convert-cri-dialog-box"></a><a name="bkmk_convertCRIdialog"></a> 轉換 CRI 對話方塊  
 此報表包含自訂報表項目 (CRI) 與不支援的功能。 CRI 是報表定義語言 (RDL) 的延伸模組，支援在報表中顯示資料的自訂物件。 CRI 包括軟體協力廠商所提供的設計階段和執行階段元件。  
  
> [!NOTE]  
>  選擇在報表伺服器上支援自訂報表項目是由系統管理員所做的決定。 若要檢視報表中的 CRI，必須在報表撰寫用戶端上安裝 CRI 元件才能預覽報表，並在報表伺服器上檢視已發行或已上傳的報表。 如需詳細資訊，請參閱 [自訂報表項目](../../reporting-services/custom-report-items/custom-report-items.md) 以及軟體協力廠商的文件。  
  
 某些 CRI 可以轉換成新報表定義格式的報表項目。 利用下列清單，決定是否轉換此報表中的 CRI。  
  
-   **是** ：選擇 **[是]** ，在可能的情況下轉換報表中的所有 CRI。 在 CRI 中不支援的功能無法升級，而且會從報表定義檔案中移除。 檢視報表時，您可能會看到 CRI 在報表中顯示的方式有些差異。  
  
-   **否** ：當您不要轉換報表中的 CRI 時，選擇 **[否]** 。 這些 CRI 無法透過報表處理器顯示在其目前的版本中。 如果您的系統管理員打算安裝軟體協力廠商所提供，而且與新報表定義格式相容的新版 CRI，您應該選擇 **[否]** 。 在新版本提供之前，CRI 會在報表中顯示為一個有紅色 X 的空文字方塊。  
  
 在任一種情況下，報表會升級到新的報表定義格式，並將原始報表的備份複本儲存為 *報表名稱>\<* `-` Backup.rdl。 如果您以報表撰寫工具儲存報表，您就是以新的報表定義格式儲存升級的報表。 如果您發行報表，此報表會先儲存在您的電腦中，然後再發行到報表伺服器。 您會將升級版本的報表發行至報表伺服器。  
  
 如果您沒有儲存報表，原始報表就會維持不變。 不過，您無法在 SQL Server 2016 版本的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，或使用較新版本報表定義格式的報表撰寫環境中編輯此報表。 您可以使用入口網站將原始版本的報表上傳到 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 報表伺服器，藉此執行該報表。 如需詳細資訊，請參閱[入口網站](../../reporting-services/web-portal-ssrs-native-mode.md)。  
  
 對於您上傳 (而非發行) 到報表伺服器的報表，報表處理器會決定是否可以在第一次使用時升級報表。 無法升級的報表會在回溯相容性模式下處理，而且會如同在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中繼續顯示。  

## <a name="next-steps"></a>後續步驟

[升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[SQL Server 2016 中 SQL Server Reporting Services 的重大變更](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
[SQL Server 2016 中 SQL Server Reporting Services 的行為變更](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
[SQL Server 2016 中 SQL Server Reporting Services 已停止的功能](../../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
[自訂報表項目](../../reporting-services/custom-report-items/custom-report-items.md)   
[升級報表伺服器資料庫](../../reporting-services/install-windows/upgrade-a-report-server-database.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
