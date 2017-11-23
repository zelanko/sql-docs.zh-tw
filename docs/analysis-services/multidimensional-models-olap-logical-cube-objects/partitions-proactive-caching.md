---
title: "主動式快取 （資料分割） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- hybrid OLAP
- partitions [Analysis Services], proactive caching
- relational OLAP
- multidimensional OLAP
- MOLAP
- proactive caching [Analysis Services]
- ROLAP
- cache [Analysis Services]
ms.assetid: 422660b2-4d80-4165-b1c9-3963bcde556b
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9b6a653ac28762dc391c0999a4ac179dd0ad2095
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="partitions---proactive-caching"></a>資料分割-主動式快取
  主動式快取會提供自動 MOLAP 快取建立及 OLAP 物件的管理。 Cube 會根據從資料庫接收而來的通知，立即併入對資料庫資料所做的變更。 主動式快取的目標是要提供傳統 MOLAP 的效能，同時保持 ROLAP 所提供的立即性與便於管理性。  
  
 簡單的 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件是由時間指定和資料表通知所組成。 時間指定會定義在收到變更通知以後，用於更新快取的時間範圍。 資料表通知會定義在資料表與 <xref:Microsoft.AnalysisServices.ProactiveCaching> 物件之間的通知結構描述。  
  
 多維度 OLAP (MOLAP) 儲存提供最佳查詢回應，但有些資料延遲是其負面影響。 即時關聯式 OLAP (ROLAP) 儲存可讓使用者立即瀏覽資料來源的最新變更，但效能比多維度 OLAP (MOLAP) 儲存差很多是其負面影響，因為資料缺乏預先導出摘要，且因為關聯式儲存不是 OLAP 式查詢的最佳方式。 如果使用者需要在您的應用程式中查看最新資料，而且您也想要擁有 MOLAP 儲存的效能優勢，SQL Server Analysis Services 提供了主動式快取的選擇來應付這個狀況，特別是在結合使用資料分割時。 主動式快取的設定是以每個資料分割和每個維度為準， 主動式快取選項可以在 MOLAP 儲存的增強式效能及 ROLAP 儲存的立即性之間提供平衡，並在基礎資料變更時或是根據設定的排程來提供自動資料分割處理。  
  
## <a name="proactive-caching-configuration-options"></a>主動式快取組態選項  
 SQL Server Analysis Services 提供數個主動式快取組態選項，可讓您將效能最大化、將延遲最小化，及排程處理。 主動式快取功能可簡化處理資料陳舊過時的過程。 主動式快取設定會決定多維度 OLAP 結構 (也稱為 MOLAP 快取) 的重建頻率、重建快取時會查詢過期的 MOLAP 儲存還是基礎 ROLAP 資料來源，以及重建快取時是依照排程還是根據資料庫中的變更。  
  
### <a name="minimizing-latency"></a>將延遲最小化  
 當主動式快取設為將延遲最小化時，會根據資料最近是否發生變更以及設定主動式快取的方式，對 ROLAP 儲存或 MOLAP 儲存提出 OLAP 物件的使用者查詢。 查詢引擎會將查詢引導至 MOLAP 儲存的來源資料，直到資料來源發生變更為止。 為了將延遲減至最少，資料來源中發生變更之後，可以卸除快取的 MOLAP 物件，而當 MOLAP 物件在快取中重建時，查詢會切換至 ROLAP 儲存。 當 MOLAP 物件重建及處理之後，查詢會自動切換回 MOLAP 儲存。 在小的資料分割中 (如目前的資料分割，可能會和當日的資料一樣小)，會以極快的速度重新整理快取。  
  
### <a name="maximizing-performance"></a>將效能最大化  
 為了要將效能提升到最高，同時也減少延遲，也可以在不卸除目前 MOLAP 物件的情況下使用快取。 於是，查詢會繼續針對 MOLAP 物件提出，但資料則讀入新的快取中加以處理。 此方法提供更好的效能，但會導致在建立新快取時，查詢仍傳回舊資料。  
  
## <a name="see-also"></a>請參閱＜  
 [維度儲存](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)   
 [設定分割區儲存 &#40;Analysis Services - 多維度&#41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)  
  
  
