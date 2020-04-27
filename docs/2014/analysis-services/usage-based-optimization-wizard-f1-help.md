---
title: 基於使用方式的優化嚮導 F1 說明 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.f1
helpviewer_keywords:
- Usage-Based Optimization Wizard
ms.assetid: e5f5a938-ae7c-4f4e-9416-a7f94ac82763
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e94818245ba1e87d90f87539ae07e9531e5450
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66065564"
---
# <a name="usage-based-optimization-wizard-f1-help"></a>基於使用方式的最佳化精靈 F1 說明
  基於使用方式的最佳化精靈，在輸出方面類似於彙總設計精靈，並可用於設計資料分割的彙總。 然而，基於使用方式的最佳化精靈會依據查詢的特定使用模式來設計彙總，而這些使用模式是記錄於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的查詢記錄檔中。 匯總藉由允許[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]直接從 cube 儲存體抓取預先計算的總計，而不需要重新計算每個查詢之基礎資料來源中的資料，來改善效能。  
  
 若要從開啟 [基於使用方式的優化[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]嚮導]，請開啟[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]專案的 cube 設計師，然後按一下 [**匯總] 索引**標籤。按一下工具列中的 [以使用量為基礎的**優化**] 按鈕。  
  
 若要從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 開啟 [基於使用方式的最佳化精靈]，請連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，然後開啟 [Cubes]**** 資料夾。 選取一個 Cube，接著開啟 **[Measure Groups]** 資料夾，並展開您要修改的量值群組。 以滑鼠右鍵按一下 [資料分割]**** 資料夾，然後選取 [基於使用方式的最佳化]****。  
  
 若要設計這些彙總，您可以使用彙總設計精靈。 這個精靈會引導您執行下列步驟：  
  
-   針對資料分割、量值群組或 Cube 的儲存和快取選項，選取標準或自訂設定。  
  
-   提供資料分割、量值群組或 Cube 所參考之物件的估計或實際計數。  
  
-   指定彙總選項與限制，將設計彙總所提供的儲存和查詢效能最佳化。  
  
-   儲存和選擇性地處理資料分割、量值群組或 Cube，以產生定義的彙總。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的彙總設計精靈，可以依據資料分割結構的統計分析來設計彙總，以提供可受儲存體大小或估計之效能改善限制的彙總設計。 您可以使用彙總設計精靈來改善資料分割的整體效能，但是其中的彙總設計不一定適用於商務使用者的特定需求。 基於使用方式的最佳化精靈可以提供針對這些特定需求的彙總設計，但前提是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的查詢記錄檔必須包含足以建構這種查詢的資訊。  
  
 通常這兩種精靈都會搭配使用，以改善部署之初以及經過一段時間之後的效能。 在最初部署資料分割 (或包含資料分割的 Cube 或量值群組) 時，應先使用彙總設計精靈，才能提供整體效能上的益處。 在查詢記錄檔中記錄了商務使用者針對資料分割的查詢一段時間之後，您就可以使用基於使用方式的最佳化精靈，進一步改善彙總設計，將重點放在滿足商務使用者對於效能及查詢的需求上。  
  
> [!NOTE]  
>   如需有關設定查詢記錄的詳細資訊，請參閱＜ [設定 Analysis Services 查詢記錄](instances/log-operations-in-analysis-services.md?view=sql-server-2014#bkmk_querylog)＞(英文)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [選取 [分割區] 以修改 &#40;以使用方式為基礎的優化 Wizard&#41;](select-partitions-to-modify-usage-based-optimization-wizard.md)  
  
-   [指定查詢準則 &#40;基於使用方式的優化 Wizard&#41;](specify-query-criteria-usage-based-optimization-wizard.md)  
  
-   [查看將優化的查詢，&#40;基於使用方式的優化 Wizard&#41;](review-the-queries-that-will-be-optimized-usage-based-optimization-wizard.md)  
  
-   [查看匯總使用量 &#40;以使用方式為基礎的基於優化 Wizard&#41;](review-aggregation-usage-usage-based-optimiation-wizard.md)  
  
-   [指定物件計數 &#40;以使用方式為基礎的優化 Wizard&#41;](specify-object-counts-usage-based-optimization-wizard.md)  
  
-   [設定匯總選項 &#40;基於使用方式的優化 Wizard&#41;](set-aggregation-options-usage-based-optimization-wizard.md)  
  
-   [正在完成 Wizard &#40;基於使用方式的優化 Wizard&#41;](completing-the-wizard-usage-based-optimization-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
 [匯總和匯總設計](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [多維度模型中的 cube](multidimensional-models/cubes-in-multidimensional-models.md)   
 [匯總設計嚮導 F1 說明](aggregation-design-wizard-f1-help.md)   
 [Analysis Services 的 &#40;多維度資料的嚮導&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
