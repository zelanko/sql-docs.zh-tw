---
title: 處理對話方塊 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.processdialog.f1
ms.assetid: c065248c-9001-4f0c-928f-9c59eccb618b
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5788bce44bc3ad63956183ac4e8950a0ace11d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134818"
---
# <a name="process-dialog-box-analysis-services---multidimensional-data"></a>處理對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [處理] 對話方塊，即可處理 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件。 您可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中依下列方式顯示 [處理] 對話方塊：  
  
-   以滑鼠右鍵按一下方案總管中的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案、Cube、維度或採礦結構，然後選取 [處理]。  
  
-   從 [Cube 設計師] 的每個頁面、[維度設計師] 的每個頁面或 [資料採礦模型設計師] 的 [採礦結構] 和 [採礦模型] 頁面上的工具列，選取 [處理]。  
  
-   以滑鼠右鍵按一下 [資料採礦模型設計師] 之 [採礦模型] 頁面中的採礦模型，然後選取 [處理採礦結構和所有模型] 或 [處理模型]。  
  
 您可以在 [SQL Server Management Studio] 中依下列方式顯示 [處理] 對話方塊：  
  
-   以滑鼠右鍵按一下物件總管中的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫、Cube、量值群組、資料分割、維度、採礦結構或採礦模型，然後選取 [處理]。  
  
## <a name="options"></a>選項。  
 **物件清單**  
 選取要處理的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件，以及要套用的處理選項和設定。 方格包含下列資料行：  
  
 **Object Name**  
 顯示要處理的物件名稱。 名稱左邊的圖示會指出物件類型。  
  
 **型別**  
 顯示要處理的物件類型。  
  
 **處理選項**  
 選取在選取之物件上要執行的處理類型。 如需可用處理選項的詳細資訊，請參閱[多維度模型物件處理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 **設定**  
 在 Cube、量值群組或資料分割的 [處理選項] 中選擇 [處理累加] 時，會顯示 [設定] 超連結。 按一下 [設定] 即可啟動 [累加式更新] 對話方塊。 如需 [累加式更新] 對話方塊的詳細資訊，請參閱[累加式更新對話方塊 &#40;Analysis Services - 多維度資料&#41;](incremental-update-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **移除**  
 按一下即可從 [物件清單] 中移除選取的項目。  
  
 **影響分析**  
 按一下即可開啟 [影響分析] 對話方塊，並顯示受到處理工作影響的物件。 如需 [影響分析] 對話方塊的詳細資訊，請參閱[影響分析對話方塊 &#40;Analysis Services - 多維度資料&#41;](impact-analysis-dialog-box-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  當選取 [變更設定] 對話方塊中的 [處理受影響的物件] 選項時，就會停用此選項。  
  
 **變更設定**  
 按一下即可開啟 [變更設定] 對話方塊，以變更會影響所選取物件之處理方式的設定，包括批次處理設定、回寫設定以及維度索引鍵錯誤設定。 如需 [變更設定] 對話方塊的詳細資訊，請參閱[變更設定對話方塊 &#40;Analysis Services - 多維度資料&#41;](change-settings-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **執行**  
 按一下即可處理物件。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [處理進度對話方塊&#40;Analysis Services-多維度資料&#41;](process-progress-dialog-box-analysis-services-multidimensional-data.md)  
  
  