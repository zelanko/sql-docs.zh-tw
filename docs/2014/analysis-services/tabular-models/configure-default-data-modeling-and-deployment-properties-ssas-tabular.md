---
title: 設定預設的資料模型和部署屬性 (SSAS 表格式) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.deployment.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql12.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8a38556f1c6b9d93f844441327a5ea8fe5f9ae9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030376"
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>設定預設的資料模型和部署屬性 (SSAS 表格式)
  本主題描述如何設定預設相容性層級、部署和工作空間資料庫屬性設定，這些設定可以針對您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立的新表格式模型專案預先定義。 建立新專案之後，這些屬性仍可依據您的特殊需求進行變更。  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>若要針對新的模型專案設定預設相容性層級屬性設定  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，按一下 **[工具]** 功能表，然後按一下 **[選項]**。  
  
2.  在 **[選項]** 對話方塊中，展開 **[Analysis Services 表格式設計師]**，然後按一下 **[相容性層級]**。  
  
3.  設定下列屬性設定：  
  
    |屬性|預設設定|描述|  
    |--------------|---------------------|-----------------|  
    |**新專案的預設相容性層級**|SQL Server 2012 (1100)|此設定會指定建立新的表格式模型專案時的預設相容性層級。 如果您要部署到未套用 SP1 的 Analysis Services 執行個體，可以選擇 SQL Server 2012 RTM (1100)；如果您的部署執行個體已套用 SP1，可以選擇 SQL Server 2012 SP1；您也可以選擇 SQL Server 2014。 如需詳細資訊，請參閱[相容性層級&#40;SSAS 表格式 SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)。|  
    |**相容性層級選項**|所有已核取|指定新表格式模型專案以及在部署至其他 Analysis Services 執行個體時的相容性層級選項。|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>若要針對新的模型專案設定預設部署伺服器屬性設定  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，按一下 **[工具]** 功能表，然後按一下 **[選項]**。  
  
2.  在 **[選項]** 對話方塊中，展開 **[Analysis Services 表格式設計師]**，然後按一下 **[部署]**。  
  
3.  設定下列屬性設定：  
  
    |屬性|預設設定|描述|  
    |--------------|---------------------|-----------------|  
    |**預設部署伺服器**|localhost|此設定會指定部署模型時使用的預設伺服器。 您可以按一下向下箭頭，瀏覽可以使用的區域網路 Analysis Services 伺服器，或是輸入遠端伺服器的名稱。|  
  
    > [!NOTE]  
    >  變更 [預設部署伺服器] 屬性設定並不會影響變更前已建立的現有專案。  
  
###  <a name="bkmk_conf_default"></a> 若要針對新的模型專案設定預設工作空間資料庫屬性設定  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，按一下 **[工具]** 功能表，然後按一下 **[選項]**。  
  
2.  在 **[選項]** 對話方塊中，展開 **[Analysis Services 表格式設計師]**，然後按一下 **[工作空間資料庫]**。  
  
3.  設定下列屬性設定：  
  
    |屬性|預設設定|描述|  
    |--------------|---------------------|-----------------|  
    |**預設工作空間伺服器**|**localhost**|此屬性指定在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中撰寫模型時，用來主控工作空間資料庫的預設伺服器。 在本機電腦上執行的所有可用 Analysis Services 執行個體都包含在清單方塊中。<br /><br /> 注意：建議您一律將本機 Analysis Services 伺服器指定為工作空間伺服器。 若是遠端伺服器上的工作空間資料庫，則不支援從 PowerPivot 匯入資料，也無法在本機備份資料，而且使用者介面在查詢期間可能會遇到延遲。|  
    |**在關閉模型之後保留工作空間資料庫**|**將工作空間資料庫保留在磁碟上，但是從記憶體卸載**|指定在關閉模型之後，如何保留工作空間資料庫。 工作空間資料庫包含模型中繼資料、匯入模型的資料，以及模擬認證 (已加密)。 在某些情況下，工作空間資料庫可能會非常大，因此耗用大量的記憶體。 依預設，工作空間資料庫會從記憶體中移除。 變更此設定時，最好考慮您的可用記憶體資源，以及您打算處理模型的頻率。 此屬性設定具有以下選項：<br /><br /> **將工作空間保留在記憶體中** ：指定在關閉模型後，將工作空間保留在記憶體中。 此選項會耗用較多的記憶體，但是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟模型時，會耗用較少的資源，而且工作空間將會更快載入。<br /><br /> **‭將工作空間資料庫保留在磁碟上，但是從記憶體中卸載** ：指定在關閉模型後，將工作空間資料庫保留在磁碟上，但不再保留在記憶體中。 此選項將耗用較少的記憶體，但是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]開啟模型時，將耗用額外的資源，而且模型的載入速度比將工作空間資料庫保留在記憶體中更慢。 當記憶體中的資源有限，或者當處理遠端工作空間資料庫時，請使用此選項。<br /><br /> **刪除工作空間** ：指定在關閉模型後，即從記憶體刪除工作空間資料庫，而且不將工作空間資料庫保留在磁碟上。 此選項將耗用較少的記憶體，但是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]開啟模型時，將耗用額外的資源，而且模型的載入速度比將工作空間資料庫保留在記憶體中更慢。 只有在偶爾處理模型時，才使用此選項。|  
    |**資料備份**|**在磁碟上保留資料備份**|指定是否要將模型資料的備份保留在備份檔中。 此屬性設定具有以下選項：<br /><br /> **在磁碟上保留資料備份** ：指定要將模型資料的備份保留在磁碟上。 儲存模型時，也會將資料儲存到備份 (ABF) 檔。 選取此選項可能會使模型的儲存和載入速度更慢。<br /><br /> **不要在磁碟上保留資料備份** ：指定不要將模型資料的備份保留在磁碟上。 此選項會將模型的儲存和載入時間降至最低。|  
  
> [!NOTE]  
>  變更預設模型屬性並不會影響變更前已建立之現有模型的屬性。  
  
## <a name="see-also"></a>另請參閱  
 [專案屬性&#40;SSAS 表格式&#41;](properties-ssas-tabular.md)   
 [模型屬性的&#40;SSAS 表格式&#41;](model-properties-ssas-tabular.md)   
 [相容性層級&#40;SSAS 表格式 SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  