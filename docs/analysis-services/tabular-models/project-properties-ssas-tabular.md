---
title: Analysis Services 表格式模型專案屬性 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b695f847ec7f99366e71e76aefe5aecb99cf5933
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162648"
---
# <a name="project-properties"></a>專案屬性 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  這篇文章描述模型專案屬性。 每個表格式模型專案都含有部署選項與部署伺服器選項，可指定專案及模型的部署方式。 例如，模型要部署至的伺服器及部署的模型資料庫名稱。 這些設定不同於模型屬性，後者會影響模型工作空間資料庫。 此處所述的專案屬性位於強制回應屬性對話方塊中，與用於顯示其他屬性類型的屬性視窗不同。 若要在顯示強制回應專案屬性，請在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 方案總管  中，以滑鼠右鍵按一下專案，然後按一下 [屬性]  。  
  
 本主題的章節：  
  
-   [專案屬性](#bkmk_proj_properties)  
  
-   [設定部署選項與部署伺服器屬性設定](#bkmk_conf_proj_settings)  
  
##  <a name="bkmk_proj_properties"></a> 專案屬性  
 **部署選項**  
  
|屬性|預設設定|描述|  
|--------------|---------------------|-----------------|  
|**處理選項**|**預設值**|依預設，Analysis Services 會在部署物件變更時決定所需的處理類型， 這通常會產生最快的部署時間； 但是，您也可以選擇在每一次部署時進行完整的處理或是不執行任何處理。|  
|**交易式部署**|**False**|會指定模型部署是否為交易式。 依預設，在處理這些已部署的物件時，所有物件或已變更之物件的部署並不是交易式。 即使處理失敗，部署仍可以成功，並持續存在。 您可以變更這項預設值，在單一交易中併入部署和處理。|  
|**查詢模式**|**In-Memory**|指定傳回查詢結果的來源。 如需詳細資訊，請參閱 < [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。|  
  
 **部署伺服器**  
  
|屬性|預設設定|描述|  
|--------------|---------------------|-----------------|  
|**Server**|**localhost**|指定 Analysis Services 的執行個體。 依預設，模型將會部署到本機電腦上的預設 Analysis Services 執行個體。 您可以變更這項設定，以便在本機電腦上或是您有權建立 Analysis Services 物件之任何遠端電腦上的任何執行個體上指定具名執行個體。 這通常是管理員的權限。<br /><br /> 您可以在 [部署] 頁面之 [工具\選項] 對話方塊的 [Analysis Server 設定] 中，使用 [預設部署伺服器] 屬性變更此屬性的預設值。 如需詳細資訊，請參閱 <<c0> [ 設定預設資料模型化和部署屬性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。|  
|**版本(Edition)**|**開發人員**|會指定要將模型部署到哪一個版本的 Analysis Services 伺服器。 這些伺服器版本會定義可以納入專案中的多種功能。|  
|**[資料庫備份]**|**模型**|指定一旦部署之後，模型物件會立刻具現化所在的 Analysis Services 資料庫名稱。 此名稱將會在資料連接或 .rsds 資料連接檔案中指定。 建議名稱要能反映將使用模型執行之分析的類型，例如 AdventureWorksSalesModel。<br /><br /> 若要避免已部署模型的名稱重複，您應該變更 **[資料庫]** 屬性名稱設定以反映模型用途。 當使用者連接至做為資料來源的模型時，這是他們會看到的名稱。|  
|**Cube 名稱**|**型號**|指定報告用戶端資料連接中顯示的資料庫 Cube 名稱。|  
|**版本**|**13.0**|專案部署所在之 Analysis Services 執行個體的版本。|  
  
 **DirectQuery 選項**  
  
|屬性|預設設定|描述|  
|--------------|---------------------|-----------------|  
|**模擬設定**|**預設值**|指定用來連接至執行於 DirectQuery 模式中之模型資料來源的認證。 這些認證不同於用在預設記憶體模式中的模擬認證。 如需詳細資訊，請參閱 <<c0> [ 模擬](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)。|  
  
##  <a name="bkmk_conf_proj_settings"></a> 設定部署選項與部署伺服器屬性設定  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的方案總管  中，以滑鼠右鍵按一下專案，然後按一下 [屬性]  。  
  
2.  在 **[屬性]** 視窗中，按一下屬性，然後輸入值，或按一下向下鍵選取設定選項。  
  
## <a name="see-also"></a>另請參閱  
 [設定預設資料模型化和部署屬性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [模型屬性](../../analysis-services/tabular-models/model-properties-ssas-tabular.md)   
 [表格式模型解決方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
