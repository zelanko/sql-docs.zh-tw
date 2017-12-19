---
title: "篩選資料表 (SSAS 表格式) 中的資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
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
f1_keywords:
- sql13.asvs.bidtoolset.notallitemsshowing.f1
- sql13.asvs.bidtoolset.autofiltermenu.f1
- sql13.asvs.bidtoolset.customfilterdb.f1
ms.assetid: 3223059d-f525-4835-bf88-ebc195d9dbdc
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 775a79fb6130bd8504efa7f05778b2690afb5803
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="filter-data-in-a-table-ssas-tabular"></a>篩選資料表中的資料 (SSAS 表格式)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]當您匯入資料，以控制載入資料表中的資料列，您可以套用篩選。 匯入資料之後，您就無法刪除個別的資料列。 但是，您可以套用自訂篩選來控制資料列的顯示方式。 不符合篩選準則的資料列則會隱藏起來。 您可以依一個或多個資料行進行篩選。 篩選會加總，也就是說，每一個額外的篩選都會以目前的篩選為基礎，並進一步減少資料子集。  
  
> [!NOTE]  
>  篩選預覽視窗會限制顯示的不同值數量。 如果超出限制，將顯示一則訊息。  
  
### <a name="to-filter-data-based-on-column-values"></a>若要根據資料行值篩選資料  
  
1.  在模型設計師中，選取資料表，然後按一下您要做為篩選依據之資料行標頭的箭頭。  
  
2.  在 [自動篩選] 功能表中，執行下列其中一項：  
  
    -   在資料行值清單中，選取或清除做為篩選依據的一個或多個值，然後按一下 **[確定]**。  
  
         如果值的數量非常大，在清單中可能不會顯示個別的項目。 但是您會看到「要顯示的項目太多」這個訊息。  
  
    -   按一下 [數字篩選] 或 [文字篩選] \(視資料行的類型而定)，然後按一下其中一個比較運算子命令 (例如 [等於])，或按一下 [自訂篩選]。 在 **[自訂篩選]** 對話方塊中，建立篩選，然後按一下 **[確定]**。  
  
### <a name="to-clear-a-filter-for-a-column"></a>若要清除資料行的篩選  
  
1.  按一下您要清除篩選之資料行標頭中的箭號。  
  
2.  按一下**清除篩選器，從\<資料行名稱 >**。  
  
### <a name="to-clear-all-filters-for-a-table"></a>清除資料表的所有篩選  
  
1.  在模型設計師中，選取您要為其清除篩選的資料表。  
  
2.  按一下 **[資料行]** 功能表，然後按一下 **[清除所有篩選]**。  
  
## <a name="see-also"></a>請參閱  
 [篩選與排序資料 &#40;SSAS 表格式&#41;](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [檢視方塊 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
