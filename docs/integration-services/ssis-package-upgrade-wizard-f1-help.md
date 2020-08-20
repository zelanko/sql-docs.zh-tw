---
description: SSIS 封裝升級精靈 F1 說明
title: SSIS 套件升級精靈 F1 說明 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
f1_keywords:
- sql13.is.upgradewizard.ssisupgradewizard.f1
- sql13.is.upgradewizard.selectsourcelocation.f1
- sql13.is.upgradewizard.selectdestinationlocation.f1
- sql13.is.upgradewizard.selectpackagemgtoptions.f1
- sql13.is.upgradewizard.selectpackages.f1
- sql13.is.upgradewizard.completewizard.f1
- sql13.is.upgradewizard.upgradingpackage.f1
ms.assetid: 7fe886ff-1ea5-48d5-9d20-d5da36dd1cd7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9e47bae183dc2d0e790a6f0cb6be207d30cd4834
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495509"
---
# <a name="ssis-package-upgrade-wizard-f1-help"></a>SSIS 封裝升級精靈 F1 說明

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  使用 [SSIS 套件升級精靈] 將舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所建立套件升級為目前 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 版本的套件格式。  
  
 **執行 SSIS 封裝升級精靈**  
  
-   [使用 SSIS 套件升級精靈來升級 Integration Services 套件](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  

## <a name="ssis-upgrade-wizard"></a>SSIS 升級精靈
  
### <a name="options"></a>選項。  
 **不要再顯示此頁面。**  
 下次開啟精靈時略過歡迎頁面。  
 
## <a name="select-source-location-page"></a>選取來源位置頁面
 使用 **[選取來源位置]** 頁面，指定升級封裝的來源。  
  
> [!NOTE]  
>  只有當您從 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或命令提示字元執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 封裝升級精靈時，才可使用此頁面。  
  
### <a name="static-options"></a>靜態選項  
 **封裝來源**  
 選取包含要升級之封裝的儲存位置。 這個選項的值列於下表中。  
  
|值|描述|  
|-----------|-----------------|  
|**檔案系統**|指示要升級的封裝位於本機電腦的資料夾中。<br /><br /> 若要讓精靈在升級這些封裝之前先備份原始封裝，原始封裝必須儲存在檔案系統中。 如需詳細資訊，請參閱「如何」主題。|  
|**SSIS 封裝存放區**|指示要升級的封裝位於封裝存放區中。 此封裝存放區是由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所管理的檔案系統資料夾集合所組成。 如需詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](../integration-services/service/package-management-ssis-service.md)。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
|**Microsoft SQL Server**|指示要升級的封裝是來自現有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
  
 **資料夾**  
 輸入包含您想要升級之封裝的資料夾名稱，或是按一下 [瀏覽]  並尋找資料夾。  
  
 **瀏覽**  
 瀏覽來尋找包含您要升級之封裝的資料夾。  
  
### <a name="package-source-dynamic-options"></a>封裝來源動態選項  
  
#### <a name="package-source--ssis-package-store"></a>封裝來源 = SSIS 封裝存放區  
 **Server**  
 輸入具有要升級之封裝的伺服器名稱，或是從清單中選取此伺服器。  
  
#### <a name="package-source--microsoft-sql-server"></a>封裝來源 = Microsoft SQL Server  
 **Server**  
 輸入具有要升級之封裝的伺服器名稱，或是從清單中選取此伺服器。  
  
 **使用 Windows 驗證**  
 選取此選項可使用 Windows 驗證來連接伺服器。  
  
 **使用 SQL Server 驗證**  
 選取此選項可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證連接到伺服器。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證將用來連接伺服器的使用者名稱。  
  
 **密碼**  
 輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證將用來連接伺服器的密碼。  
 
## <a name="select-destination-location-page"></a>選取目的地位置頁面
 使用 **[選取目的地位置]** 頁面，指定用來儲存升級封裝的目的地。  
  
> [!NOTE]  
>  只有當您從 [!INCLUDE[ssIS](../includes/ssis-md.md)] 或命令提示字元執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 封裝升級精靈時，才可使用此頁面。  
 
