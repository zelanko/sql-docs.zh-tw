---
title: "處理工作空間資料庫中的分割區 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3a369705-43fa-4961-9045-32e06fbdde33
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45818de8d3793895720bca625170863b3f17f5b4
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="process-partitions-in-the-workspace-databse"></a>在工作空間資料庫中處理資料分割 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
分割區會將一個資料表分割成多個邏輯部分。 接著，每個分割區可以不受其他分割區的影響，單獨處理 (重新整理)。 本主題中的工作說明如何使用 **中的** [處理資料分割] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]對話方塊，處理模型工作空間資料庫中的資料分割。  
  
 將模型部署至其他 Analysis Services 執行個體之後，資料庫管理員即可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、指令碼或 IS 封裝，建立及管理 (已部署) 模型中的資料分割。 如需詳細資訊，請參閱[建立及管理表格式模型資料分割](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)。  
  
###  <a name="bkmk_create_new"></a> 處理資料分割  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中，依序按一下 [模型] 功能表、[處理]\ (重新整理) 及 [處理資料分割]。  
  
2.  在 **[模式]** 清單方塊，選取下列其中一個處理模式：  
  
    |[模式]|說明|  
    |----------|-----------------|  
    |**處理預設**|偵測資料分割物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的資料分割物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立階層、導出資料行及關聯性。|  
    |**完整處理**|處理資料分割物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。|  
    |**處理資料**|將資料載入資料分割或資料表，而不重新建立階層或關聯性，或重新計算導出資料行和量值。|  
    |**處理清除**|移除資料分割中的所有資料。|  
    |**處理加入**|以新資料累加地更新資料分割。|  
  
3.  在 **[處理]** 核取方塊資料行中，選取您想透過選取的模式處理的資料分割，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [資料分割](../../analysis-services/tabular-models/partitions-ssas-tabular.md)   
 [在工作空間資料庫中建立及管理資料分割](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)  
  
  
