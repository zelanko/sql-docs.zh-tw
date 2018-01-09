---
title: "刪除資料行 (SSAS 表格式) |Microsoft 文件"
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
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d413e4bdfffcdf0210f960c34bfafa8dc82946ca
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="delete-a-column-ssas-tabular"></a>刪除資料行 (SSAS 表格式)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]本主題描述如何從表格式模型資料表刪除資料行。  
  
## <a name="delete-a-model-table-column"></a>刪除模型資料表資料行  
  
> [!NOTE]  
>  從模型資料表中刪除資料行時，並不會從資料分割查詢定義中刪除該資料行。 如果您要刪除的資料行屬於資料分割的一部分，就必須從資料分割查詢定義中手動刪除該資料行。 如果沒有從資料分割查詢定義中刪除資料行，將會導致系統在處理作業期間查詢該資料行並且傳回資料，但是不會擴展至模型資料表。 如需詳細資訊，請參閱 [資料分割 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
#### <a name="to-delete-a-model-table-column"></a>若要刪除模型資料表資料行  
  
-   在模型設計師中，於包含您想要刪除之資料行的資料表內，以滑鼠右鍵按一下資料行，然後按一下 [刪除]。  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>若要使用資料表屬性對話方塊來刪除模型資料表資料行  
  
1.  在模型設計師中，按一下包含您想要刪除之資料行的資料表、按一下 [資料表] 功能表，然後按一下 [資料表屬性]。  
  
2.  在 [資料行名稱來自] 中，選取 [模型] \(使用模型資料表資料行名稱，如果與來源不同的話)。  
  
3.  在 [編輯資料表屬性] 對話方塊的 [資料表預覽] 視窗中，取消核取您想要刪除的資料行，然後按一下 [確定]。  
  
## <a name="see-also"></a>請參閱  
 [將資料行加入至資料表 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [資料分割 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
