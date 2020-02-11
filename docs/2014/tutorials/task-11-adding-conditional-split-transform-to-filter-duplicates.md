---
title: 工作11：新增條件式分割轉換來篩選重複專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65476745"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>工作 11：加入條件式分割轉換來篩選重複項
  在這項工作中，您會將條件式分割轉換加入至資料流程。 此轉換可幫助您篩選傳入記錄集中的重複項。 模糊群組轉換會將它找到的相符記錄群組在一起，並挑選其中一筆記錄當做樞紐記錄。 群組中的所有記錄都有相同的 _key_out 值。 群組中的樞紐記錄的 _key_in 值與 _key_out 值相同。 群組中其他記錄的 _key_in 和 _key_out 值不同。 因此，當您使用 _key_in==_key_out 條件篩選時，您只會得到群組中的樞紐資料列。  
  
1.  從 [ **SSIS 工具箱**] 中的 [**通用**] 區段將 [**條件式分割**轉換] 拖放至 [**資料流程**] 索引標籤。  
  
2.  以滑鼠右鍵**按一下 [資料流程**] 索引標籤中的 [**條件式分割轉換**]，然後按一下 [**重新命名**] 輸入**篩選重複專案**，然後按**enter**。  
  
3.  連接**具有相符識別碼的群組供應商**來**篩選重複專案**。  
  
4.  按兩下 [**篩選重複專案**]，啟動 [**條件式分割轉換編輯器**] 對話方塊。  
  
5.  展開左上方窗格中的 [資料**行**]。  
  
6.  將 **_key_in**拖放至 [**條件**] 資料行。  
  
7.  在 [ **_key_in** ] 旁輸入 = = （等於），並將 **_key_out**拖放。  
  
8.  在 [**輸出名稱**] 資料行中按一下 [**案例 1** ]，輸入**唯一記錄**，然後按**enter**。  
  
     ![條件式分割轉換編輯器](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "條件式分割轉換編輯器")  
  
9. 按一下 **[確定]** 以關閉 [**條件式分割轉換編輯器**] 對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 12：加入衍生的資料行轉換，以加入 MDS 需要的資料行](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