### <a name="static-options"></a>靜態選項  
 **儲存至來源位置**  
 將升級封裝儲存到此精靈之 [選取來源位置]  頁面上所指定的相同位置。  
  
 如果原始封裝儲存在檔案系統中，而且您希望精靈備份這些封裝，請選取 **[儲存至來源位置]** 選項。 如需詳細資訊，請參閱 [使用 SSIS 封裝升級精靈來升級 Integration Services 封裝](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)。  
  
 **選取新的目的地位置**  
 將升級封裝儲存到此頁面上指定的目的地位置。  
  
 **封裝來源**  
 指定要儲存升級封裝的位置。 這個選項的值列於下表中。  
  
|值|描述|  
|-----------|-----------------|  
|**檔案系統**|指示升級封裝要儲存到本機電腦的資料夾中。|  
|**SSIS 封裝存放區**|指示升級封裝要儲存到 Integration Services 封裝存放區。 此封裝存放區是由 Integration Services 服務所管理的檔案系統資料夾集合所組成。 如需詳細資訊，請參閱[封裝管理 &#40;SSIS 服務&#41;](../integration-services/service/package-management-ssis-service.md)。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
|**Microsoft SQL Server**|指示升級封裝要儲存到現有的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。<br /><br /> 選取這個值會顯示對應的 **[封裝來源]** 動態選項。|  
  
 **資料夾**  
 輸入將用來儲存升級封裝的資料夾名稱，或是按一下 [瀏覽]  並尋找資料夾。  
  
 **瀏覽**  
 瀏覽來尋找將儲存升級封裝的資料夾。  
  
### <a name="package-source-dynamic-options"></a>封裝來源動態選項  
  
#### <a name="package-source--ssis-package-store"></a>封裝來源 = SSIS 封裝存放區  
 **Server**  
 輸入升級封裝儲存所在的伺服器名稱，或是從清單中選取伺服器。  
  
#### <a name="package-source--microsoft-sql-server"></a>封裝來源 = Microsoft SQL Server  
 **Server**  
 輸入升級封裝儲存所在的伺服器名稱，或是從清單中選取此伺服器。  
  
 **使用 Windows 驗證**  
 選取此選項可使用 Windows 驗證來連接伺服器。  
  
 **使用 SQL Server 驗證**  
 選取此選項可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證連接到伺服器。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 輸入使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來連接伺服器時所要使用的使用者名稱。  
  
 **密碼**  
 輸入使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來連接伺服器時所要使用的密碼。  
 
## <a name="select-package-management-options-page"></a>選取套件管理選項頁面
  使用 [選取封裝管理選項]  頁面，指定用來升級封裝的選項。  
  
 **執行 SSIS 封裝升級精靈**  
  
-   [使用 SSIS 套件升級精靈來升級 Integration Services 套件](../integration-services/install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
### <a name="options"></a>選項。  
 **更新連接字串以使用新的提供者名稱**  
 更新目前版本之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的連接字串，以使用下列提供者的名稱：  
  
-   OLE DB Provider for [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈] 只會更新儲存在連線管理員中的連接字串。 此精靈不會更新使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 運算式語言或使用指令碼工作中之程式碼以動態方式建構的連接字串。  
  
 **驗證升級套件**  
 驗證升級封裝，並只儲存通過驗證的那些升級封裝。  
  
 如果您不選取這個選項，此精靈將不會驗證升級封裝。 因此，此精靈將會儲存所有的升級封裝，不論封裝是否有效。 此精靈會將升級封裝儲存到精靈之 [選取目的地位置]  頁面上所指定的目的地。  
  
 驗證會增加升級程序的時間。 如果是可能會升級成功的大型封裝，我們建議您不要選取這個選項。  
  
 **建立新的套件識別碼**  
 為升級封裝建立新的封裝識別碼。  
  
 **當套件升級失敗時，繼續升級程序**  
 指定當封裝無法升級時，[ [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈] 應繼續升級其餘的封裝。  
  
 **套件名稱衝突**  
 指定精靈應該要如何處理同名的封裝。 這個選項的值列於下表中。  
  
 **覆寫現有套件檔案**  
 以同名的升級封裝取代現有的封裝。  
  
 **在升級套件名稱後新增數字後置字元**  
 在升級封裝名稱後加入數字後置字元。  
  
 **不升級套件**  
 停止升級封裝，並在完成精靈時顯示錯誤。  
  
 當您在精靈的 [選取目的地位置]  頁面上選取 [儲存至來源位置]  選項時，無法使用這些選項。  
  
 **忽略設定**  
 封裝升級期間不載入封裝組態。 選取此選項可減少升級封裝所需的時間。  
  
 **備份原始套件**  
 讓精靈將原始封裝備份到 **SSISBackupFolder** 資料夾。 此精靈會將 **SSISBackupFolder** 資料夾建立為包含原始封裝和升級封裝之資料夾的子資料夾。  
  
> [!NOTE]  
>  只有當您指定原始封裝和升級封裝儲存在檔案系統和相同的資料夾時，才可使用這個選項。  

## <a name="select-packages-page"></a>選取套件頁面
  使用 **[選取封裝]** 頁面，選取要升級的封裝。 這個頁面會列出精靈的 **[選取來源位置]** 頁面上指定之位置內所儲存的封裝。  
  
### <a name="options"></a>選項。  
 **現有套件名稱**  
 選取一或多個要升級的封裝。  
  
 **升級套件名稱**  
 提供目的地封裝名稱，或使用精靈提供的預設名稱。  
  
> [!NOTE]  
>  您也可以在升級封裝之後變更目的地封裝名稱。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中，開啟升級的封裝及變更封裝名稱。  
  
 **密碼**  
 指定用來解密選定升級封裝的密碼。  
  
 **套用至選取項目**  
 套用指定的密碼來解密選取的升級封裝。  
 
## <a name="complete-the-wizard-page"></a>完成精靈頁面
  使用 **[完成精靈]** 頁面，即可檢閱及確認您已選取的封裝升級選項。 這是在精靈的這個工作階段中，您可以返回和變更選項的最後一個精靈頁面。  
  
### <a name="options"></a>選項。  
 **選項摘要**  
 檢閱您在精靈中選取的升級選項。 若要變更任何選項，請按 **[上一步]** 回到之前的精靈頁面。
 
## <a name="upgrading-the-packages-page"></a>正在升級套件頁面
  使用 **[正在升級封裝]** 頁面，即可檢視封裝升級的進度，並在必要時中斷升級程序。 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝升級精靈會逐一升級選取的封裝。  
  
### <a name="options"></a>選項。  
 **訊息窗格**  
 在升級進行期間顯示進度訊息和摘要資訊。  
  
 **動作**  
 檢視升級中的動作。  
  
 **狀態**  
 檢視每個動作的結果。  
  
 **訊息**  
 檢視每個動作所產生的錯誤訊息。  
  
 **停止**  
 停止封裝升級。  
  
 **Report**  
 選取您想要針對包含封裝升級結果的報表採取什麼動作：  
  
-   線上檢視報表。  
  
-   將報表儲存為檔案。  
  
-   將報表複製到剪貼簿。  
  
-   以電子郵件訊息傳送報表。  

## <a name="view-upgraded-packages"></a>檢視升級的套件
### <a name="view-upgraded-packages-that-were-saved-to-a-sql-server-database-or-to-the-package-store"></a>檢視儲存至 SQL Server 資料庫或套件存放區的已升級套件
  
在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]的 [物件總管] 中，連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的本機執行個體，然後展開 **[存放的封裝]** 節點，查看已升級的封裝。  
  
### <a name="view-upgraded-packages-that-were-upgraded-from-sql-server-data-tools"></a>檢視從 SQL Server Data Tools 升級的已升級套件  
  
在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的 [方案總管] 中，開啟 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，然後展開 **[SSIS 封裝]** 節點，查看升級的封裝。  
  
## <a name="see-also"></a>另請參閱  
 [升級 Integration Services 套件](../integration-services/install-windows/upgrade-integration-services-packages.md)  
  
  
