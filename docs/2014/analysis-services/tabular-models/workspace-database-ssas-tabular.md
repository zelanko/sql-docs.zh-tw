---
title: 工作空間資料庫 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8708bd3f4375179638ce5e86a0619a1e1ccf4d77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066262"
---
# <a name="workspace-database-ssas-tabular"></a>工作空間資料庫 (SSAS 表格式)
  當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中建立新的表格式模型專案時，會建立表格式模型工作空間資料庫 (模型撰寫期間所使用)。 工作空間資料庫存在於以表格式模式執行之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的記憶體中，通常會與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 位在相同的電腦上。  
  
 本主題包含下列各節：  
  
-   [工作空間資料庫概觀](#bkmk_overview)  
  
-   [工作區資料庫屬性](#bkmk_ws_prop)  
  
-   [使用 SSMS 管理工作空間資料庫](#bkmk_use_ssms)  
  
-   [相關工作](#bkmk_related_tasks)  
  
##  <a name="bkmk_overview"></a> 工作空間資料庫概觀  
 當您使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的其中一個表格式模型專案範本建立新的商業智慧專案時，會在工作區伺服器屬性指定的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]執行個體上建立工作區資料庫。 每個表格式模型專案都會有其專屬的工作區資料庫。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，檢視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上的工作區資料庫。 工作區資料庫名稱包含專案名稱，後面依序接著底線、使用者名稱、底線及 GUID。  
  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟表格式模型專案時，工作區資料庫仍會存在於記憶體中。 關閉專案時，根據工作區保留屬性，工作區資料庫會保留在記憶體中、儲存至磁碟並從記憶體中移除 (預設)，或從記憶體中移除但不儲存在磁碟上。 如需 [工作空間保留] 屬性的詳細資訊，請參閱本主題稍後的[工作空間資料庫屬性](#bkmk_ws_prop)。  
  
 使用資料表匯入精靈或透過複製/貼上將資料加入至模型專案之後，當您在模型設計師中檢視資料表、資料行及資料時，即會檢視工作空間資料庫。 如果您加入其他資料表、資料行、關聯性等，即會變更工作空間資料庫。  
  
> [!IMPORTANT]  
>  如果模型中的任何資料表將包含大量資料列，請考慮只在模型撰寫期間匯入某個資料子集。 您可以藉由匯入資料子集來減少處理時間及工作區資料庫伺服器資源的耗用量。  
  
> [!NOTE]  
>  [資料表匯入精靈] 的 [選取資料表和檢視表] 頁面、[編輯資料表屬性] 對話方塊及 [資料分割管理員] 對話方塊中的預覽視窗會顯示資料來源的資料表、資料行及資料列，且可能與工作空間資料庫中的資料表、資料行及資料列不同。  
  
 當您部署表格式模型專案時，會在 [部署伺服器] 屬性所指定的 Analysis Services 伺服器執行個體上，建立已部署的模型資料庫 (基本上是工作空間資料庫的副本)。 如需 [部署伺服器] 屬性的詳細資訊，請參閱[專案屬性 &#40;SSAS 表格式&#41;](properties-ssas-tabular.md)。  
  
 模型工作區資料庫一般存在於 localhost 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器的本機具名執行個體上。 您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的遠端執行個體主控工作區資料庫；但是由於資料查詢期間的延遲及其他限制，不建議使用此組態。 在理想情況下，即將主控工作區資料庫的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]位在相同的電腦上。 在主控工作區資料庫之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體所在的相同電腦上撰寫模型專案可提升效能。  
  
 遠端工作區資料庫具有下列限制：  
  
-   在查詢期間可能會發生延遲。  
  
-   無法將 [資料備份] 屬性設為 [備份到磁碟]  。  
  
-   當您建立新的表格式模型專案時，不能使用 [從 PowerPivot 匯入] 專案範本從 PowerPivot 活頁簿匯入資料。  
  
##  <a name="bkmk_ws_prop"></a> 工作區資料庫屬性  
 工作區資料庫屬性包含在模型屬性中。 若要檢視模型屬性，請在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的方案總管  中，按一下 [Model.bim]  檔案。 模型屬性可以使用 [屬性]  視窗進行設定。 工作空間資料庫的特定屬性包括：  
  
> [!NOTE]  
>  當您建立新的模型專案時，[工作空間伺服器]  、[工作空間保留]  及 [資料備份]  屬性會套用預設值。 您可以在 [資料模型化]  頁面之 [工具\選項] 對話方塊的 [Analysis Server]  設定中，變更新模型專案的預設設定。 您也可以在 [屬性]  視窗中，為每個模型專案設定上述屬性及其他屬性。 變更預設設定不會套用至已建立的模型專案。 如需詳細資訊，請參閱 [設定預設的資料模型和部署屬性 &#40;SSAS 表格式&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
|屬性|預設值|描述|  
|--------------|---------------------|-----------------|  
|**工作空間資料庫**|專案名稱，後面依序接著底線、使用者名稱、底線及 GUID。|工作空間資料庫的名稱，用於儲存及編輯記憶體中的模型專案。 建立表格式模型專案之後，此資料庫會出現在 [工作空間伺服器]  屬性所指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體中。 您無法在 [屬性] 視窗中設定此屬性。|  
|**工作空間保留**|在記憶體中卸載|指定在關閉模型專案之後，如何保留工作區資料庫。 工作區資料庫包含模型中繼資料及匯入的資料。 在某些情況下，工作區資料庫可能會非常大，因此耗用大量的記憶體。 依預設，當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中關閉模型專案時，會從記憶體中卸載工作區資料庫。 變更此設定時，最好考慮您的可用記憶體資源，以及您打算處理模型專案的頻率。 此屬性設定具有以下選項：<br /><br /> **保留在記憶體中** - 指定在關閉模型專案後，將工作區資料庫保留在記憶體中。 此選項將耗用較多的記憶體，但是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟模型專案時，將耗用較少的資源，而且工作區資料庫將會更快載入。<br /><br /> **從記憶體中卸載** - 指定在關閉模型專案後，將工作區資料庫保留在磁碟上，但不再保留在記憶體中。 這個選項會耗用較少記憶體，不過，當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟模型專案時，必須重新附加工作區資料庫；此外，還會耗用額外的資源且模型專案載入會比較慢 (與工作區資料庫保留在記憶體中相比)。 當記憶體中的資源有限，或者當處理遠端工作區資料庫時，請使用此選項。<br /><br /> **刪除工作區** ：指定在關閉模型專案後，從記憶體中刪除工作區資料庫，而且不將工作區資料庫保留在磁碟上。 此選項將耗用較少的記憶體和儲存空間，但是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟模型專案時，將耗用額外的資源，而且模型專案的載入速度比將工作區資料庫保留在記憶體或磁碟中更慢。 只有在偶爾處理模型專案時，才使用此選項。<br /><br /> <br /><br /> 您可以在 [資料模型化]  頁面之 [工具\選項] 對話方塊的 [Analysis Server]  設定中，變更此屬性的預設設定。|  
|**工作空間伺服器**|localhost|此屬性指定在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中撰寫模型專案時，用來裝載工作區資料庫的預設伺服器。 在本機電腦上執行的所有可用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體都包含在清單方塊中。<br /><br /> 若要指定其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器 (以表格式模式執行)，請輸入伺服器名稱。 登入的使用者必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上的管理員。<br /><br /> 請注意，建議您指定本機[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]為工作空間伺服器的伺服器。 針對遠端伺服器上的工作空間資料庫，並不支援從 PowerPivot 匯入，也無法在本機上備份資料，且使用者介面在查詢期間可能會發生延遲。<br /><br /> 也請注意，可以在資料模型化 頁面中變更此屬性的預設設定[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)][工具] 對話方塊中的設定。|  
  
##  <a name="bkmk_use_ssms"></a> 使用 SSMS 管理工作區資料庫  
 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 連接至主控工作空間資料庫的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 通常，無須對工作區資料庫進行管理；例外的情況是卸離或刪除工作區資料庫，這必須從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行。  
  
> [!WARNING]  
>  在模型設計師中開啟專案時，請勿使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 管理工作區資料庫。 這麼做會導致資料遺失。  
  
##  <a name="bkmk_related_tasks"></a> 相關工作  
  
|主題|描述|  
|-----------|-----------------|  
|[模型屬性 &#40;SSAS 表格式&#41;](model-properties-ssas-tabular.md)|提供說明及組態步驟的模型工作空間資料庫屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [設定預設的資料模型和部署屬性 &#40;SSAS 表格式&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [專案屬性 &#40;SSAS 表格式&#41;](properties-ssas-tabular.md)  
  
  
