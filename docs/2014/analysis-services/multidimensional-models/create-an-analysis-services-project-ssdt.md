---
title: 建立 Analysis Services 專案 (SSDT) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services]
- templates [Analysis Services], projects
- projects [Analysis Services], creating
- projects [Analysis Services], Business Intelligence Development Studio
- Business Intelligence Development Studio, defining projects [Analysis Services]
- items [Analysis Services]
ms.assetid: d00913b0-cd6d-4de0-a1e7-4ce86fcc078d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ccf355df8a26136a72b48c4b81a1953d84d90186
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702245"
---
# <a name="create-an-analysis-services-project-ssdt"></a>建立 Analysis Services 專案 (SSDT)
  您可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 專案範本，或使用 [匯入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫精靈] 讀取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的內容，來定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案。 如果目前在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中未載入任何方案，則建立新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案會自動建立新的方案； 否則會將新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案加入至現有的方案。 方案開發的最佳作法需要為不同類型的應用程式資料建立個別的專案，並在專案相關時使用單一方案。 例如，您可以擁有一個方案，其中包含 Integration Services 封裝、Analysis Services 資料庫及 Reporting Services 報表的不同專案，以供相同的商務應用程式使用。  
  
 Analysis Services 專案包含單一 Analysis Services 資料庫中所使用的物件。 專案的部署屬性指定伺服器和資料庫名稱，專案中繼資料會透過這些名稱部署為具現化的物件。  
  
 本主題包含下列幾節：  
  
 [使用 Analysis Services 專案範本建立新專案](#bkmk_NewUsingTemplate)  
  
 [使用現有的 Analysis Services 資料庫建立新專案](#bkmk_NewUsingWizard)  
  
 [將 Analysis Services 專案加入至現有的方案](#bkmk_AddtoExistingSolution)  
  
 [建立及部署方案](#bkmk_buildDeploy)  
  
 [Analysis Services 專案資料夾](#bkmk_ProjectFolders)  
  
 [Analysis Services 檔案類型](#bkmk_FileTypes)  
  
 [Analysis Services 項目範本](#bkmk_ItemTemplates)  
  
##  <a name="bkmk_NewUsingTemplate"></a> 使用 Analysis Services 專案範本建立新專案  
 您可以使用下列指示建立空白的專案，並在其中定義可在稍後部署為新 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中按一下 [檔案]、指向 [新增]，然後按一下 [專案]。 在 [新增專案] 對話方塊的 [專案類型] 窗格中，選取 [商業智慧專案]。  
  
2.  在 [新增專案] 對話方塊的 [Visual Studio 安裝的範本] 類別目錄中，選取 [Analysis Services 專案]。  
  
3.  在 [名稱] 文字方塊中，輸入此專案的名稱。 您輸入的名稱會當做預設資料庫名稱使用。  
  
4.  在 [位置] 下拉式清單中，輸入或選取您想要用來儲存專案之檔案的資料夾，或是按一下 [瀏覽] 選取資料夾。  
  
5.  若要將新的專案加入至現有的方案，請在 [方案] 下拉式清單中選取 [加入至方案]。  
  
     -或-  
  
     若要建立新的方案，請在 [方案] 下拉式清單中，選取 [建立新方案]。 若要對新的方案建立新的資料夾，請選取 [為方案建立目錄]。 在 [方案名稱] 中，輸入新方案的名稱。  
  
6.  按一下 [確定] 。  
  
##  <a name="bkmk_NewUsingWizard"></a> 使用現有的 Analysis Services 資料庫建立新專案  
 使用 [匯入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫精靈]，根據現有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的物件建立專案。 當您根據現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]專案中開啟該資料庫的中繼資料。 然後可以在專案中修改這些物件，而不會影響原始物件；之後可以部署到相同的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫 (如果部署屬性指定該資料庫) 或新建的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，以便進行比較測試。 所做的變更要等到部署之後，才會影響現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。  
  
 您也可以使用匯入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫範本，從實際執行的資料庫建立專案。自從部署了原始的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案之後，已經直接對此資料庫進行變更。  
  
 在您處理或部署專案之前，可能需要變更資料來源中指定的資料提供者。 如果您使用的 SQL Server 軟體版本比建立資料庫的軟體版本更新，電腦上可能不會安裝專案中指定的資料提供者。 在處理期間，會使用服務帳戶來擷取 Analysis Services 資料庫中的資料。 如果資料庫在遠端伺服器上，請檢查本機服務是否具有該伺服器的處理和讀取權限。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中按一下 [檔案]、指向 [新增]，然後按一下 [專案]。 在 [新增專案] 對話方塊的 [專案類型] 窗格中，選取 [商業智慧專案]。  
  
2.  在 [新增專案] 對話方塊的 [Visual Studio 安裝的範本] 類別目錄中，選取 [匯入 Analysis Services 資料庫]。  
  
3.  輸入專案和方案的屬性資訊，包括檔案的名稱和位置。 按一下 [確定] 。  
  
4.  在 [歡迎使用匯入 Analysis Services 資料庫精靈] 頁面上，按一下 [下一步]。  
  
5.  在 [來源資料庫] 頁面上，指定此精靈將從中擷取內容及建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的伺服器和資料庫，然後按一下 [下一步]。  
  
     支援的資料庫包括使用下列 Analysis Services 版本建立的資料庫：[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 及 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
     您可以輸入資料庫名稱或是查詢伺服器，以檢視伺服器上現有的資料庫。 如果資料庫在遠端伺服器或實際執行伺服器上，您可能必須要求讀取資料庫的權限。 防火牆組態設定可以進一步限制對資料庫的存取。 如果在嘗試連接至資料庫時發生錯誤，請先檢查權限和防火牆設定。  
  
6.  當此精靈完成擷取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的內容之後，按一下 [正在完成精靈] 頁面上的 [完成]。  
  
7.  開啟 [方案總管] 視窗，檢視此專案的內容。  
  
##  <a name="bkmk_AddtoExistingSolution"></a> 將 Analysis Services 專案加入至現有的方案  
 如果您的方案包含商務應用程式的所有來源檔案，則可以將新的 Analysis Services 專案加入至該方案。  
  
 將現有的專案加入至方案會建立專案與方案的關聯，但不會複製專案。 如果在其他方案中建立 Analysis Services 專案，專案檔案會與建立專案的原始方案保留在一起。 這表示您透過任一方案對專案進行的任何變更，會影響同一組來源檔案。 如果這不是您預期的行為，您應該先將專案檔案複製或移至新方案資料夾，再將專案加入至方案。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中開啟此方案。 在方案總管的方案上按一下滑鼠右鍵，然後指向 [加入]，再按一下 [現有專案] 以選取您要加入的專案。  
  
2.  選取 .dwproj 檔案以加入至方案。  
  
##  <a name="bkmk_buildDeploy"></a> 建立及部署方案  
 依預設， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會將專案部署到本機電腦上的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預設執行個體。 您可以變更這個部署目的地，其方式是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的 [屬性頁] 對話方塊來變更 [伺服器] 組態屬性。  
  
> [!NOTE]  
>  依預設，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 在部署方案時，只會處理由部署指令碼所變更的物件和相依物件。 您可以變更這項功能，其方式是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的 [屬性頁] 對話方塊來變更 [處理選項] 組態屬性。  
  
 建立方案並部署至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體進行測試。 建立方案會驗證專案中的物件定義和相依性，並產生部署指令碼。 部署方案會使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署引擎，將部署指令碼傳送至指定的執行個體。  
  
 部署專案之後，請檢閱及測試已部署的資料庫。 然後，您可以修改物件定義，並重新建立及部署，直到完成專案。  
  
 完成專案之後，您可以使用 [部署精靈]，將建立方案時所產生的部署指令碼部署到目的地執行個體，以進行最終測試、暫存及部署。  
  
##  <a name="bkmk_ProjectFolders"></a> Analysis Services 專案資料夾  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案包含下列資料夾，這些資料夾是用於組織專案中所含的項目。  
  
|資料夾|描述|  
|------------|-----------------|  
|資料來源|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的資料來源。 您可以使用資料來源精靈建立這些物件，並以資料來源設計師來編輯。|  
|資料來源檢視|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的資料來源檢視。 您可以使用資料來源檢視精靈建立這些物件，並以資料來源檢視設計師來編輯。|  
|Cube|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的 Cube。 您可以使用 Cube 精靈建立這些物件，並以 Cube 設計師來編輯。|  
|維度|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的維度。 您可以使用維度精靈或 Cube 精靈建立這些物件，並以維度設計師來編輯。|  
|採礦結構|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的採礦結構。 您可以使用採礦模型精靈建立這些物件，並以採礦模型設計師來編輯。|  
|角色|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的資料庫角色。 您可以使用角色設計師來建立和管理角色。|  
|組件|包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 專案的 COM 程式庫和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .NET Framework 組件的參考。 您可以使用 [加入參考] 對話方塊來建立參考。|  
|其他|包含除了 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 檔案類型以外的任何檔案類型。 使用此資料夾加入任何其他檔案，例如，包含專案附註的文字檔。|  
  
##  <a name="bkmk_FileTypes"></a> Analysis Services 檔案類型  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 方案可包含數種檔案類型，視您包括在方案中的專案及您包括在該方案中之每個專案的項目而定。 通常， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 方案中每個專案的檔案是儲存在方案資料夾內，每一個專案都有個別的資料夾。  
  
> [!NOTE]  
>  將物件的檔案複製到專案資料夾不會將物件加入至專案。 您必須從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的專案內容功能表中使用 [加入] 命令，將現有的物件定義加入專案中。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的專案資料夾可以包含下表所列的檔案類型。  
  
|檔案類型|描述|  
|---------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案定義檔 (.dwproj)|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中所定義及包含的項目、組態及組件參考的相關中繼資料。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案使用者設定 (.dwproj.user)|包含特定使用者之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的組態資訊。|  
|資料來源檔案 (.ds)|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 元素，這些元素會定義資料來源的中繼資料。|  
|資料來源檢視檔案 (.dsv)|包含 ASSL 元素，這些元素會定義資料來源檢視的中繼資料。|  
|Cube 檔案 (.cube)|包含 ASSL 元素，這些元素會定義 Cube 的中繼資料，其中包括量值群組、量值及 Cube 維度。|  
|資料分割檔案 (.partitions)|包含 ASSL 元素，這些元素會定義指定之 Cube 的資料分割中繼資料。|  
|維度檔案 (.dim)|包含 ASSL 元素，這些元素會定義資料庫維度的中繼資料。|  
|採礦結構檔案 (.dmm)|包含 ASSL 元素，這些元素會定義採礦結構和相關聯採礦模型的中繼資料。|  
|資料庫檔案 (.database)|包含 ASSL 元素，這些元素會定義資料庫的中繼資料，包括帳戶類型、翻譯以及資料庫權限。|  
|資料庫角色檔案 (.role)|包含 ASSL 元素，這些元素會定義資料庫角色的中繼資料，包括角色成員。|  
  
##  <a name="bkmk_ItemTemplates"></a> Analysis Services 項目範本  
 如果您使用 [加入新項目] 對話方塊將新的項目加入 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中，您可以選擇使用項目範本，此範本為示範如何執行指定動作之預先定義的指令碼或陳述式。  
  
 [加入新項目] 對話方塊的 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案項目] 類別目錄中會提供下表所列的項目範本。  
  
|Category|項目範本|描述|  
|--------------|-------------------|-----------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案項目|Cube|啟動 [Cube 精靈]，將新的 Cube 加入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中。|  
||資料來源|啟動 [資料來源精靈]，將新的資料來源加入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中。|  
||[資料來源檢視]|啟動 [資料來源檢視精靈]，將新的資料來源檢視加入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中。|  
||資料庫角色|將新的資料庫角色加入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中，然後針對這個新的資料庫角色顯示角色設計師。|  
||維度|啟動 [維度精靈]，將新的資料庫維度加入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中。|  
||採礦結構|啟動 [資料採礦精靈]，將新的採礦結構和關聯的採礦模型加入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中。|  
  
## <a name="see-also"></a>另請參閱  
 [設定 Analysis Services 專案屬性 &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [建立 Analysis Services 專案 &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [部署 Analysis Services 專案 &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
