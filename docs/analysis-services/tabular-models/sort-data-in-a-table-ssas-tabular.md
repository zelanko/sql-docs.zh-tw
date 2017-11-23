---
title: "排序資料表 (SSAS 表格式) 中的資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5fa6ad56-bf68-4aac-a226-52556173b7e2
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 331894e59c7cbf8d5fe2b4e6112732f45a986f6e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sort-data-in-a-table-ssas-tabular"></a>排序資料表中的資料 (SSAS 表格式)
  您可以依一個或多個資料行中的文字 (A 到 Z 或 Z 到 A) 和數字 (最小到最大或最大到最小) 來排序資料。  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>根據文字資料行排序資料表中的資料  
  
1.  在模型設計師中，選取英數資料的資料行、資料行中的資料格範圍，或確認作用中資料格位於包含英數資料的資料表資料行中，然後按一下您要做為篩選依據的資料行標頭中的箭號。  
  
2.  在 [自動篩選] 功能表中，執行下列其中一項：  
  
    -   若要以遞增的英數順序排序，按一下 **[從 A 到 Z 排序]**。  
  
    -   若要以遞減的英數順序排序，按一下 **[從 Z 到 A 排序]**。  
  
    > [!NOTE]  
    >  在某些情況下，從其他應用程式匯入的資料在資料前面可能會插入開頭空白。 您必須移除開頭空白，才能正確排序資料。  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>根據數字資料行排序資料表中的資料  
  
1.  在模型設計師中，選取英數資料的資料行、資料行中的資料格範圍，或確認作用中資料格位於包含英數資料的資料表資料行中，然後按一下您要做為篩選依據的資料行標頭中的箭號。  
  
2.  在 [自動篩選] 功能表中，執行下列其中一項：  
  
    -   若要從最小的數字排序到最大的數字，按一下 **[從最小到最大排序]**。  
  
    -   若要從最大的數字排序到最小的數字，按一下 **[從最大到最小排序]**。  
  
    > [!NOTE]  
    >  如果結果不如預期，資料行可能會包含儲存為文字而非數字的數字。 例如，從某些會計系統匯入的負數，或者以開頭 ' (單引號) 輸入的數字儲存為文字。  
  
## <a name="see-also"></a>請參閱＜  
 [篩選與排序資料 &#40;SSAS 表格式&#41;](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [檢視方塊 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [角色 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
