---
title: 處理表格式模型資料分割（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6c498d2b-22d6-4661-bc21-2ee708336c8b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 96845e99f9d183df8545b1da379ced41496923c1
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938729"
---
# <a name="process-tabular-model-partitions-ssas-tabular"></a>處理表格式模型資料分割 (SSAS 表格式)
  分割區會將一個資料表分割成多個邏輯部分。 接著，每個分割區可以不受其他分割區的影響，單獨處理 (重新整理)。 此主題中的工作描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [處理資料分割]**** 對話方塊，處理模型資料庫中的資料分割。  
  
###  <a name="to-process-a-partition"></a><a name="bkmk_create_new"></a> 處理資料分割  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下含有您要處理之資料分割的資料表，然後按一下 [資料分割]****。  
  
2.  在 [資料分割]**** 對話方塊的 [資料分割]**** 中，按一下 [處理] 按鈕。  
  
3.  在 [**處理資料分割**] 對話方塊的 [**模式**] 清單方塊中，選取下列其中一個處理模式：  
  
    |[模式]|描述|  
    |----------|-----------------|  
    |**處理預設**|偵測資料分割物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的資料分割物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立階層、導出資料行及關聯性。|  
    |**完整處理**|處理資料分割物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。|  
    |**處理資料**|將資料載入資料分割或資料表，而不重新建立階層或關聯性，或重新計算導出資料行和量值。|  
    |**處理清除**|移除資料分割中的所有資料。|  
    |**處理加入**|以新資料累加地更新資料分割。|  
  
4.  在 **[處理]** 核取方塊資料行中，選取您想透過選取的模式處理的資料分割，然後按一下 **[確定]**。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)   
 [建立及管理表格式模型資料分割 &#40;SSAS 表格式&#41;](create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
