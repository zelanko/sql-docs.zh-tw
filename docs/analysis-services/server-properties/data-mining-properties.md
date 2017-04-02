---
title: "資料採礦屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "ClusterCount 屬性"
  - "AllowedProvidersInOpenRowset 屬性"
  - "MinimumSeriesValue 屬性"
  - "ScoreMethod 屬性"
  - "MinimumImportance 屬性"
  - "ModellingCardinality 屬性"
  - "BrentTolerance 屬性"
  - "ComplexityPenalty 屬性"
  - "MaximumItemsetCount 屬性"
  - "MinimumSupport 屬性"
  - "AllowSessionMiningModels 屬性"
  - "HoldoutPercentage 屬性"
  - "ClusterCountPrior 屬性"
  - "MaximumSequenceStates 屬性"
  - "OptimizedPredictionCount 屬性"
  - "資料採礦 [Analysis Services], 屬性"
  - "MaximumStates 屬性"
  - "MaximumContinuousInputAttributes 屬性"
  - "MaximumOutputAttributes 屬性"
  - "AllowAdHocOpenRowsetQueries 屬性"
  - "Enabled 屬性"
  - "HistoricModelGap 屬性"
  - "SampleSize 屬性"
  - "MaximumInputAttributes 屬性"
  - "PeriodicityHint 屬性"
  - "MissingValueSubstitution 屬性"
  - "SplitMethod 屬性"
  - "ForceRegressor 屬性"
  - "MaximumBucketsForContinuousSplit 屬性"
  - "MaxConcurrentPredictionQueries 屬性"
  - "MinimumItemsetSize 屬性"
  - "AcyclicGraph 屬性"
  - "HoldoutMethod 屬性"
  - "StoppingTolerance 屬性"
  - "屬性 [資料採礦]"
  - "AutoDetectPeriodicity 屬性"
  - "HoldoutTolerance 屬性"
  - "MinimumLeafCases 屬性"
  - "HoldoutSeed 屬性"
  - "MinimumClusterCases 屬性"
  - "ClusterCountDeviation 屬性"
  - "MinimumDependencyProbability 屬性"
  - "ClusteringMethod 屬性"
  - "MaximumItemsetSize 屬性"
  - "HiddenNodeRatio 屬性"
  - "MaximumSeriesValue 屬性"
ms.assetid: 9bc9abed-180a-4bd8-b2eb-89c62fa88110
caps.latest.revision: 19
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# 資料採礦屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的資料採礦伺服器屬性。 如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **適用於** ：僅限於多維度伺服器模式  
  
## 非特定類別目錄  
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
  
## 演算法類別目錄  
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
  
## 請參閱＜  
 [實體架構 &#40;Analysis Services – 資料採礦&#41;](../../analysis-services/data-mining/physical-architecture-analysis-services-data-mining.md)   
 [Analysis Services 的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  