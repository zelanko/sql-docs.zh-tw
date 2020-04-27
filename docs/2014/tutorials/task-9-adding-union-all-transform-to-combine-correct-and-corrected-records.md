---
title: 工作9：加入聯集全部轉換來結合正確和更正的記錄 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 93b160b6e513ad866126df8b401b82ee1270be84
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489639"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>工作 9：新增聯集全部轉換來結合正確和更正的記錄
  在這項工作，您會將聯集全部轉換加入至資料流程。 「聯集全部」轉換會將多項輸入結合至單一輸出。 在您的案例中，它會將正確和已更正的記錄結合到一個資料流中。  
  
1.  從 [ **SSIS 工具箱**] 的 [**通用**] 區段將 [**全部**轉換] 拖放至 [**資料流程**] 索引標籤，並放在 [**挑選正確和已更正的記錄**] 下。  
  
2.  以滑鼠右鍵按一下 [**資料流程**] 索引標籤中的 [**全部聯集**]，然後按一下 [**重新命名**]。 輸入**結合正確和已更正的記錄**，然後按**enter**鍵。  
  
     ![結合正確與更正的記錄](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "結合正確與更正的記錄")  
  
3.  連接**挑選正確和已更正的記錄**，以使用藍色連接器結合 [**資料流程**] 索引標籤中**正確和已更正的記錄**。 您應該會看到 [**輸入輸出選擇**] 對話方塊。  
  
4.  在 [**輸入輸出**] 對話方塊中，針對 [**輸出**] 選取 [**正確**]，然後按一下 **[確定]**。  
  
     ![[輸入輸出選擇] 對話方塊](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "[輸入輸出選擇] 對話方塊")  
  
5.  將標題為 [**正確**] 的連接器移至左邊，並將其拖放至左邊的連接器結尾。  
  
     ![將 [正確] 連接至 [結合正確與更正]](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "將 [正確] 連接至 [結合正確與更正]")  
  
6.  如果您選取 [**挑選正確和已更正的記錄**] 轉換，您應該會看到另一個藍色的連接器。 拖曳藍色接頭以**結合正確和已更正的記錄**。  
  
     ![將 [更正] 連接至 [結合正確與更正]](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "將 [更正] 連接至 [結合正確與更正]")  
  
7.  此**連接器**的標題應為 [已**更正**]。 因為您只有兩個條件**正確**和已**更正**，而且有一個條件已在使用中，所以這次不會顯示 [**輸入輸出選擇**] 對話方塊。 如果連接器重疊，請將連接器往左或往右拖曳，將其中一個往左移，將另一個往右移。  
  
## <a name="next-step"></a>後續步驟  
 [工作 10：新增模糊群組轉換來識別重複項](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
