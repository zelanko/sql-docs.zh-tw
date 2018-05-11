---
title: 設定量值群組屬性 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f6aa82d79fab41e5cd0000c4a8337470309ca71
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="configure-measure-group-properties"></a>設定量值群組屬性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  量值群組有一些屬性可讓您定義量值群組的運作方式。  
  
## <a name="measure-group-properties"></a>量值群組屬性  
 量值群組屬性會決定整個量值群組的行為，以及設定量值群組內量值之某些屬性的預設行為。  
  
|屬性|定義|  
|--------------|----------------|  
|**AggregationPrefix**|套用至 ROLAP 儲存體。 指派一般的前置詞給 SQL Server 中的索引檢視表，以供儲存此量值群組所關聯之資料分割的彙總。|  
|**DataAggregation**|此屬性保留供日後使用，目前沒有任何作用。 建議您不要修改此設定。|  
|**說明**|您可以使用此屬性記錄量值群組。|  
|**ErrorConfiguration**|用於處理重複索引鍵、未知索引鍵、Null 索引鍵、錯誤限制、偵測到錯誤時的動作和錯誤記錄檔的可設定錯誤處理設定。 請參閱[設定 Cube、資料分割和維度處理時發生錯誤 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)。|  
|**EstimatedRows**|指定事實資料表中的估計資料列數目。|  
|**EstimatedSize**|指定量值群組的估計大小 (以位元組為單位)。|  
|**識別碼**|指定物件的識別碼。|  
|**IgnoreUnrelatedDimensions**|決定當查詢中包含與量值群組不相關的維度成員時，是否將不相關的維度強制在其最上層。 預設設定是 **True**。|  
|**名稱**|量值的名稱。 此屬性是唯讀的。|  
|**ProactiveCaching**|用於處理重複索引鍵、未知索引鍵、Null 索引鍵、錯誤限制、偵測到錯誤時的動作和錯誤記錄檔的可設定錯誤處理設定。|  
|**ProcessingMode**|指出在處理期間或處理之後，是否應該進行檢索和彙總。 選項為 Regular 和 LazyAggregations。 LazyAggregations 可以用於將彙總以背景工作方式執行。|  
|**ProcessingPriority**|決定 Cube 在背景作業 (例如延遲彙總和索引) 期間的處理優先權。 預設值是 **0**。|  
|**StorageLocation**|量值群組的檔案系統儲存位置。 如果未指定，則會從包含該量值群組的 Cube 中繼承位置。|  
|**StorageMode**|量值群組的儲存模式。 可用的值為 MOLAP、ROLAP 或 HOLAP。|  
|**型別**|指定量值群組的類型。|  
  
  
