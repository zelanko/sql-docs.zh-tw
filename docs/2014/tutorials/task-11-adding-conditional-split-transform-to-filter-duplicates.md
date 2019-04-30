---
title: 工作 11：加入條件式分割轉換來篩選重複項目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e2b5fc47b6823a91dd4bb7f74d3ea65fca13bce9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222573"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>工作 11：新增條件式分割轉換來篩選重複項
  在這項工作中，您會將條件式分割轉換加入至資料流程。 此轉換可幫助您篩選傳入記錄集中的重複項。 模糊群組轉換會將它找到的相符記錄群組在一起，並挑選其中一筆記錄當做樞紐記錄。 群組中的所有記錄都有相同的 _key_out 值。 群組中的樞紐記錄的 _key_in 值與 _key_out 值相同。 群組中其他記錄的 _key_in 和 _key_out 值不同。 因此，當您使用 _key_in==_key_out 條件篩選時，您只會得到群組中的樞紐資料列。  
  
1.  拖放**條件式分割**從轉換**常見**一節中**SSIS 工具箱**至**資料流程** 索引標籤。  
  
2.  以滑鼠右鍵按一下**條件式分割轉換**中**資料流程**索引標籤，然後按一下**重新命名**。 型別**篩選重複項**然後按**ENTER**。  
  
3.  連接**分組具有相符識別碼的供應商**要**篩選重複項目**。  
  
4.  按兩下**篩選重複項**來啟動**條件式分割轉換編輯器** 對話方塊。  
  
5.  依序展開**資料行**左上方窗格中。  
  
6.  拖放 **_key_in**要**條件**資料行。  
  
7.  類型 = = （等於） 旁 **_key_in**和 拖放 **_key_out**。  
  
8.  按一下 **案例 1**中**輸出名稱**資料行中輸入**唯一記錄**，然後按**ENTER**。  
  
     ![條件式分割轉換編輯器](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "條件式分割轉換編輯器")  
  
9. 按一下 [ **[確定]** 以關閉**Conditional Split Transformation Editor** ] 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 12:加入衍生的資料行轉換，以加入 MDS 所需的資料行](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
