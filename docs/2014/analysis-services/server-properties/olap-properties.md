---
title: OLAP 屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AggregationPerfLog property
- DefaultPageSizeForProp property
- UseSinglePassForDimSecurityAutoExist property
- DeepCompressValue property
- CacheRowsetRows property
- Income property
- AggregationNewAlgo property
- MemoryAdjustFactor property
- DimensionLatencyAccuracy property
- InitialBonus property
- DefaultPageSizeForDataHeader property
- MaxCPUUsage property
- DistinctBuffer property
- PartitionLatencyAccuracy property
- MaxRetries property
- UseDataCacheRegistryMultiplyKey property
- ConvertDeletedToUnknown property
- DatabaseConnectionPoolMax property
- DataFileInitEnabled property
- DefaultPageSizeForHash property
- MaxRolapOrConditions property
- UseDataCacheFreeLastPageMemory property
- OLAP [Analysis Services], properties
- MapHandleAlgorithm property
- IndexBuildEnabled property
- MaxObjectsInParallel property
- IgnoreNullRolapRows property
- DimensionPropertyCacheSize property
- DefaultRefreshInterval property
- CheckDistinctRecordSortOrder property
- BufferMemoryLimit property
- EnableTableGrouping property
- ExpressNonEmptyUseEnabled property
- CopyLinkedDataCacheAndRegistry property
- UseDataSlice property
- MemoryLimitErrorEnabled property
- Enabled property
- EnableRolapOptimization property
- DatabaseConnectionPoolTimeout property
- UseDataCacheRegistryHashTable property
- AggregationsBuildEnabled property
- Tax property
- DatabaseConnectionPoolGeneralTimeout property
- DefaultPageSizeForString property
- DatabaseConnectionPoolConnectTimeout property
- MinimumBalance property
- OptimizeSchema property
- UseCalculationCacheRegistry property
- MaxTableDepth property
- DataSliceInitEnabled property
- PrefetchLowerGranularities property
- UseVBANet property
- BufferRecordLimit property
- DefaultPageSizeForIndexHeader property
- MaximumBalance property
- CalculationCacheRegistryMaxIterations property
- DefaultDrillthroughMaxRows property
- IndexBuildThreshold property
- UseDataCacheRegistry property
- MemoryAdjustConst property
- ApplyIntersect property
- IndexFileInitEnabled property
- CacheRowsetToDisk property
- DataCacheRegistryMaxIterations property
- AllowSEFiltering property
- ForceMultiPass property
- ApplySubtract property
- IndexUseEnabled property
- AggregationsUseEnabled property
- DataPlacementOptimization property
- UseMaterializedIterators property
- CacheRecordLimit property
- ROLAPDimensionProcessingEffort property
- DefaultPageSizeForIndex property
- EnableRolapDimQueryTableGrouping property
- DimensionPropertyKeyCache property
- SleepIntervalSecs property
- DefaultPageSizeForData property
- MapFormatMask property
- CalculationEvaluationPolicy property
- AggregationMemoryLimitMin property
- RecordsReportGranularity property
- MemoryLimit property
- AggregationMemoryLimitMax property
ms.assetid: 06eb0d78-96c0-42ff-b759-f4c794597c8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b26323f99d0b31cdb31e12b64eabdd2a855d907
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068864"
---
# <a name="olap-properties"></a>OLAP 屬性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援下表列出的 OLAP 伺服器屬性。 如需有關其他伺服器屬性及如何設定伺服器屬性的詳細資訊，請參閱＜ [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)＞。  
  
 **適用於：** 僅限多維度伺服器模式  
  
## <a name="memory"></a>記憶體  
 `DefaultPageSizeForData`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultPageSizeForDataHeader`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultPageSizeForIndex`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultPageSizeForIndexHeader`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultPageSizeForString`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultPageSizeForHash`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultPageSizeForProp`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="lazyprocessing"></a>LazyProcessing  
 `Enabled`  
 此為布林值屬性，指定是否啟用延遲彙總處理。  
  
 `SleepIntervalSecs`  
 此為帶正負號的 32 位元整數屬性，定義伺服器檢查是否有延遲處理作業暫止的間隔 (以秒為單位)。  
  
 `MaxCPUUsage`  
 此為帶正負號的 64 位元雙精確度浮點數屬性，定義延遲處理的最大 CPU 使用率 (以百分比表示)。 伺服器會依據快照集監視平均 CPU 使用。 CPU 超過此臨界值之上是正常的行為。  
  
 此屬性的預設值為 0.5，表示最多有 50% 的 CPU 會專用於延遲處理。  
  
 `MaxObjectsInParallel`  
 此為帶正負號的 32 位元整數屬性，指出可平行延遲處理的最大分割區數目。  
  
 `MaxRetries`  
 此為帶正負號的 32 位元整數屬性，定義在引發錯誤之前，延遲處理失敗事件的重試次數。  
  
