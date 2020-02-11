---
title: 設定量值群組屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], measure groups
ms.assetid: fa66bdb6-60b8-413c-ac2a-00e4d09f60a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c7571457847d8ffb0388608b7d634cc19261a609
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076664"
---
# <a name="configure-measure-group-properties"></a>設定量值群組屬性
  量值群組有一些屬性可讓您定義量值群組的運作方式。  
  
## <a name="measure-group-properties"></a>量值群組屬性  
 量值群組屬性會決定整個量值群組的行為，以及設定量值群組內量值之某些屬性的預設行為。  
  
|屬性|定義|  
|--------------|----------------|  
|`AggregationPrefix`|套用至 ROLAP 儲存體。 指派一般的前置詞給 SQL Server 中的索引檢視表，以供儲存此量值群組所關聯之資料分割的彙總。|  
|`DataAggregation`|此屬性保留供日後使用，目前沒有任何作用。 建議您不要修改此設定。|  
|`Description`|您可以使用此屬性記錄量值群組。|  
|`ErrorConfiguration`|用於處理重複索引鍵、未知索引鍵、Null 索引鍵、錯誤限制、偵測到錯誤時的動作和錯誤記錄檔的可設定錯誤處理設定。 請參閱[設定 Cube、資料分割和維度處理時發生錯誤 &#40;SSAS - 多維度&#41;](error-configuration-for-cube-partition-and-dimension-processing.md)。|  
|`EstimatedRows`|指定事實資料表中的估計資料列數目。|  
|`EstimatedSize`|指定量值群組的估計大小 (以位元組為單位)。|  
|`ID`|指定物件的識別碼。|  
|`IgnoreUnrelatedDimensions`|決定當查詢中包含與量值群組不相關的維度成員時，是否將不相關的維度強制在其最上層。 預設值是 `True`。|  
|`Name`|量值的名稱。 這個屬性是唯讀的。|  
|`ProactiveCaching`|用於處理重複索引鍵、未知索引鍵、Null 索引鍵、錯誤限制、偵測到錯誤時的動作和錯誤記錄檔的可設定錯誤處理設定。|  
|`ProcessingMode`|指出在處理期間或處理之後，是否應該進行檢索和彙總。 選項為 Regular 和 LazyAggregations。 LazyAggregations 可以用於將彙總以背景工作方式執行。|  
|`ProcessingPriority`|決定 Cube 在背景作業 (例如延遲彙總和索引) 期間的處理優先權。 預設值為**0**。|  
|`StorageLocation`|量值群組的檔案系統儲存位置。 如果未指定，則會從包含該量值群組的 Cube 中繼承位置。|  
|`StorageMode`|量值群組的儲存模式。 可用的值為 MOLAP、ROLAP 或 HOLAP。|  
|`Type`|指定量值群組的類型。|  
  
  
