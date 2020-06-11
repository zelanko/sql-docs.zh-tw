---
title: 一般（資料分割屬性對話方塊）（SSMS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 434eb332c7fc8829d515ac33102604dd9ca46d5e
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544396"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>一般 (資料分割屬性對話方塊) (SSMS)
  在 SQL Server Management Studio 中，使用 [資料分割屬性]**** 對話方塊的 [一般]**** 頁面，即可針對 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中的 Cube，設定量值群組中之資料分割的一般屬性。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**彙總設計識別碼**|顯示資料分割所使用之彙總設計的識別碼。|  
|**彙總前置詞**|顯示資料分割所包含之彙總執行個體的預設前置詞。|  
|**建立時間戳記**|顯示建立資料分割的日期和時間。|  
|**目前儲存模式**|顯示資料分割的目前儲存模式。<br /><br /> 注意：此模式可能會依據資料分割的主動式快取設定而改變。 如需主動式快取的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**描述**|鍵入即可變更資料分割的描述。|  
|**估計的資料列**|鍵入資料分割代表之基礎資料來源中所估計的資料列數目。 此值會於處理期間使用，以估計處理資料分割所需的時間和儲存體。|  
|**估計的大小**|顯示資料分割的估計大小。|  
|**識別碼**|顯示資料分割的識別碼。|  
|**上次處理**|顯示上次處理資料分割的日期和時間。|  
|**上次結構描述更新**|顯示上次更新資料分割之中繼資料的日期和時間。|  
|**名稱**|顯示分割區的名稱。|  
|**處理模式**|選取資料分割的處理模式。 如需物件之處理模式的詳細資訊 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，請參閱多[維度模型物件處理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。|  
|**遠端資料來源識別碼**|顯示從其中擷取資料分割之來源資料的遠端資料來源識別碼。<br /><br /> 注意：此屬性包含僅適用於遠端資料分割的值。|  
|**圓形圖**|顯示識別資料分割所代表之資料配量的運算式。|  
|**來源**|顯示提供資料分割之來源資料的資料表或查詢。|  
|**State**|顯示資料分割目前的處理狀態。|  
|**儲存位置**|顯示儲存資料分割之資料的資料夾。<br /><br /> 注意：唯有指定了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的預設儲存位置之外的儲存位置之後，此屬性才會包含值。|  
|**型別**|顯示資料分割的類型。|  
  
## <a name="see-also"></a>另請參閱  
 [分割區 &#40;Analysis Services 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [遠端資料分割](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [&#40;SSMS&#41;的 [資料分割屬性] 對話方塊](partition-properties-dialog-box-ssms.md)   
 [[選取 &#40;資料分割屬性] 對話方塊&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [主動式快取 &#40;資料分割屬性] 對話方塊&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [&#40;SSAS 的 Cube、資料分割和維度處理的錯誤設定&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
