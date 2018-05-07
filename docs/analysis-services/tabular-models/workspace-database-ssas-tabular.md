---
title: SQL Server Data Tools 中的工作空間資料庫 |Microsoft 文件
ms.custom: ''
ms.date: 03/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 30fc4cfad99cc88a92a986c8c55fc5c0ef75115b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="workspace-database"></a>工作區資料庫 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立新的表格式模型專案時，會建立表格式模型工作區資料庫 (模型撰寫期間所使用)。
  
## <a name="specifying-a-workspace-instance"></a>指定工作區執行個體  
  當您在 SSDT 中建立新的表格式模型專案時，可以指定撰寫專案時所要使用的 Analysis Services 執行個體。 自 2016 年 9 月發行的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]版本 (14.0.60918.0) 中引進了兩種模式，可讓您在建立新的表格式模型專案時，指定工作區執行個體。 

**整合式工作區** - 使用 SSDT 自己的內部 Analysis Services 執行個體。

**工作區伺服器** - 直接在 Analysis Services 執行個體上建立工作區資料庫，通常會在 SSDT 所在的同一部電腦上，或同一網路中的另一部電腦上。
  
### <a name="integrated-workspace"></a>整合式工作區
使用整合式工作區會使用 SSDT 自己隱含的 Analysis Services 執行個體，在記憶體內建立工作資料庫。 整合式工作區模式因為不需要另外特別安裝的 SQL Server Analysis Services，所以大幅降低在 SSDT 中撰寫表格式專案的複雜性。

使用整合式工作區模式讓 SSDT 表格式得以動態方式，在背景啟動自己內部的 SSAS 執行個體並載入資料庫。 您可以在模型設計工具中新增並檢視資料表、資料行與資料。 若新增其他資料表、資料行、關聯性等等，即會修改工作區資料庫。 整合式工作區模式不會變更 SSDT 表格式與工作區伺服器及資料庫搭配運作的方式。 變更之處在於 SSDT 表格式裝載工作區資料庫的位置。

您可以在 SSDT 中建立新的表格式模型專案時，選取整合式工作區模式。

![SSAS 整合式工作區模式](../../analysis-services/tabular-models/media/ssas-integrated-workspace-mode.png)

您可以使用 model.bim 的工作區資料庫與工作區伺服器屬性，探索暫存資料庫的名稱，以及 SSDT 表格式裝載資料庫所在之內部 SSAS 執行個體的 TCP 連接埠。 凡是 SSDT 表格式已經載入的資料庫，都可以使用 SSMS 連線到工作區資料庫。 工作區保留設定可指定 SSDT 表格式將工作區資料庫保留在磁碟上，但當模型專案關閉之後，即不會再存在記憶體內。 這會比將模型一直保留在記憶體內所耗用的記憶體少。 若要控制這些設定，請將整合式工作區模式屬性設定為 False，並提供明確的工作區伺服器。 若您要匯入模型的資料超過 SSDT 工作站的記憶體容量，也可提供明確的工作區伺服器。

> [!NOTE]  
>  使用整合式工作區模式時，本機 Analysis Services 執行個體時，64 位元，SSDT 32 位元的環境中執行的 Visual Studio。 若要連線到特殊的資料來源，請務必在您的工作站上安裝對應資料提供者的 32 位元及 64 位元版本。 64 位元提供者則需要 64 位元的 Analysis Services 執行個體，因此在 SSDT 中的資料表匯入精靈需要 32 位元版本。

###  <a name="bkmk_overview"></a> 工作區伺服器  
 當您使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的其中一個表格式模型專案範本建立新的商業智慧專案時，會在工作區伺服器屬性指定的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]執行個體上建立工作區資料庫。 每個表格式模型專案都會有其專屬的工作區資料庫。 您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，檢視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上的工作區資料庫。 工作區資料庫名稱包含專案名稱，後面依序接著底線、使用者名稱、底線及 GUID。  
  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟表格式模型專案時，工作區資料庫仍會存在於記憶體中。 關閉專案時，根據工作區保留屬性，工作區資料庫會保留在記憶體中、儲存至磁碟並從記憶體中移除 (預設)，或從記憶體中移除但不儲存在磁碟上。 如需工作區保留屬性的詳細資訊，請參閱本主題後文中的 [工作區資料庫屬性](#bkmk_ws_prop) 。  
  
 使用資料表匯入精靈或複製/貼上將資料新增到模型專案之後，則當您在模型設計工具中檢視資料表、資料行及資料時，即是在檢視工作區資料庫。 如果您加入其他資料表、資料行、關聯性等，即會變更工作區資料庫。  
  
 當您部署表格式模型專案時，會在 [部署伺服器] 屬性所指定的 Analysis Services 伺服器執行個體上，建立已部署的模型資料庫 (基本上是工作區資料庫的副本)。 如需部署伺服器屬性的詳細資訊，請參閱[專案屬性](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)。  
  
 模型工作區資料庫一般存在於 localhost 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器的本機具名執行個體上。 您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的遠端執行個體主控工作區資料庫；但是由於資料查詢期間的延遲及其他限制，不建議使用此組態。 在理想情況下，即將主控工作區資料庫的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體會與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]位在相同的電腦上。 在主控工作區資料庫之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體所在的相同電腦上撰寫模型專案可提升效能。  
  
 遠端工作區資料庫具有下列限制：  
  
-   在查詢期間可能會發生延遲。  
  
