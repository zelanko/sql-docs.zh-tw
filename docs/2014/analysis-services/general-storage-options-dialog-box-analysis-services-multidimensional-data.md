---
title: 一般（儲存選項對話方塊）（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c7ddd5311232ae12b3eb9f66adc0cd1f5714b32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081013"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>一般 (儲存選項對話方塊) (Analysis Services - 多維度資料)
  在 ** 中，使用 [儲存選項]**** 對話方塊的 [一般]**[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 索引標籤，即可為維度、Cube、量值群組或資料分割設定儲存模式與主動式快取設定。  
  
> [!NOTE]  
>  在您修改這些設定之前，必須先熟悉儲存模式與主動式快取功能。 如需詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**儲存模式**|選取用於物件的儲存模式。<br /><br /> **MOLAP**<br /> 物件使用多維度 OLAP (MOLAP) 儲存。<br /><br /> **HOLAP**<br /> 物件使用混合式 OLAP (HOLAP) 儲存。<br /><br /> **ROLAP**<br /> 物件使用關聯式 OLAP (ROLAP) 儲存。|  
|**啟用主動式快取**|啟用主動式快取。<br /><br /> 注意：如果未選取此選項，則除了 [儲存模式]**** 之外，所有選項都會停用。|  
|**當資料變更時更新快取**|使用 [通知]**** 索引標籤中所選取的通知方法，即可在接收到通知時，更新物件的 MOLAP 影像。 如需 [通知]**** 索引標籤的詳細資訊，請參閱[通知 &#40;儲存選項對話方塊&#41; &#40;Analysis Services - 多維度資料&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)。<br /><br /> 注意：除非選取 [啟用主動式快取]****，否則此選項會停用。|  
|**無回應間隔**|設定在主動式快取開始建立物件的新 MOLAP 影像之前，物件沒有活動的最短間隔與時間單位。<br /><br /> 注意：除非選取 [當資料變更時更新快取]****，否則此選項會停用。|  
|**無回應覆寫間隔**|設定在接收到針對物件的通知之後，主動式快取開始建立物件之新 MOLAP 影像的最長間隔與時間單位 (不論物件的目前活動情況)。 在到達此間隔後收到的通知，不會取消此間隔所觸發的 MOLAP 影像處理。<br /><br /> 注意：除非選取 [當資料變更時更新快取]****，否則此選項會停用。 另請注意，如果**儲存模式**設定為**HOLAP**，就不應該設定此選項。|  
|**卸除過期的快取**|指定在開始建立新的 MOLAP 快取與移除現有 MOLAP 快取之間的期間。<br /><br /> 注意：除非選取 [啟用主動式快取]****，否則此選項會停用。 另請注意，如果**儲存模式**設定為 HOLAP，就不應該設定此選項。|  
|**延遲**|指定在開始建立新 MOLAP 快取與移除現有 MOLAP 快取之間的期間之間隔及時間單位。<br /><br /> 注意：除非選取了 [卸除過期的快取]****，否則此選項會停用。 另請注意，如果**儲存模式**設定為**HOLAP**，就不應該設定此選項。|  
|**定期更新快取**|不論是否接收到通知，都會定期更新 MOLAP 影像。<br /><br /> 注意：除非選取 [啟用主動式快取]****，否則此選項會停用。 另請注意，如果**儲存模式**設定為**HOLAP**，就不應該設定此選項。|  
|**重建間隔**|選取期間的間隔和時間單位，在建立[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]新的 MOLAP 影像之後，就會再次針對物件啟動 MOLAP 影像處理（不論是否有通知）。 在到達此間隔後收到的通知，不會取消此間隔所觸發的 MOLAP 影像處理。<br /><br /> 注意：除非選取了 [定期更新快取]****，否則此選項會停用。 另請注意，如果**儲存模式**設定為**HOLAP**，就不應該設定此選項。|  
|**立即線上工作**|使物件立即到線上工作。 如果設定了此選項，在重建 MOLAP 快取的期間，物件就會使用基礎 ROLAP 儲存體來解析查詢。 如果未設定此選項，只有在完成了物件的 MOLAP 快取之後，才會使物件上線。|  
|**啟用 ROLAP 彙總**|在基礎資料來源上使用具體化檢視來儲存彙總。<br /><br /> 注意：如果基礎資料來源不支援具體化檢視，在處理物件時就會發生錯誤。|  
|**套用設定至維度**|將儲存模式及主動式快取設定，套用到相關聯的維度。|  
  
## <a name="see-also"></a>另請參閱  
 [[儲存選項] 對話方塊 &#40;Analysis Services-多維度資料&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [[通知] &#40;[儲存選項] 對話方塊&#41; &#40;Analysis Services 多維度資料&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  
