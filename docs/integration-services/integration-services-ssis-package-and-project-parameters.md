---
title: Integration Services (SSIS) 套件和專案參數 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.parameterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b595c8e2c09260e6874fc3cbaab8cc06d2a0c9df
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296165"
---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Integration Services (SSIS) 套件和專案參數

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 參數可讓您在封裝執行時，將值指派給封裝內的屬性。 您可以在專案層級建立 *「專案參數」* (Project Parameter)，並在封裝層級建立 *「封裝參數」* (Package Parameter)。 專案參數可用於向專案中的一個或多個封裝提供專案接收的任何外部輸入。 封裝參數可讓您修改封裝執行，而不需要編輯和重新部署封裝。  
  
 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中您使用 **[Project.params]** 視窗建立、修改或刪除專案參數。 您可使用 **設計師中的** [參數] [!INCLUDE[ssIS](../includes/ssis-md.md)] 索引標籤建立、修改或刪除封裝參數。 您可使用 **[參數化]** 對話方塊將新的或現有的參數與工作屬性產生關聯。 如需使用 **[Project.params]** 視窗和 **[參數]** 索引標籤的詳細資訊，請參閱＜ [Create Parameters](https://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99)＞。 如需 **[參數化]** 對話方塊的詳細資訊，請參閱＜ [Parameterize Dialog Box](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350)＞。  
  
## <a name="parameters-and-package-deployment-model"></a>參數及封裝部署模型  
 一般而言，若您是使用封裝部署模型部署封裝，就應該使用組態而不是參數。  
  
 當您使用封裝部署模型部署含有參數的封裝，然後執行此封裝時，則不會在執行期間呼叫參數。 若封裝包含了封裝參數以及封裝內使用參數的運算式，就會在執行階段套用結果值。 若封裝包含專案參數，則執行封裝可能會失敗。  
  
## <a name="parameters-and-project-deployment-model"></a>參數及專案部署模型  
 當您將專案部署至 Integration Services (SSIS) 伺服器時，請使用檢視、預存程序和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 管理專案及封裝參數。 如需詳細資訊，請參閱下列主題。  
  
-   [檢視 &#40;Integration Services 目錄&#41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [預存程序 &#40;Integration Services 目錄&#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [設定對話方塊](../integration-services/service/configure-dialog-box.md)  
  
-   [執行套件對話方塊](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>參數值  
 您最多可以將三種不同類型的值指派給參數。 啟動封裝執行時，單一值會用於參數，而且參數會解析成最終常值。  
  
 下表將列出值的類型。  
  
|值名稱|描述|值的類型|  
|----------------|-----------------|-------------------|  
|執行值|指派給封裝執行之特定執行個體的值。 此指派會覆寫所有其他值，但是只會套用至封裝執行的單一執行個體。|常值|  
|伺服器值|在專案部署至 Integration Services 伺服器之後，指派給專案範圍內之參數的值。 此值會覆寫設計預設值。|常值或環境變數參考|  
|設計值|在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中建立或編輯專案時，指派給參數的值。 此值會一直跟著專案。|常值|  
  
 您可以使用單一參數，將值指派給多個封裝屬性。 但是，您只能從單一參數，將值指派給單一封裝屬性。  
  
###  <a name="executions"></a> 執行和參數值  
 *「執行」* (Execution) 是一個物件，代表封裝執行的單一執行個體。 當您建立執行時，可以指定執行封裝的所有必要詳細資料，例如執行參數值。 您也可以修改現有執行的參數值。  
  
 當您明確設定執行參數值時，此值只適用於執行的該特定執行個體。 系統會使用執行值，而非伺服器值或設計值。 如果您沒有明確設定執行值，而且已經指定伺服器值，則會使用伺服器值。  
  
 當參數標示為必要項目時，必須為該參數指定伺服器值或執行值。 否則，對應的封裝無法執行。 雖然參數在設計階段有預設值，但是一旦部署專案之後，絕對不會使用該值。  
  
#### <a name="environment-variables"></a>環境變數  
 如果參數參考環境變數，則會透過所指定的環境參考來解析該變數，並將其套用至參數。 用於封裝執行的最後常值參數值是指執行參數值。 您可以使用 **[執行]** 對話方塊來指定執行的環境參考。  
  
 如果專案參數參考環境變數，而且變數中的常值無法在執行時解析，則會使用設計值。 系統不會使用伺服器值。  
  
 若要檢視指派給參數值的環境變數，請查詢 catalog.object_parameters 檢視。 如需詳細資訊，請參閱 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)。  
  
#### <a name="determining-execution-parameter-values"></a>決定執行參數值  
 下列 Transact-SQL 檢視和預存程序可用來顯示和設定參數值。  
  
 [catalog.execution_parameter_values &#40;SSISDB 資料庫&#41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md) (檢視)  
 顯示特定執行將會使用的實際參數值。  
  
 [catalog.get_parameter_values &#40;SSISDB 資料庫&#41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (預存程序)  
 解析並顯示指定封裝和環境參考的實際值  
  
 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (檢視)  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄中顯示所有封裝及專案的參數和屬性，包括設計預設值和伺服器預設值。  
  
 [catalog.set_execution_parameter_value &#40;SSISDB 資料庫&#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 為 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定參數值。  
  
 您也可以在 **中使用** [執行封裝] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 對話方塊修改參數值。 如需詳細資訊，請參閱＜ [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)＞。  
  
 您也可以使用 dtexec **/Parameter** 選項修改參數值。 如需詳細資訊，請參閱 [dtexec Utility](../integration-services/packages/dtexec-utility.md)。  
  
### <a name="parameter-validation"></a>參數驗證  
 如果無法解析參數值，則對應的封裝執行將會失敗。 若要避免失敗，您可以使用 **中的** [驗證] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]對話方塊來驗證專案及封裝。 驗證可讓您確認所有參數都有必要的值，或是可以用特定的環境參考來解析必要的值。 驗證也會檢查其他常見的封裝問題。  
  
 如需詳細資訊，請參閱＜ [Validate Dialog Box](../integration-services/service/validate-dialog-box.md)＞。  
  
### <a name="parameter-example"></a>參數範例  
 此範例描述一個名為 **pkgOptions** 的參數，可用來指定其所在之封裝的選項。  
  
 在設計期間，於 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中建立參數時，會將預設值 1 指派給該參數。 此預設值就是設計預設值。 如果將專案部署至 SSISDB 目錄，而沒有指派任何其他值給這個參數，就會在封裝執行期間，指派值 1 給對應 **pkgOptions** 參數的封裝屬性。 在專案的整個生命週期內，設計預設值都會一直跟著專案。  
  
 在準備封裝執行的特定執行個體時，系統會指派值 5 給 **pkgOptions** 參數。 這個值就是執行值，因為只能針對執行的該特定執行個體，將此值套用至該參數。 執行啟動時，系統會將值 5 指派給對應至 **pkgOptions** 參數的封裝屬性。  
  
## <a name="create-parameters"></a>建立參數
您可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 來建立專案參數和封裝參數。 下列程序會提供建立封裝/專案參數的逐步指示。  
  
> **注意：** 如果要將使用舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 建立的專案轉換為專案部署模型，可以使用 **[Integration Services 專案轉換精靈]** ，根據組態建立參數。 如需詳細資訊，請參閱[部署 Integration Services (SSIS) 專案和套件](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。  
  
### <a name="create-package-parameters"></a>建立套件參數  
  
1.  開啟 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中的封裝，然後按一下 SSIS 設計師中的 **[參數]** 索引標籤。  
  
     ![套件的 [參數] 索引標籤](../integration-services/media/denali-package-parameters.gif "套件的 [參數] 索引標籤")  
  
2.  按一下工具列上的 **[加入參數]** 按鈕。  
  
     ![新增工具列按鈕](../integration-services/media/denali-parameter-add.gif "新增工具列按鈕")  
  
3.  在清單本身或 **[屬性]** 視窗中，輸入 **[名稱]** 、 **[資料類型]** 、 **[值]** 、 **[區分]** 以及 **[必要]** 屬性的值。 下表描述這些屬性。  
  
    |屬性|描述|  
    |--------------|-----------------|  
    |名稱|參數名稱。|  
    |資料類型|參數的資料類型。|  
    |預設值|在設計時指派的參數預設值。 這也稱為設計預設值。|  
    |敏感|敏感性參數值會在目錄中加密，以 Transact-SQL 或 SQL Server Management Studio 來檢視時，會顯示為 NULL 值。|  
    |必要|必須先指定一個值 (非設計預設值)，封裝才能執行。|  
    |描述|為方便維護，使用參數的描述。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，於 Visual Studio 的 [屬性] 視窗中設定參數描述 (已在適用的參數視窗中選取參數)。|  
  
    > **注意：** 當您將專案部署至目錄時，會再多幾個屬性與專案相關聯。 若要查看目錄中所有參數的所有屬性，請使用 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) 檢視。  
  
4.  儲存專案以儲存參數的變更。 參數值會儲存在專案檔案中。  
  
    > **警告！！** 您可以在清單中就地編輯，也可以使用 [屬性]  視窗來修改參數屬性的值。 您可以使用 [刪除] **(X)** 工具列按鈕來刪除參數。 您可以使用最後一個工具列按鈕，為僅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中執行包時使用的參數指定值。  
  
    > **注意：** 如果您在沒有開啟 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中專案的情況下重新開啟封裝檔案，[參數]  索引標籤將會是空的，而且遭到停用。  
  
### <a name="create-project-parameters"></a>建立專案參數  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中開啟專案。  
  
2.  以滑鼠右鍵按一下方案總管中的 **Project.params**，然後按一下 [開啟]  \(或) 按兩下 **Project.params** 來開啟它。  
  
     ![專案參數視窗](../integration-services/media/denali-project-parameters.gif "專案參數視窗")  
  
3.  按一下工具列上的 **[加入參數]** 按鈕。  
  
     ![新增工具列按鈕](../integration-services/media/denali-parameter-add.gif "新增工具列按鈕")  
  
4.  輸入 **[名稱]** 、 **[資料類型]** 、 **[值]** 、 **[區分]** 以及 **[必要]** 屬性的值。  
  
    |屬性|描述|  
    |--------------|-----------------|  
    |名稱|參數名稱。|  
    |資料類型|參數的資料類型。|  
    |預設值|在設計時指派的參數預設值。 這也稱為設計預設值。|  
    |敏感|敏感性參數值會在目錄中加密，以 Transact-SQL 或 SQL Server Management Studio 來檢視時，會顯示為 NULL 值。|  
    |必要|必須先指定一個值 (非設計預設值)，封裝才能執行。|  
    |描述|為方便維護，使用參數的描述。 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，於 Visual Studio 的 [屬性] 視窗中設定參數描述 (已在適用的參數視窗中選取參數)。|  
  
5.  儲存專案以儲存參數的變更。 參數值儲存在專案檔案的組態中。 儲存專案檔案即可將參數值的任何變更認可到磁碟。  
  
    > **警告！！！** 您可以在清單中就地編輯，也可以使用 [屬性]  視窗來修改參數屬性的值。 您可以使用 [刪除] **(X)** 工具列按鈕來刪除參數。 使用最後一個工具列按鈕開啟 **[管理參數值]** 對話方塊，針對僅在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中執行封裝時使用的參數指定值。  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
[參數化]  對話方塊可讓您將新的或現有的參數與工作屬性建立關聯。 您可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，以滑鼠右鍵按一下工作或 [控制流程] 索引標籤，然後按一下 [參數化]  即可開啟此對話方塊。 下列清單描述對話方塊中的 UI 元素。 如需參數的詳細資訊，請參閱 [Integration Services (SSIS) 參數](https://msdn.microsoft.com/library/hh213214.aspx)。
  
### <a name="options"></a>選項。  
 **屬性**  
 選取要與參數產生關聯的工作屬性。 此清單會以可參數化的所有屬性擴展。  
  
 **使用現有的參數**  
 選取此選項可讓任務屬性與某個現有的參數產生關聯，然後從下拉式清單中選取該參數。  
  
 **不使用參數**  
 選取此選項以移除參數的參考。 未刪除參數。  
  
 **建立新的參數**  
 選取此選項可建立要與任務屬性產生關聯的新參數。  
  
 **名稱**  
 指定您要建立之參數的名稱。  
  
 **說明**  
 指定參數的描述。  
  
 **ReplTest1**  
 指定參數的預設值。 這也稱作設計預設值，以後在部署時可以覆蓋該值。  
  
 **範圍**  
 選取 [專案]  或 [封裝]  選項來指定參數的範圍。 專案參數可用於向專案中的一個或多個封裝提供專案接收的任何外部輸入。 封裝參數可讓您修改封裝執行，而不需要編輯和重新部署封裝。  
  
 **區分**  
 透過檢查或清除該核取方塊來指定參數是否敏感。 敏感性參數值會在目錄中加密，以 Transact-SQL 或 SQL Server Management Studio 來檢視時，會顯示為 NULL 值。  
  
 **必要**  
 指定參數是否是否需要先指定一個值 (非設計預設值)，指定的封裝才能執行。  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>部署專案之後設定參數值
部署精靈可讓您在將專案部署到目錄時，設定伺服器預設參數值。 專案在目錄中之後，您可以使用 SQL Server Management Studio (SSMS) 物件總管或 Transact-SQL 來設定伺服器預設值。  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>使用 SSMS 物件總管設定伺服器預設值  
  
1.  選取並以滑鼠右鍵按一下 [Integration Services]  節點底下的專案。  
  
2.  按一下 **[屬性]** ，以開啟 **[專案屬性]** 對話方塊視窗。  
  
3.  按一下 **[選取頁面]** 底下的 **[參數]** ，以開啟參數頁面。  
  
4.  在 **[參數]** 清單選取所需的參數。 注意:[容器]  資料行有助於區分專案參數與封裝參數。  
  
5.  在 **[值]** 資料行中，指定所需的伺服器預設參數值。  

### <a name="set-server-defaults-with-transact-sql"></a>使用 Transact-SQL 設定伺服器預設值  
 若要使用 Transact-SQL 設定伺服器預設值，請使用 [catalog.set_object_parameter_value &#40;SSISDB 資料庫&#41;](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) 預存程序。 若要檢視目前的伺服器預設值，請查詢 [catalog.object_parameters &#40;SSISDB 資料庫&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) 檢視。 若要清除伺服器預設值，請使用 [catalog.clear_object_parameter_value &#40;SSISDB 資料庫&#41;](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md) 預存程序。  
  
## <a name="related-content"></a>相關內容  
 mattmasson.com 上的部落格文章：[SSIS 快速提示：必要參數](https://go.microsoft.com/fwlink/?LinkId=239781)。  
  
  
