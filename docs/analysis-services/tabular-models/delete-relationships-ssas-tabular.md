---
title: "刪除關聯性 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d40e3f05-54e8-4c4b-807a-0b06f446079b
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b71d8acb6016e425d62c49caa536fafaed8404c9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="delete-relationships-ssas-tabular"></a>刪除關聯性 (SSAS 表格式)
  您可以刪除現有的關聯性，方法是使用 [圖表檢視] 中的模型設計師或使用 [管理關聯性] 對話方塊。 如需如何在表格式模型中使用關聯性的資訊，請參閱 [關聯性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md)。  
  
## <a name="considerations-for-deleting-relationships"></a>刪除關聯性的考量  
 當您決定是否要刪除關聯性時，請牢記以下問題：  
  
-   您無法復原關聯性的刪除。 您可以重新建立關聯性，但是這個動作需要全面重新計算模型中的公式。 因此，在刪除公式中使用的關聯性之前，請務必先檢查。  
  
-   刪除兩個資料表之間的關聯性會造成參考這些資料表的公式發生錯誤。  
  
-   Data Analysis Expression (DAX) RELATED 函數會使用資料表之間的關聯性來查閱另一個資料表中相關的值。 它會在關聯性遭刪除之後傳回不同的結果。 如需詳細資訊，請參閱 RELATED 函數 (DAX)。  
  
-   除了變更樞紐分析表和公式結果以外，建立及刪除關聯性都會使活頁簿重新計算，這可能要花費一些時間。  
  
## <a name="delete-relationships"></a>刪除關聯性  
  
#### <a name="to-delete-a-relationship-by-using-diagram-view"></a>若要使用圖表檢視刪除關聯性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後指向 **[模型檢視]**，再按一下 **[圖表檢視]**。  
  
2.  以滑鼠右鍵按一下兩個資料表之間的關聯性線條，然後按一下 [刪除]。  
  
#### <a name="to-delete-a-relationship-by-using-the-manage-relationships-dialog-box"></a>若要使用 [管理關聯性] 對話方塊刪除關聯性  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中按一下 **[資料表]** 功能表，然後按一下 **[管理關聯性]**。  
  
2.  在 **[管理關聯性]** 對話方塊中，選取清單中的一個或多個關聯性。  
  
     若要選取多個關聯性，請按住 CTRL 同時按一下每個關聯性。  
  
3.  按一下 **[刪除關聯性]**。  
  
4.  按一下 **[管理關聯性]** 對話方塊中的 **[關閉]**。  
  
## <a name="see-also"></a>請參閱＜  
 [關聯性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/relationships-ssas-tabular.md)   
 [建立兩個資料表之間的關聯性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  

