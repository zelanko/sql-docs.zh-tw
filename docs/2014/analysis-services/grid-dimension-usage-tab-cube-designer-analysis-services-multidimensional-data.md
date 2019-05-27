---
title: 方格 （維度使用方式索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ed63b1da-0fce-4f24-a722-5cff378831e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 294b40d07731f588267e94ff748adaf871a8ac3b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080813"
---
# <a name="grid-dimension-usage-tab-cube-designer-analysis-services---multidimensional-data"></a>方格 (維度使用方式索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  在 Cube 設計師中，使用 **[維度使用方式]** 索引標籤上的 **[方格]** 窗格，即可檢視及編輯 Cube 維度與量值群組之間的維度關聯性。 每一項維度關聯性都會以方格中的資料格來代表，其中的量值群組會顯示為資料行，而維度則顯示為資料列。  
  
## <a name="options"></a>選項  
  
|選項|定義|  
|------------|----------------|  
|**量值群組**|選取在 **[方格]** 窗格中顯示為資料行的量值群組。 選取 [(全部顯示)] 就會顯示所有可用的量值群組。<br /><br /> 按一下量值群組的所選取資料行標頭，即可重新命名量值群組。|  
|**Dimensions**|選取在 **[方格]** 窗格中顯示為資料列的 Cube 維度。 選取 [(全部顯示)] 就會顯示所有可用的 Cube 維度。<br /><br /> 按一下維度的所選取資料列標頭，即可重新命名 Cube 維度。|  
|**(Cell)**|選取一個資料格，再按一下省略符號按鈕 ([...])，即可顯示 [定義關聯性] 對話方塊，並定義 Cube 維度與量值群組之間的維度關聯性。 如需 [定義關聯性] 對話方塊的詳細資訊，請參閱[定義關聯性對話方塊 &#40;Analysis Services - 多維度資料&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="context-menu"></a>操作功能表  
 下列選項可以在內容功能表中使用，以滑鼠右鍵按一下 [方格] 窗格即可顯示內容功能表：  
  
|選項|定義|  
|------------|----------------|  
|**加入 Cube 維度**|選取即可顯示 **[加入 Cube 維度]** 對話方塊，並在 Cube 中加入對現有或新的資料庫維度之參考。 如需 [加入 Cube 維度] 對話方塊的詳細資訊，請參閱[加入 Cube 維度加對話方塊 &#40;Analysis Services - 多維度資料&#41;](add-cube-dimension-dialog-box-analysis-services-multidimensional-data.md)。|  
|**新增連結的物件**|選取即可顯示 **[連結物件精靈]** ，並將來自其他 Cube 的量值群組和維度連結到選取的 Cube 中，以及將動作、KPI 和計算等，匯入到選取的 Cube 中。 如需 [連結物件精靈] 的詳細資訊，請參閱[連結物件精靈 F1 說明](linked-object-wizard-f1-help.md)。|  
|**Cut**|注意:已停用此選項。|  
|**[複製]**|注意:已停用此選項。|  
|**貼上**|注意:已停用此選項。|  
|**刪除**|選取即可從 Cube 中刪除選取的 Cube 維度、量值群組或維度關聯性。|  
|**重新命名**|選取即可重新命名選取的 Cube 維度、量值群組或維度關聯性。|  
|**屬性**|選取即可針對選取的 Cube 維度、量值群組或維度關聯性，在 **中顯示** [屬性] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 視窗。|  
  
## <a name="see-also"></a>另請參閱  
 [Cube 物件&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多維度模型中的 Cube](multidimensional-models/cubes-in-multidimensional-models.md)   
 [維度使用方式&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;維度使用方式索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [維度使用方式&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)  
  
  
