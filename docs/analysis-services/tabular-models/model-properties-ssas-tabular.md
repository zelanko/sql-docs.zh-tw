---
title: "模型屬性 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.wspacedbconfig.f1
- sql13.asvs.bidtoolset.fileprop.f1
ms.assetid: 8ab04656-75a5-485c-9687-7b1ca49f7f80
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 10fc0c4c74dddf6faaa2cfe0b2bff4e24695ec2d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="model-properties-ssas-tabular"></a>Model Properties (SSAS Tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]本主題描述表格式模型屬性。 每個表格式模型專案皆含有模型屬性，可影響您在 SQL Server 開發工具中撰寫之模型的建立方式、備份方式，以及工作空間資料庫的儲存方式。 此處所述的模型屬性，並不適用於已部署的模型。  
  
 本主題的章節：  
  
-   [模型屬性](#bkmk_model_properties)  
  
-   [設定模型屬性設定](#bkmk_conf_model_prop)  
  
##  <a name="bkmk_model_properties"></a> 模型屬性  
 **進階**  
  
|屬性|預設設定|說明|  
|--------------|---------------------|-----------------|  
|**建置動作**|編譯|此屬性會指定檔案與建立及部署程序的關聯。 此屬性設定具有以下選項：<br /><br /> **編譯** ：發生一般建置動作。 模型物件的定義會寫入至 .asdatabase 檔。<br /><br /> **無** ：.asdatabase 檔的輸出會是空的。|  
|**複製到輸出目錄**|不要複製|此屬性指定將來源檔案複製到輸出目錄。 此屬性設定具有以下選項：<br /><br /> **不要複製** ：不會在輸出目錄中建立任何副本。<br /><br /> **永遠複製** ：一律在輸出目錄中建立副本。<br /><br /> **有更新時才複製** ：僅當 model.bim 檔變更時，才在輸出目錄中建立副本。|  
  
 **其他**  
  
> [!NOTE]  
>  有些屬性是在建立模型時自動設定，且無法變更。  
  
> [!NOTE]  
>  當您建立新的模型專案時，[工作空間伺服器]、[工作空間保留] 及 [資料備份] 屬性會套用預設值。 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [Analysis Server] 設定中，變更新模型的預設值。 您也可以在 [屬性] 視窗中，為每個模型設定上述屬性及其他屬性。 如需詳細資訊，請參閱 [設定預設的資料模型和部署屬性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
|屬性|預設設定|說明|  
|--------------|---------------------|-----------------|  
|**定序**|安裝 Visual Studio 之電腦的預設定序。|模型的定序指示項。|  
|**相容性層級**|預設或建立專案時選取的其他項目。|適用於 SQL Server 2012 Analysis Services SP1 或更新版本。 指定此模型可用的功能和設定。 如需詳細資訊，請參閱 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。|  
|**資料備份**|不要備份到磁碟|指定是否要將模型資料的備份保留在備份檔中。 此屬性設定具有以下選項：<br /><br /> **備份到磁碟** ：指定將模型資料的備份保留在磁碟上。 儲存模型時，也會將資料儲存到備份 (ABF) 檔。 選取此選項可能會使模型的儲存和載入速度更慢。<br /><br /> **不要備份到磁碟** ：指定不要將模型資料的備份保留在磁碟上。 此選項會將模型的儲存和載入時間降至最低。<br /><br /> <br /><br /> 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [Analysis Server] 設定中，變更此屬性的預設設定。| 
|**預設篩選方向**|單一方向|決定新的關聯性的預設篩選方向。| 
|**DirectQuery 模式**|關閉|指定此模型是否以 DirectQuery 模式運作。 如需詳細資訊，請參閱 [DirectQuery 模式 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。|  
|**檔案名稱**|Model.bim|指定 .bim 檔的名稱。 檔案名稱不應變更。|  
|**完整路徑**|建立專案時所指定的路徑。|model.bim 檔案位置。 您無法在 [屬性] 視窗中設定此屬性。|  
|**語言**|英文|模型的預設語言。 預設語言取決於 Visual Studio 的語言。 您無法在 [屬性] 視窗中設定此屬性。|  
|**工作空間資料庫**|專案名稱，後面接著底線及 GUID。|工作空間資料庫的名稱，用於儲存及編輯選取之 model.bim 檔的記憶體中模型。 此資料庫會出現在 [工作空間伺服器] 屬性所指定的 Analysis Services 執行個體中。 您無法在 [屬性] 視窗中設定此屬性。 如需詳細資訊，請參閱[工作空間資料庫 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)。|  
|**工作空間保留**|從記憶體中卸載|指定在關閉模型之後，如何保留工作空間資料庫。 工作空間資料庫包含模型中繼資料、匯入模型的資料，以及模擬認證 (已加密)。 在某些情況下，工作空間資料庫可能會非常大，因此耗用大量的記憶體。 根據預設，工作空間資料庫會從記憶體中卸載。 變更此設定時，最好考慮您的可用記憶體資源，以及您打算處理模型的頻率。 此屬性設定具有以下選項：<br /><br /> **保留在記憶體中** ：指定在關閉模型後，將工作空間資料庫保留在記憶體中。 此選項將耗用較多的記憶體，但是開啟模型時，將耗用較少的資源，而且工作空間資料庫將會更快載入。<br /><br /> **從記憶體中卸載** ：指定在關閉模型後，將工作空間資料庫保留在磁碟上，但不再保留在記憶體中。 此選項將耗用較少的記憶體，但是開啟模型時，將耗用額外的資源，而且模型的載入速度比將工作空間資料庫保留在記憶體中更慢。 當記憶體中的資源有限，或者當處理遠端工作空間資料庫時，請使用此選項。<br /><br /> **刪除工作空間** ：指定在關閉模型後，從記憶體中刪除工作空間資料庫，而且不將工作空間資料庫保留在磁碟上。 此選項將耗用較少的記憶體，但是開啟模型時，將耗用額外的資源，而且模型的載入速度比將工作空間資料庫保留在記憶體中更慢。 只有在偶爾處理模型時，才使用此選項。<br /><br /> <br /><br /> 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [Analysis Server] 設定中，變更此屬性的預設設定。|  
|**工作空間伺服器**|localhost|此屬性指定在撰寫模型時，用來主控工作空間資料庫的預設伺服器。 在本機電腦上執行的所有可用 Analysis Services 執行個體都包含在清單方塊中。<br /><br /> 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [Analysis Server] 設定中，變更此屬性的預設設定。<br /><br /> <br /><br /> 注意：建議您一律將本機 Analysis Services 伺服器指定為工作空間伺服器。 若是遠端伺服器上的工作空間資料庫，則不支援從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 匯入，也無法在本機備份資料，而且使用者介面在查詢期間可能會遇到延遲。|  
  
##  <a name="bkmk_conf_model_prop"></a> 設定模型屬性設定  
  
1.  在 SSDT 的方案總管中，按一下 [Model.bim] 檔案。  
  
2.  在 **[屬性]** 視窗中，按一下屬性，然後輸入值，或按一下向下鍵選取設定選項。  
  
## <a name="see-also"></a>請參閱  
 [設定預設的資料模型和部署屬性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [專案屬性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