-   無法將 [資料備份] 屬性設為 [備份到磁碟]。  
  
-   當您建立新的表格式模型專案時，不能使用 [從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 匯入] 專案範本從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿匯入資料。  
  
  > [!IMPORTANT]  
>  模型的相容性層級和工作區伺服器必須對應。
  
> [!NOTE]  
>  如果模型中的任何資料表將包含大量資料列，請考慮只在模型撰寫期間匯入某個資料子集。 您可以藉由匯入資料子集來減少處理時間及工作區資料庫伺服器資源的耗用量。  
  
> [!NOTE]  
>  [資料表匯入精靈] 的 [選取資料表和檢視表] 頁面、[編輯資料表屬性] 對話方塊及 [資料分割管理員] 對話方塊中的預覽視窗會顯示資料來源的資料表、資料行及資料列，且可能與工作區資料庫中的資料表、資料行及資料列不同。  
  
  
##  <a name="bkmk_ws_prop"></a> 工作區資料庫屬性  
 工作區資料庫屬性包含在模型屬性中。 若要檢視模型屬性，請在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 的方案總管中，按一下 [Model.bim] 檔案。 模型屬性可以使用 [屬性] 視窗進行設定。 工作區資料庫的特定屬性包括：  
  
> [!NOTE]  
>  當您建立新的模型專案時，會對**整合工作區模式**、**工作區伺服器**、**工作區保留**及**資料備份**套用預設值。 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [Analysis Server] 設定中，變更新模型專案的預設設定。 您也可以在 [屬性] 視窗中，為每個模型專案設定上述屬性及其他屬性。 變更預設設定不會套用至已建立的模型專案。 如需詳細資訊，請參閱[設定預設資料模型和部署屬性](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)。  
  
|屬性|預設值|Description|  
|--------------|---------------------|-----------------|  
|**整合工作區模式**|True、False|若在建立專案時，為工作區資料庫選取整合式工作區模式，此屬性會是 True。 若在建立專案時選取了 **工作區伺服器** ，此屬性會是 False。 | 
|**工作區資料庫**|名稱|工作區資料庫的名稱。 當 [整合工作區模式] 為 [True] 時，無法編輯此屬性。|  
|**工作空間保留**|從記憶體中卸載|指定在關閉模型專案之後，如何保留工作區資料庫。 工作區資料庫包含模型中繼資料及匯入的資料。 在某些情況下，工作區資料庫可能會非常大，因此耗用大量的記憶體。 依預設，當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中關閉模型專案時，會從記憶體中卸載工作區資料庫。 變更此設定時，最好考慮您的可用記憶體資源，以及您打算處理模型專案的頻率。 此屬性設定具有以下選項：<br /><br /> **保留在記憶體中** - 指定在關閉模型專案後，將工作區資料庫保留在記憶體中。 此選項將耗用較多的記憶體，但是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟模型專案時，將耗用較少的資源，而且工作區資料庫將會更快載入。<br /><br /> **從記憶體中卸載** - 指定在關閉模型專案後，將工作區資料庫保留在磁碟上，但不再保留在記憶體中。 這個選項會耗用較少記憶體，不過，當您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟模型專案時，必須重新附加工作區資料庫；此外，還會耗用額外的資源且模型專案載入會比較慢 (與工作區資料庫保留在記憶體中相比)。 當記憶體中的資源有限，或者當處理遠端工作區資料庫時，請使用此選項。<br /><br /> **刪除工作區** ：指定在關閉模型專案後，從記憶體中刪除工作區資料庫，而且不將工作區資料庫保留在磁碟上。 此選項將耗用較少的記憶體和儲存空間，但是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中開啟模型專案時，將耗用額外的資源，而且模型專案的載入速度比將工作區資料庫保留在記憶體或磁碟中更慢。 只有在偶爾處理模型專案時，才使用此選項。<br /><br /> 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [Analysis Server] 設定中，變更此屬性的預設設定。 當 [整合工作區模式] 為 [True] 時，無法編輯此屬性。|  
|**工作空間伺服器**|localhost|此屬性指定在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中撰寫模型專案時，用來裝載工作區資料庫的預設伺服器。 在本機電腦上執行的所有可用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體都包含在清單方塊中。<br /><br /> 若要指定其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器 (以表格式模式執行)，請輸入伺服器名稱。 登入的使用者必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器上的管理員。<br /><br /> 請注意，建議您指定本機 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器作為工作區伺服器。 若是遠端伺服器上的工作區資料庫，則不支援從 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 匯入，也無法在本機備份資料，而且使用者介面在查詢期間可能會遇到延遲。<br /><br /> 您可以在 [資料模型化] 頁面之 [工具\選項] 對話方塊的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 設定中，變更此屬性的預設設定。 當 [整合工作區模式] 為 [True] 時，無法編輯此屬性。|  
  
##  <a name="bkmk_use_ssms"></a> 使用 SSMS 管理工作區資料庫  
 您可以使用 SQL Server Management Studio (SSMS) 連接線到裝載工作區資料庫伺服器的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 通常，無須對工作區資料庫進行管理；例外的情況是卸離或刪除工作區資料庫，這必須從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行。 在模型設計師中開啟專案時，請勿使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 管理工作區資料庫。 這麼做會導致資料遺失。
   
## <a name="see-also"></a>另請參閱  
[模型屬性](../../analysis-services/tabular-models/model-properties-ssas-tabular.md) 
  
  
