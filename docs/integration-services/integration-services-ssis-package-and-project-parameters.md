---
title: "Integration Services (SSIS) 封裝和專案參數 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.parameter.f1"
  - "sql13.dts.designer.paramterwindow.f1"
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Integration Services (SSIS) 封裝和專案參數
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) 參數可讓您在封裝執行時，將值指派給封裝內的屬性。 您可以建立 *參數專案* 專案層級和 *封裝參數* 套件層級。 專案參數可用於向專案中的一個或多個封裝提供專案接收的任何外部輸入。 封裝參數可讓您修改封裝執行，而不需要編輯和重新部署封裝。  
  
 在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 建立、 修改或刪除專案參數使用 **Project.params** 視窗。 建立、 修改和刪除封裝參數使用 **參數** 索引標籤中 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計工具。 與工作屬性中建立新的或現有的參數關聯使用 **參數化** 對話方塊。 如需詳細資訊使用 **Project.params** 視窗和 **參數** 索引標籤上，請參閱 [建立參數](../Topic/Create%20Parameters.md)。 如需詳細資訊 **參數化** 對話方塊中，請參閱 [參數化對話方塊](../Topic/Parameterize%20Dialog%20Box.md)。  
  
## 參數及封裝部署模型  
 一般而言，若您是使用封裝部署模型部署封裝，就應該使用組態而不是參數。  
  
 當您使用封裝部署模型部署含有參數的封裝，然後執行此封裝時，則不會在執行期間呼叫參數。 若封裝包含了封裝參數以及封裝內使用參數的運算式，就會在執行階段套用結果值。 若封裝包含專案參數，則執行封裝可能會失敗。  
  
## 參數及專案部署模型  
 當您部署專案至 Integration Services (SSIS) 伺服器時，您可使用檢視、 預存程序，而 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] UI 管理專案和封裝參數。 如需詳細資訊，請參閱下列主題。  
  
-   [檢視 #40; Integration Services 目錄 & #41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [預存程序 #40; Integration Services 目錄 & #41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [設定對話方塊](../integration-services/service/configure-dialog-box.md)  
  
-   [執行封裝對話方塊](../integration-services/packages/execute-package-dialog-box.md)  
  
### 參數值  
 您最多可以將三種不同類型的值指派給參數。 啟動封裝執行時，單一值會用於參數，而且參數會解析成最終常值。  
  
 下表將列出值的類型。  
  
|值名稱|描述|值的類型|  
|----------------|-----------------|-------------------|  
|執行值|指派給封裝執行之特定執行個體的值。 此指派會覆寫所有其他值，但是只會套用至封裝執行的單一執行個體。|常值|  
|伺服器值|在專案部署至 Integration Services 伺服器之後，指派給專案範圍內之參數的值。 此值會覆寫設計預設值。|常值或環境變數參考|  
|設計值|在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中建立或編輯專案時，指派給參數的值。 此值會一直跟著專案。|常值|  
  
 您可以使用單一參數，將值指派給多個封裝屬性。 但是，您只能從單一參數，將值指派給單一封裝屬性。  
  
###  <a name="executions"></a> 執行和參數值  
  *執行* 是物件，代表封裝執行的單一執行個體。 當您建立執行時，可以指定執行封裝的所有必要詳細資料，例如執行參數值。 您也可以修改現有執行的參數值。  
  
 當您明確設定執行參數值時，此值只適用於執行的該特定執行個體。 系統會使用執行值，而非伺服器值或設計值。 如果您沒有明確設定執行值，而且已經指定伺服器值，則會使用伺服器值。  
  
 當參數標示為必要項目時，必須為該參數指定伺服器值或執行值。 否則，對應的封裝無法執行。 雖然參數在設計階段有預設值，但是一旦部署專案之後，絕對不會使用該值。  
  
#### 環境變數  
 如果參數參考環境變數，則會透過所指定的環境參考來解析該變數，並將其套用至參數。 用於封裝執行的最後常值參數值是指執行參數值。 使用指定的環境參考。 執行 **Execute** 對話方塊  
  
 如果專案參數參考環境變數，而且變數中的常值無法在執行時解析，則會使用設計值。 系統不會使用伺服器值。  
  
 若要檢視指派給參數值的環境變數，請查詢 catalog.object_parameters 檢視。 如需詳細資訊，請參閱 [catalog.object_parameters & #40。SSISDB 資料庫 & #41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)。  
  
#### 決定執行參數值  
 下列 Transact-SQL 檢視和預存程序可用來顯示和設定參數值。  
  
 [catalog.execution_parameter_values & #40。SSISDB 資料庫 & #41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)（檢視）  
 顯示特定執行將會使用的實際參數值。  
  
 [catalog.get_parameter_values & #40。SSISDB 資料庫 & #41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) （預存程序）  
 解析並顯示指定封裝和環境參考的實際值  
  
 [catalog.object_parameters & #40。SSISDB 資料庫 & #41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) （檢視）  
 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄中顯示所有封裝及專案的參數和屬性，包括設計預設值和伺服器預設值。  
  
 [catalog.set_execution_parameter_value & #40。SSISDB 資料庫 & #41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 為 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 目錄中執行的執行個體設定參數值。  
  
 您也可以使用 **執行封裝** 對話方塊中的 [ [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 修改參數值。 如需詳細資訊，請參閱 [Execute Package Dialog Box](../integration-services/packages/execute-package-dialog-box.md)。  
  
 您也可以使用 dtexec **/Parameter** 選項修改參數值。 如需詳細資訊，請參閱 [dtexec Utility](../integration-services/packages/dtexec-utility.md)。  
  
### 參數驗證  
 如果無法解析參數值，則對應的封裝執行將會失敗。 若要避免失敗，驗證專案和封裝使用 **驗證** 對話方塊 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。 驗證可讓您確認所有參數都有必要的值，或是可以用特定的環境參考來解析必要的值。 驗證也會檢查其他常見的封裝問題。  
  
 如需詳細資訊，請參閱 [驗證對話方塊](../integration-services/service/validate-dialog-box.md)。  
  
### 參數範例  
 此範例描述一個名為參數 **pkgOptions** 用來指定其所在之封裝的選項。  
  
 在設計期間，於 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中建立參數時，會將預設值 1 指派給該參數。 此預設值就是設計預設值。 如果將專案部署至 SSISDB 目錄，以及任何其他值已指派給這個參數，以對應的封裝屬性 **pkgOptions** 參數會在封裝執行期間指派的值為 1。 在專案的整個生命週期內，設計預設值都會一直跟著專案。  
  
 在準備封裝執行的特定執行個體，5 的值指派給 **pkgOptions** 參數。 這個值就是執行值，因為只能針對執行的該特定執行個體，將此值套用至該參數。 執行啟動時，封裝屬性對應至 **pkgOptions** 值 5 指派給參數。  
  
## 相關工作  
 [建立參數](../Topic/Create%20Parameters.md)  
  
 [部署專案之後設定參數值](../Topic/Set%20Parameter%20Values%20After%20the%20Project%20Is%20Deployed.md)  
  
## 相關內容  
 部落格文章 [SSIS 快速提示︰ 必要參數](http://go.microsoft.com/fwlink/?LinkId=239781), ，mattmasson.com 上。  
  
  