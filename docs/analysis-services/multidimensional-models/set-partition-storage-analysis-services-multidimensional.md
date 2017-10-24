---
title: "設定分割區儲存 (Analysis Services-多維度) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- low latency MOLAP
- standard storage [Analysis Services]
- hybrid OLAP
- automatic MOLAP
- relational OLAP
- multidimensional OLAP
- scheduled MOLAP [Analysis Services]
- partitions [Analysis Services], storage
- HOLAP
- MOLAP
- real time ROLAP
- real time HOLAP
- ROLAP
- medium latency MOLAP
ms.assetid: e525e708-f719-4905-a4cc-20f6a9a3edcd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8915a2890be20925d739ae03098a2f29a1fab8ef
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-partition-storage-analysis-services---multidimensional"></a>設定分割區儲存 (Analysis Services - 多維度)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會針對儲存模式和快取選項提供數個標準儲存組態。 這些會提供更新通知、延遲以及重建資料的常用組態。  
  
 您可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]之 Cube 的 [分割區] 索引標籤，或在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的分割區屬性頁面上，指定分割區儲存。  
  
## <a name="guidelines-for-choosing-a-storage-mode"></a>選擇儲存模式的指導方針  
 針對大型量值群組，為不同的分割區設定不同的儲存是常見的作法。 請考慮下列指導方針：  
  
-   針對持續更新的目前資料，請使用即時 ROLAP。  
  
-   針對以不常更新的資料來源為基礎的分割區，請使用低度延遲或中度延遲的主動式快取。  
  
-   針對使用者需要高效能但可以接受部份資料延遲的資料來源，請使用自動 MOLAP。  
  
-   針對使用者需要能夠連續存取資料但只定期查看變更的資料來源，請使用已排程 MOLAP。  
  
-   針對不常變更或完全不變更的分割區、針對使用者不需要瀏覽最新資料的分割區，以及在任何必要更新和處理期間使用者不必持續存取資料的情況下，請使用無主動式快取的 MOLAP 儲存。  
  
 這些是一般的指導方針，若要為您的資料開發最佳的儲存配置，仍然需要謹慎的分析和測試。 如果標準組態都不符合您的需求，您也可以手動設定分割區的儲存設定。  
  
## <a name="storage-settings-descriptions"></a>儲存設定描述  
  
