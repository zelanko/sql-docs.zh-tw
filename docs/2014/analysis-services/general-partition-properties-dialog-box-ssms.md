---
title: 一般 （資料分割屬性對話方塊） (SSMS) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 05d840d4e43d9856dedeb3fd446c8158f23275b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081067"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>一般 (資料分割屬性對話方塊) (SSMS)
  在 SQL Server Management Studio 中，使用 [資料分割屬性]  對話方塊的 [一般]  頁面，即可針對 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中的 Cube，設定量值群組中之資料分割的一般屬性。  
  
## <a name="options"></a>選項  
  
|詞彙|定義|  
|----------|----------------|  
|**彙總設計識別碼**|顯示資料分割所使用之彙總設計的識別碼。|  
|**彙總前置詞**|顯示資料分割所包含之彙總執行個體的預設前置詞。|  
|**建立時間戳記**|顯示建立資料分割的日期和時間。|  
|**目前儲存模式**|顯示資料分割的目前儲存模式。<br /><br /> 注意:此模式可能有所不同的磁碟分割的主動式快取設定。 如需主動式快取的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**說明**|鍵入即可變更資料分割的描述。|  
|**估計的資料列**|鍵入資料分割代表之基礎資料來源中所估計的資料列數目。 此值會於處理期間使用，以估計處理資料分割所需的時間和儲存體。|  
|**估計的大小**|顯示資料分割的估計大小。|  
|**ID**|顯示資料分割的識別碼。|  
|**上次處理**|顯示上次處理資料分割的日期和時間。|  
|**上次結構描述更新**|顯示上次更新資料分割之中繼資料的日期和時間。|  
|**名稱**|顯示分割區的名稱。|  
|**處理模式**|選取資料分割的處理模式。 如需處理模式的詳細資訊[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]物件，請參閱[多維度模型物件處理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。|  
|**遠端資料來源識別碼**|顯示從其中擷取資料分割之來源資料的遠端資料來源識別碼。<br /><br /> 注意:此屬性包含遠端資料分割僅的值。|  
|**Slice**|顯示識別資料分割所代表之資料配量的運算式。|  
|**Source**|顯示提供資料分割之來源資料的資料表或查詢。|  
|**狀態**|顯示資料分割目前的處理狀態。|  
|**儲存體位置**|顯示儲存資料分割之資料的資料夾。<br /><br /> 注意:此屬性包含值，只有當儲存位置以外的預設儲存體位置[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]指定執行個體。|  
|**型別**|顯示資料分割的類型。|  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [遠端資料分割](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [資料分割屬性 對話方塊中&#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [選取&#40;資料分割屬性對話方塊&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [主動式快取&#40;資料分割屬性對話方塊&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [Cube、 分割區和維度處理的錯誤組態&#40;SSAS-多維度&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
