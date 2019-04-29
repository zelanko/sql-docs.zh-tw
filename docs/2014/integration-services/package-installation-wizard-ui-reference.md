---
title: 封裝安裝精靈 UI 參考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.deploymentwizard.confirminstallation.f1
- sql12.dts.deploymentwizard.deploydtspackages.f1
- sql12.dts.deploymentwizard.selectinstfolder.f1
- sql12.dts.deploymentwizard.specifytargetsqlserver.f1
- sql12.dts.deploymentwizard.welcome.f1
- sql12.dts.deploymentwizard.finish.f1
- sql12.dts.deploymentwizard.configurepackages.f1
- sql12.dts.deploymentwizard.packagevalidation.f1
helpviewer_keywords:
- Package Installer Wizard
ms.assetid: 6fca44d9-5001-4644-bcf3-c2d10a674b97
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 68f464d49680e3563f44768e9d8ad29d947a8b24
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62890271"
---
# <a name="package-installation-wizard-ui-reference"></a>封裝安裝精靈 UI 參考
  使用 [封裝安裝精靈] 來部署 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案，包括其內含的封裝和其他檔案，以及任何封裝的相依性。  
  
 在部署封裝之前，可以建立組態，然後將其隨封裝部署。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會使用組態，在執行階段以動態方式更新封裝及封裝物件的屬性。 例如，OLE DB 連接的連接字串可提供對應值與包含連接字串屬性的組態，藉此於執行階段進行動態設定。  
  
 您必須先建置 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案並建立部署公用程式，才能執行 [封裝安裝精靈]。 如需詳細資訊，請參閱 [使用部署公用程式來部署封裝](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)。  
  
 下列章節描述精靈頁面。  
  
## <a name="welcome-to-the-package-installation-wizard-page"></a>歡迎使用封裝安裝精靈頁面  
 使用 [封裝安裝精靈]，即可部署建立了封裝部署公用程式的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
 **不要再顯示此開始頁面**  
 選取再次執行精靈時要略過開始頁面。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **[完成]**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
## <a name="configure-packages-page"></a>設定封裝頁面  
 使用 [設定封裝] 頁面即可編輯封裝組態。  
  
### <a name="options"></a>選項。  
 **組態檔**  
 從清單中選取檔案來編輯組態檔的內容。  
  
 **相關主題：**[建立套件設定](../../2014/integration-services/create-package-configurations.md)  
  
 **路徑**  
 檢視要設定之屬性的路徑。  
  
 **型別**  
 檢視屬性的資料類型。  
  
 **值**  
 指定組態的值。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **[完成]**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
## <a name="confirm-installation-page"></a>確認安裝頁面  
 使用 [確認安裝] 頁面，即可開始安裝封裝、檢視狀態，以及檢視精靈用以從指定專案中安裝檔案的資訊。  
  
 **下一個**  
 安裝封裝及其相依檔案，並在安裝完成時移到下一個精靈頁面。  
  
 **狀態**  
 顯示封裝安裝的進度。  
  
 **[完成]**  
 移至 [完成封裝安裝精靈] 頁面。 如果您有回到先前的精靈頁面來修改選擇，並且指定了所有必要的選項，請使用此選項。  
  
## <a name="deploy-ssis-packages-page"></a>部署 SSIS 封裝頁面  
 使用 [部署 SSIS 封裝] 頁面，來指定安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝及其相依性的位置。  
  
### <a name="options"></a>選項。  
 **檔案系統部署**  
 將封裝及相依性部署到檔案系統的指定資料夾中。  
  
 **SQL Server 部署**  
 將封裝及相依性部署到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體中。 如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在伺服器之間共用封裝，請使用此選項。 所有的封裝相依性都會安裝到檔案系統的指定資料夾中。  
  
 **安裝之後驗證封裝**  
 指出是否在安裝之後驗證封裝。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **[完成]**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
## <a name="packages-validation-page"></a>封裝驗證頁面  
 使用 [封裝驗證] 頁面，即可檢視封裝驗證的進度與結果。  
  
 **下一個**  
 移至精靈的下一頁。  
  
## <a name="select-installation-folder-page"></a>選取安裝資料夾頁面  
 使用 [選取安裝資料夾] 頁面，即可指定安裝封裝及其相依性的檔案系統資料夾。  
  
### <a name="options"></a>選項。  
 **資料夾**  
 指定複製封裝及其相依性的路徑和資料夾。  
  
 **瀏覽**  
 使用 [瀏覽資料夾] 對話方塊，即可瀏覽至目標資料夾。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **[完成]**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您有依序返回精靈的其他頁面以修訂選擇，並且已指定了所有必要的選項，則請使用此選項。  
  
## <a name="specify-target-sql-server-page"></a>指定目標 SQL Server 頁面  
 使用 [指定目標 SQL Server] 頁面，即可指定將封裝部署至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的選項。  
  
### <a name="options"></a>選項。  
 **伺服器名稱**  
 指定部署封裝目的地之伺服器的名稱。  
  
 **[使用 Windows 驗證]**  
 指定是否使用 Windows 驗證來登入伺服器。 建議使用 Windows 驗證，以獲得較佳的安全性。  
  
 **使用 SQL Server 驗證**  
 指定封裝是否應使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證來登入伺服器。 如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 指定使用者名稱。  
  
 **密碼**  
 指定密碼。  
  
 **封裝路徑**  
 指定邏輯資料夾名稱，或輸入 "/" 代表預設資料夾。  
  
 若要在 [SSIS 封裝] 對話方塊中選取資料夾，請按一下 [瀏覽 (...)]。不過，此對話方塊並不能用來選取預設資料夾。 如果想要使用預設資料夾，必須在文字方塊中輸入 "/"。  
  
> [!NOTE]  
>  如果未輸入有效的套件路徑，則會出現下列錯誤訊息：「一或多個引數無效。」  
  
 **依賴伺服器儲存體進行加密**  
 選取即可使用 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的安全性功能來保護封裝的安全。  
  
 **下一個**  
 移至精靈的下一頁。  
  
 **[完成]**  
 跳到 [完成封裝安裝精靈] 頁面。 如果您依序返回精靈的頁面以修訂您的選擇，並且指定了所有必要的選項，則請使用這個選項。  
  
## <a name="finish-the-package-installation-page"></a>完成封裝安裝頁面  
 使用 [完成封裝安裝精靈] 頁面，即可檢視封裝安裝結果的摘要。 此頁面提供詳細資料，例如已部署的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案、已安裝的封裝、組態檔以及安裝位置。  
  
 **[完成]**  
 按一下 [完成] 以結束精靈。  
  
## <a name="see-also"></a>另請參閱  
 [封裝部署&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
