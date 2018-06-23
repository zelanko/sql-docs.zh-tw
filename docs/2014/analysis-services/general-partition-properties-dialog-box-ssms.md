---
title: 一般 （資料分割屬性對話方塊） (SSMS) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.general.f1
ms.assetid: efb505be-354f-4d23-8f2d-3e76fa50d27b
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0008344f56afefca65c9c94b1b4446b5d84455dd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031745"
---
# <a name="general-partition-properties-dialog-box-ssms"></a>一般 (資料分割屬性對話方塊) (SSMS)
  在 SQL Server Management Studio 中，使用 [資料分割屬性] 對話方塊的 [一般] 頁面，即可針對 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中的 Cube，設定量值群組中之資料分割的一般屬性。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**彙總設計識別碼**|顯示資料分割所使用之彙總設計的識別碼。|  
|**彙總前置詞**|顯示資料分割所包含之彙總執行個體的預設前置詞。|  
|**建立時間戳記**|顯示建立資料分割的日期和時間。|  
|**目前儲存模式**|顯示資料分割的目前儲存模式。<br /><br /> 注意：此模式可能會依據資料分割的主動式快取設定而改變。 如需主動式快取的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**說明**|鍵入即可變更資料分割的描述。|  
|**估計的資料列**|鍵入資料分割代表之基礎資料來源中所估計的資料列數目。 此值會於處理期間使用，以估計處理資料分割所需的時間和儲存體。|  
|**估計的大小**|顯示資料分割的估計大小。|  
|**ID**|顯示資料分割的識別碼。|  
|**上次處理**|顯示上次處理資料分割的日期和時間。|  
|**上次結構描述更新**|顯示上次更新資料分割之中繼資料的日期和時間。|  
|**名稱**|顯示分割區的名稱。|  
|**處理模式**|選取資料分割的處理模式。 如需有關處理模式的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]物件，請參閱[多維度模型物件處理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。|  
|**遠端資料來源識別碼**|顯示從其中擷取資料分割之來源資料的遠端資料來源識別碼。<br /><br /> 注意：此屬性包含僅適用於遠端資料分割的值。|  
|**配量**|顯示識別資料分割所代表之資料配量的運算式。|  
|**Source**|顯示提供資料分割之來源資料的資料表或查詢。|  
|**State**|顯示資料分割目前的處理狀態。|  
|**儲存位置**|顯示儲存資料分割之資料的資料夾。<br /><br /> 注意：唯有指定了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的預設儲存位置之外的儲存位置之後，此屬性才會包含值。|  
|**型別**|顯示資料分割的類型。|  
  
## <a name="see-also"></a>另請參閱  
 [資料分割&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [遠端資料分割](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [資料分割屬性對話方塊&#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [選取項目&#40;分割內容 對話方塊中&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 [主動式快取&#40;分割內容 對話方塊中&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)   
 [Cube、 分割區和維度處理的錯誤組態&#40;SSAS-多維度&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  