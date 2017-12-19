---
title: "刪除資料來源，在 [方案總管] (SSAS 多維度) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 38f16616652f18c8db3d5f7895f3994a10e3179c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>在方案總管中刪除資料來源 (SSAS 多維度)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]您可以刪除資料來源物件，從 Analysis Services 多維度模型專案永久移除。  
  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料來源會提供建構資料來源檢視的基礎，而接著會使用資料來源檢視，於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或資料庫中定義維度、Cube 和採礦結構。 因此，刪除資料來源會使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中的其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件無效。 刪除物件之前，一定要檢閱所提供的相依物件清單。  
  
> [!IMPORTANT]  
>  您無法從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以線上模式開啟的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 資料庫中，刪除其他物件所相依的資料來源。 在刪除資料來源之前，您必須先刪除相依於該資料來源之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的所有物件。 如需線上模式的詳細資訊，請參閱 [在連線模式下連接至 Analysis Services 資料庫](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)。  
  
### <a name="to-delete-a-data-source"></a>若要刪除資料來源  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟您想要從中刪除資料來源的專案，或是連接到您想要從中刪除資料來源的資料庫。  
  
2.  在**方案總管**中，展開 [資料來源] 資料夾。  
  
3.  以滑鼠右鍵按一下該資料來源，然後按一下 [刪除]。 [刪除物件] 對話方塊隨即出現，其中顯示刪除資料來源之後將失效的物件。 按一下 [確定] 刪除資料來源之前，請先仔細檢閱這份清單。  
  
4.  儲存專案。  
  
     從 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案刪除資料來源之後，您必須儲存修改過的專案，否則下次開啟此專案時會收到錯誤，因為當此專案嘗試載入已刪除的資料來源時，該資料來源的基礎 XML 檔案將會遺失。  
  
## <a name="see-also"></a>請參閱  
 [多維度模型中的資料來源](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [支援的資料來源 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
