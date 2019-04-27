---
title: 主動式快取 （資料分割屬性對話方塊） (SSMS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.proactivecaching.f1
ms.assetid: ecba72a3-703f-4ede-9d85-9a3318a749e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67ebcc8bcf5c3219d259e4b29eb5c2c737c11df1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748840"
---
# <a name="proactive-caching-partition-properties-dialog-box-ssms"></a>主動式快取 (資料分割屬性對話方塊) (SSMS)
  在 SQL Server Management Studio 中，使用 **[資料分割屬性]** 對話方塊的 **[主動式快取]** 頁面，即可針對 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中的 Cube，設定量值群組中之資料分割的儲存與主動式快取屬性。  
  
## <a name="options"></a>選項。  
 **標準設定**  
 選取以啟用 [標準設定滑桿]，並使用儲存模式與主動式快取功能的預先定義設定。  
  
 **標準設定滑桿**  
 設定為下表所列的預先定義設定之一。  
  
|設定|描述|  
|-------------|-----------------|  
|**即時 ROLAP**|選取以使用下列儲存與主動式快取設定：<br /><br /> ROLAP 儲存模式。<br /><br /> 啟用主動式快取。<br /><br /> 卸除過期的快取，延遲期間為 0 秒。<br /><br /> 使物件立刻回到線上。|  
|**即時 HOLAP**|選取以使用下列儲存與主動式快取設定：<br /><br /> HOLAP 儲存模式。<br /><br /> 啟用主動式快取。<br /><br /> 卸除過期的快取，延遲期間為 0 秒。<br /><br /> 資料變更時更新快取，無回應間隔為 0 秒，沒有無回應覆寫間隔。<br /><br /> 使物件立刻回到線上。|  
|**低度延遲 MOLAP**|選取以使用下列儲存與主動式快取設定：<br /><br /> MOLAP 儲存模式。<br /><br /> 啟用主動式快取。<br /><br /> 卸除過期的快取，延遲期間為 30 分鐘。<br /><br /> 當資料變更，無回應間隔為 10 秒，且無回應覆寫間隔為 10 分鐘時，請更新快取。<br /><br /> 當資料變更，無回應間隔為 10 秒，且無回應覆寫間隔為 10 分鐘時，請更新快取。<br /><br /> 使物件立刻回到線上。|  
|**中度延遲 MOLAP**|立即選取 useBrings 物件上線。<br /><br /> 下列儲存與主動式快取設定：<br /><br /> MOLAP 儲存模式。<br /><br /> 啟用主動式快取。<br /><br /> 卸除過期的快取，延遲期間為 4 小時。<br /><br /> 當資料變更，無回應間隔為 10 秒，且無回應覆寫間隔為 10 分鐘時，請更新快取。<br /><br /> 使物件立刻回到線上。|  
|**自動 MOLAP**|選取以使用下列儲存與主動式快取設定：<br /><br /> MOLAP 儲存模式。<br /><br /> 啟用主動式快取。<br /><br /> 資料變更時更新快取，無回應間隔為 0 秒，沒有無回應覆寫間隔。|  
|**已排程的 MOLAP**|選取以使用下列儲存與主動式快取設定：<br /><br /> MOLAP 儲存模式<br /><br /> 啟用主動式快取<br /><br /> 定期更新快取，重建間隔為 1 天|  
|**MOLAP**|選取以使用下列儲存與主動式快取設定：<br /><br /> MOLAP 儲存模式。|  
  
 **自訂設定**  
 選取以明確地設定儲存模式、主動式快取和通知選項。  
  
 **選項。**  
 按一下以顯示 [儲存選項] 對話方塊，以明確地設定儲存模式、主動式快取和通知選項。 如需 [儲存選項] 對話方塊的詳細資訊，請參閱[儲存選項對話方塊 &#40;Analysis Services - 多維度資料&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [主動式快取&#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [資料分割屬性 對話方塊中&#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [選取&#40;資料分割屬性對話方塊&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [一般&#40;資料分割屬性對話方塊&#41; &#40;SSMS&#41;](general-partition-properties-dialog-box-ssms.md)   
 [Cube、 分割區和維度處理的錯誤組態&#40;SSAS-多維度&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
