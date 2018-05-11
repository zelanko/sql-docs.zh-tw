---
title: 資料採礦屬性 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17a0f6259524e40b2c2f6b22655c1ebe9feb2c1b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-properties"></a>資料採礦屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的資料採礦伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於** ：僅限於多維度伺服器模式  
  
## <a name="non-specific-category"></a>非特定類別目錄  
 **AllowSessionMiningModels**  
 此為布林值屬性，指出是否可以建立工作階段採礦模型。  
  
 此屬性的預設值為 False，表示無法建立工作階段採礦模型。  
  
 **AllowAdHocOpenRowsetQueries**  
 此為布林值屬性，指出是否允許特定開啟資料列集查詢。  
  
 此屬性的預設值為 False，表示在工作階段期間不允許開啟資料列集查詢。  
  
 **AllowedProvidersInOpenRowset**  
 此字串屬性會識別開啟的資料列集內所允許的提供者，其中會由提供者 ProgID 的逗號/分號分隔清單或是 [全部] 所組成。  
  
 **MaxConcurrentPredictionQueries**  
 此為帶正負號的 32 位元整數屬性，定義並行預測查詢的最大數目。  
  
## <a name="algorithms-category"></a>演算法類別目錄  
 **Microsoft_Association_Rules\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Association_Rules 演算法。  
  
 **Microsoft_Clustering\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Clustering 演算法。  
  
 **Microsoft_Decision_Trees\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_DecisionTrees 演算法。  
  
 **Microsoft_Naive_Bayes\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_ Naive_Bayes 演算法。  
  
 **Microsoft_Neural_Network\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Neural_Network 演算法。  
  
 **Microsoft_Sequence_Clustering\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Sequence_Clustering 演算法。  
  
 **Microsoft_Time_Series\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Time_Series 演算法。  
  
 **Microsoft_Linear_Regression\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Linear_Regression 演算法。  
  
 **Microsoft_Logistic_Regression\ Enabled**  
 此為布林值屬性，指出是否啟用 Microsoft_Logistic_Regression 演算法。  
  
> [!NOTE]  
>  除了定義伺服器上可用之資料採礦服務的屬性以外，還有其他資料採礦屬性可定義特定演算法的行為。 當您建立個別資料採礦模型時 (不在伺服器層級上)，可以設定這些屬性。 如需詳細資訊，請參閱[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [實體架構 &#40;Analysis Services – 資料採礦&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