## <a name="processplan"></a>ProcessPlan  
 `CacheRowsetRows`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `CacheRowsetToDisk`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DistinctBuffer`  
 此為帶正負號的 32 位元整數屬性，定義用於相異計數的內部緩衝區大小。 增加此值即可加速相異計數處理，但要耗用較多記憶體。  
  
 `EnableRolapDimQueryTableGrouping`  
 此為布林值屬性，指定是否為 ROLAP 維度啟用資料表分組。 如果為 True，在執行階段查詢 ROLAP 維度時，會立即查詢整個 ROLAP 維度資料表 (而非針對每個屬性個別查詢)。  
  
 `EnableTableGrouping`  
 此為布林值屬性，指定是否啟用資料表分組。 如果為 True，在處理維度時，會立即查詢整個維度資料表 (而非針對每個屬性個別查詢)。  
  
 `ForceMultiPass`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MaxTableDepth`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryAdjustConst`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryAdjustFactor`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MemoryLimit`  
 此為帶正負號的 64 位元雙精確度浮點數屬性，定義專用於處理的記憶體數量上限 (以實體記憶體的百分比表示)。  
  
 此屬性的預設值為 65，表示實體記憶體的 65% 可能會專用於 Cube 和維度處理。  
  
 `MemoryLimitErrorEnabled`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `OptimizeSchema`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="proactivecaching"></a>ProactiveCaching  
 `DefaultRefreshInterval`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DimensionLatencyAccuracy`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `PartitionLatencyAccuracy`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="process"></a>處理  
 `AggregationMemoryLimitMax`  
 此為帶正負號的 64 位元雙精確度浮點數屬性，定義可專用於彙總處理的記憶體數量上限 (以實體記憶體的百分比表示)。  
  
 此屬性的預設值為 80，表示實體記憶體的 80% 可能會專用於彙總處理。  
  
 `AggregationMemoryLimitMin`  
 此為帶正負號的 64 位元雙精確度浮點數屬性，定義可專用於彙總處理的記憶體數量下限 (以實體記憶體的百分比表示)。 此值較大時可加速彙總處理，但要耗用較多記憶體。  
  
 此屬性的預設值為 10，表示實體記憶體最少有 10% 將會專用於彙總處理。  
  
 `AggregationNewAlgo`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `AggregationPerfLog2`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `AggregationsBuildEnabled`  
 此為布林值屬性，指定是否啟用彙總建立。 這是不用變更彙總設計即可對彙總建立進行效能評定的機制。  
  
 `BufferMemoryLimit`  
 此為帶正負號的 64 位元雙精確度浮點數屬性，定義處理緩衝區記憶體的限制 (以實體記憶體的百分比表示)。  
  
 此屬性的預設值為 60，表示最多有 60% 的實體記憶體可用於緩衝區記憶體。  
  
 `BufferRecordLimit`  
 此為帶正負號的 32 位元整數屬性，定義處理期間可以緩衝的記錄數目。  
  
 此屬性的預設值為 1048576 (個記錄)。  
  
 `CacheRecordLimit`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `CheckDistinctRecordSortOrder`  
 此為布林值屬性，定義處理分割區時，相異計數查詢結果的排序順序是否有意義。 True 表示排序順序沒有意義，且必須由伺服器進行「檢查」。 處理具有相異計數量值的分割區時，會使用 order-by 將查詢傳送到 SQL。 設定為 False 即可加速處理。  
  
 此屬性的預設值為 True，表示排序順序沒有意義且必須進行檢查。  
  
 `DatabaseConnectionPoolConnectTimeout`  
 此為帶正負號的 32 位元整數屬性，指定開啟新連接時的逾時 (以秒為單位)。  
  
 `DatabaseConnectionPoolGeneralTimeout`  
 此為帶正負號的 32 位元整數屬性，指定與外部 OLEDB 連接一起使用時的資料庫連接逾時 (以秒為單位)。  
  
 `DatabaseConnectionPoolMax`  
 此為帶正負號的 32 位元整數屬性，指定集區資料庫連接的最大數目。  
  
 此屬性的預設值為 50 (個連接)。  
  
 `DatabaseConnectionPoolTimeout`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataFileInitEnabled`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataPlacementOptimization`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataSliceInitEnabled`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DeepCompressValue`  
 此布林值屬性會套用到具 Double 資料類型的量值，以指定是否可壓縮數字而造成數值有效位數的遺失。 值為 False 表示不壓縮，且不會遺失有效位數。  
  
 此屬性的預設值為 True，表示已啟用壓縮且會遺失有效位數。  
  
 `DimensionPropertyKeyCache`  
 此為布林值屬性，指定是否要快取維度屬性索引鍵。 如果索引鍵為非唯一的，則必須設定為 True。  
  
 `IndexBuildEnabled`  
 此為布林值屬性，指定是否在處理上建立索引。 此屬性適用於效能評定和參考。  
  
 `IndexBuildThreshold`  
 此為帶正負號的 32 位元整數屬性，指定資料列計數的臨界值，在此臨界值之下將不會為分割區建立索引。  
  
 這個屬性的預設值為 4096 (個資料列)。  
  
 `IndexFileInitEnabled`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MapFormatMask`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `RecordsReportGranularity`  
 此為帶正負號的 32 位元整數屬性，指定處理期間伺服器記錄追蹤事件的頻率 (以資料列為單位)。  
  
 此屬性的預設值為 1000，表示每 1000 個資料列會記錄追蹤事件一次。  
  
 `ROLAPDimensionProcessingEffort`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="query"></a>查詢  
 `AggregationsUseEnabled`  
 此為布林值屬性，定義在執行階段是否使用預存彙總。 此屬性可以不必變更彙總設計或重新處理而停用彙總，適用於參考和效能評定。  
  
 此屬性的預設值為 True，表示已啟用彙總。  
  
 `AllowSEFiltering`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `CalculationCacheRegistryMaxIterations`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `CalculationEvaluationPolicy`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ConvertDeletedToUnknown`  
 此為布林值屬性，指定刪除的維度成員是否會轉換成未知的成員。  
  
 `CopyLinkedDataCacheAndRegistry`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCacheRegistryMaxIterations`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DefaultDrillthroughMaxRows`  
 此為帶正負號的 32 位元整數屬性，指定從鑽研查詢傳回的最大資料列數目。  
  
 此屬性的預設值為 10000 (個資料列)。  
  
 `DimensionPropertyCacheSize`  
 此為帶正負號的 32 位元整數屬性，指定用來快取查詢所使用之維度成員的記憶體數量 (位元組)。  
  
 預設值是每個屬性階層、每個使用中查詢 4,000,000 個位元組 (4 MB)。 預設值為有一般階層的方案提供平衡的快取大小。 不過，如果您增加此值，有極大量成員 (數百萬名) 或深度階層的維度會執行得更好。  
  
 增加快取大小的含意：  
  