|標準儲存設定|說明|  
|------------------------------|-----------------|  
|即時 ROLAP|OLAP 係即時進行。 詳細資料和彙總會以關聯式格式儲存。 當資料變更時，伺服器會接聽通知，且所有查詢會反映資料的目前狀態 (零延遲)。<br /><br /> 此設定通常用於會經常和持續更新、且使用者需要最新資料的資料來源。 視用戶端應用程式所產生的查詢類型而定，此方法的回應時間可能最慢。|  
|即時 HOLAP|OLAP 係即時進行。 詳細資料會以關聯式格式儲存，而彙總會以多維度格式儲存。 當資料變更時，伺服器會接聽通知，並視需要重新整理多維度 OLAP (MOLAP) 彙總。 不會建立 MOLAP 快取。 在重新整理彙總之前，每當更新資料來源時，伺服器會切換到即時關聯式 OLAP (ROLAP)。 所有查詢會反映資料的目前狀態 (零延遲)。<br /><br /> 此設定通常用於會經常和持續更新 (但不像即時 ROLAP 需要那麼頻繁)、且使用者需要最新資料的資料來源。 此方法通常會比 ROLAP 儲存提供更好的整體效能。 如果資料來源的無回應時間夠久，此設定可讓使用者達到 MOLAP 的效能。|  
|低度延遲 MOLAP|詳細資料和彙總會以多維度格式儲存。 伺服器會接聽資料變更的通知，並切換到即時 ROLAP，同時重新處理快取中的 MOLAP 物件。 更新快取之前，至少需要 10 秒的無回應間隔。 如果沒有達到無回應間隔，則會產生 10 分鐘的覆寫間隔。 隨著資料變更會自動處理，並以第一次變更之後的 30 分鐘為目標延遲。<br /><br /> 此設定通常用於會經常更新、且查詢效能比持續提供最新資料還稍微重要的資料來源。 必要時，此設定會在延遲間隔之後自動處理 MOLAP 物件。 處理 MOLAP 物件時，效能會變慢。|  
|中度延遲 MOLAP|詳細資料和彙總會以多維度格式儲存。 伺服器會接聽資料變更的通知，並切換到即時 ROLAP，同時重新處理快取中的 MOLAP 物件。 更新快取之前，至少需要 10 秒的無回應間隔。 如果沒有達到無回應間隔，則會產生 10 分鐘的覆寫間隔。 隨著資料變更會自動進行處理，並以四小時為目標延遲。<br /><br /> 此設定通常用於會經常 (或較不常) 更新、且查詢效能比持續提供最新資料更重要的資料來源。 必要時，此設定會在延遲間隔之後自動處理 MOLAP 物件。 處理 MOLAP 物件時，效能會變慢。|  
|自動 MOLAP|詳細資料和彙總會以多維度格式儲存。 伺服器會接聽通知，但在建立新的快取時會保留目前的 MOLAP 快取。 伺服器永不切換到即時 OLAP，且在建立新的快取時，查詢可能過時。<br /><br /> 在建立新的 MOLAP 快取之前，至少需要經過 10 秒的無回應間隔。 如果沒有達到無回應間隔，則會產生 10 分鐘的覆寫間隔。 隨著資料變更會自動進行處理，並以兩小時為目標延遲。<br /><br /> 此設定通常用於查詢效能非常重要的資料來源。 必要時，此設定會在延遲間隔之後自動處理 MOLAP 物件。 正在建立和處理新的快取時，查詢無法傳回最新的資料。|  
|已排程 MOLAP|詳細資料和彙總會以多維度格式儲存。 當資料變更時，伺服器不接收通知。 每隔 24 小時會自動執行處理。<br /><br /> 此設定通常用於只需要每日更新的資料來源。 查詢一律以 MOLAP 快取中的資料為對象，在建立新的快取和處理其物件之後才會捨棄這些資料。|  
|MOLAP|未啟用主動式快取。 詳細資料和彙總會以多維度格式儲存。 當資料變更時，伺服器不接收通知。 必須排程執行或手動執行處理。<br /><br /> 此設定通常用於用戶端應用程式不需要定期更新、但高效能很重要的資料來源。<br /><br /> 如果應用程式不需要最新的資料，則不具主動式快取的 MOLAP 儲存會提供最佳效能。 雖然可以在臨時伺服器上更新和處理 Cube，並使用資料庫同步處理將更新和處理的 MOLAP 物件複製到實際伺服器，藉以將停機時間縮到最短，但實際上並不需要停機來處理更新的物件。|  
  
## <a name="custom-storage-options"></a>自訂儲存選項  
 您可以不使用其中一個標準儲存設定，而以手動方式設定儲存和主動式快取。 在建立自訂儲存設定之前，您可以先按一下 [標準設定] 選項，然後將滑桿移到最符合您想要使用之組態的標準設定。 接著，若要建立自訂組態，請按一下 [自訂設定] 選項，然後按一下 [選項]。  
  
-   您可以指定資料來源中的變更是否觸發快取的更新。 為了要達到可容忍的變更率，您可以指定在資料來源更新之後的最小無回應間隔。 您也可以指定無回應間隔的覆寫，以便資料來源的變更間隔都未達到最小值時，在特定期間之後更新快取。  
  
-   您可以指定是否要在發生更新時卸除過期的快取。 如果您選取此選項，只要超過指定的延遲時間，伺服器在更新快取時就會切換到即時關聯式 OLAP (ROLAP)。 如果您沒有選取此選項，伺服器在建立新快取時仍會繼續查詢過時的多維度 OLAP (MOLAP) 快取。  
  
     您可以指定在變更之間和卸除過期的快取時，必須發生的延遲間隔。 這是使用者在過期的快取被卸除之前，可繼續瀏覽其資料的時間量。 如果發生變更而且在此間隔結束時仍然在更新或處理快取，則查詢會重新導向至 ROLAP。  
  
-   如果不論資料來源是否變更，您都想要定期更新快取的 MOLAP 物件，則可排程強制更新快取。 即時 OLAP 的好處會隨資料庫的大小和來源資料變更頻率所指派的延遲期間而異。 您希望使用者儘量傳送查詢至快取而不是至 ROLAP。  
  
 如果您選取 [套用設定至維度] 核取方塊，相同的儲存設定就會套用至與量值群組相關的維度。 維度值一開始與分割區值相同。  
  
## <a name="see-also"></a>請參閱＜  
 [多維度模型中的分割區](../../analysis-services/multidimensional-models/partitions-in-multidimensional-models.md)  
  
  

