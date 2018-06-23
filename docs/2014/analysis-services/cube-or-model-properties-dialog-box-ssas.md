---
title: Cube 或模型屬性對話方塊 (SSAS) |Microsoft 文件
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
- sql12.asvs.sqlserverstudio.cubeproperties.f1
ms.assetid: 97e367f9-f95a-4163-add1-c74fd22db249
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 90efe4a053104491b24e290641205d85628c3689
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135295"
---
# <a name="cube-or-model-properties-dialog-box-ssas"></a>Cube 或模型屬性對話方塊 (SSAS)
  使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [資料庫屬性] 對話方塊，即可設定 Cube 或模型資料庫的屬性。 您可以在**物件總管**中，以滑鼠右鍵按一下 Cube 或模型，然後選取 [屬性]，藉以顯示此對話方塊。  
  
 此對話方塊也包含下列屬性的索引標籤：  
  
-   [報表動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
-   [Cube、 分割區和維度處理的錯誤組態&#40;SSAS-多維度&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
-   [主動式快取&#40;分割內容 對話方塊中&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱**|顯示 Cube 或模型的名稱。|  
|**ID**|顯示 Cube 或模型的識別碼。|  
|**說明**|顯示 Cube 或模型的描述。|  
|**建立時間戳記**|顯示建立 Cube 或模型的日期和時間。|  
|**上次結構描述更新**|顯示上次更新 Cube 或模型之中繼資料的日期和時間。|  
|**指令碼快取處理模式**|選取用於 Cube 或模型之指令碼快取的處理模式。 如需此屬性的值的詳細資訊，請參閱<xref:Microsoft.AnalysisServices.Cube.ScriptCacheProcessingMode%2A>。|  
|**處理模式**|選取用於 Cube 或模型的處理模式。 如需此屬性的值的詳細資訊，請參閱<xref:Microsoft.AnalysisServices.Cube.ProcessingMode%2A>。|  
|**儲存位置**|針對與 Cube 或模型相關聯的量值群組和資料分割，輸入要當做預設儲存位置使用的資料夾，或按一下省略符號按鈕 (**...**) 來顯示 [瀏覽遠端資料夾] 對話方塊以選取資料夾。 如需 [瀏覽遠端資料夾] 對話方塊的詳細資訊，請參閱[瀏覽遠端資料夾對話方塊 &#40;Analysis Services - 多維度資料&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 如需此屬性的值的詳細資訊，請參閱<xref:Microsoft.AnalysisServices.Cube.StorageLocation%2A>。|  
|**State**|顯示 Cube 或模型的處理狀態。 如需此屬性的值的詳細資訊，請參閱<xref:Microsoft.AnalysisServices.ProcessableMajorObject.State%2A>。|  
|**LastProcessed**|顯示上次處理 Cube 或模型的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Cube 物件&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
  