-   當您允許維度快取使用更多記憶體時，記憶體使用量成本會增加。 實際的使用量取決於查詢執行。 並非所有的查詢都會使用最大允許值。  
  
     請注意，這些快取所使用的記憶體會視為不可壓縮，而且會計入 **TotalMemoryLimit**。  
  
-   會影響伺服器上的所有資料庫。 **DimensionPropertyCachesize** 是伺服器範圍屬性。 變更此屬性會影響在目前執行個體上執行的所有資料庫。  
  
 估計維度快取需求的方式：  
  
1.  一開始大量增加大小，決定增加維度快取大小是否有利。 例如，您可能會想要在初始步驟中將預設值加倍。  
  
2.  如果效能明顯改善，請逐步遞減值，直到達到效能和記憶體使用量之間的平衡。  
  
 `ExpressNonEmptyUseEnabled`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `IgnoreNullRolapRows`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `IndexUseEnabled`  
 此為布林值屬性，定義在執行階段是否使用索引。 此屬性適用於參考和效能評定。  
  
 `MapHandleAlgorithm`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `MaxRolapOrConditions`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseCalculationCacheRegistry`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseDataCacheFreeLastPageMemory`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseDataCacheRegistry`  
 此為布林值屬性，指定是否要啟用資料快取登錄，並在其中快取查詢結果 (雖然並非導出結果)。  
  
 `UseDataCacheRegistryHashTable`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseDataCacheRegistryMultiplyKey`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseDataSlice`  
 此為布林值屬性，定義在執行階段是否要針對查詢最佳化使用分割區的資料配量。 此屬性適用於效能評定和參考。  
  
 `UseMaterializedIterators`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseSinglePassForDimSecurityAutoExist`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `UseVBANet`  
 此為布林值屬性，定義是否要針對使用者定義函數使用 VBA .net 組件。  
  
 `CalculationPrefetchLocality\ ApplyIntersect`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `CalculationPrefetchLocality\ ApplySubtract`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `CalculationPrefetchLocality\ PrefetchLowerGranularities`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\  CachedPageAlloc\ Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\  CachedPageAlloc\ InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\  CachedPageAlloc\ MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\  CachedPageAlloc\ MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\  CachedPageAlloc\ Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\CellStore\ Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\CellStore\ InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\CellStore\ MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\CellStore\ MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\CellStore\ Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\ MemoryModel \ Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\ MemoryModel \ InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\ MemoryModel \ MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\ MemoryModel \ MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `DataCache\ MemoryModel\ Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="jobs"></a>中稱為  
 `ProcessAggregation\ MemoryModel\ Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ MemoryModel\ InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ MemoryModel\ MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ MemoryModel\ MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ MemoryModel\ Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessPartition\ Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessPartition \ InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessPartition \ MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessPartition \ MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessPartition \ Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessProperty\ Income`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessProperty\ InitialBonus`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessProperty\ MaximumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessProperty\ MinimumBalance`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
 `ProcessAggregation\ ProcessProperty\ Tax`  
 此為進階屬性，除非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技術支援的指導之下，否則不應隨意變更。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 中設定伺服器屬性](server-properties-in-analysis-services.md)   
 [判斷 Analysis Services 執行個體的伺服器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
