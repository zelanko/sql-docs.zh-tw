---
title: 工作 9：加入聯集全部轉換來結合正確與更正的記錄 |Microsoft Docs
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
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489639"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>工作 9：新增聯集全部轉換來結合正確和更正的記錄
  在這項工作，您會將聯集全部轉換加入至資料流程。 「聯集全部」轉換會將多項輸入結合至單一輸出。 在您的案例中，它會將正確和已更正的記錄結合到一個資料流中。  
  
1.  拖放**聯集全部**從轉換**常見**一節**SSIS 工具箱**至**資料流程**索引標籤，並將它放在**挑選正確和更正的記錄**。  
  
2.  以滑鼠右鍵按一下**聯集全部**轉換**資料流程**索引標籤，然後按一下**重新命名**。 型別**結合正確和已更正的記錄**，然後按**ENTER**。  
  
     ![結合正確與更正的記錄](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "結合正確與更正的記錄")  
  
3.  連接**挑選正確和已更正的記錄**要**結合正確和已更正的記錄**中**資料流程**使用藍色連接器 索引標籤。 您應該會看到**輸入輸出選擇** 對話方塊。  
  
4.  中**輸入輸出**對話方塊中，選取**更正**如**輸出**，按一下 **確定**。  
  
     ![輸入輸出選擇 對話方塊](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "輸入輸出選擇 對話方塊")  
  
5.  將標題為連接器移**更正**向左拖放至左的連接器結尾的點。  
  
     ![正確 連接至 結合正確與更正](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "正確 連接至 結合正確與更正")  
  
6.  如果您選取**挑選正確和已更正的記錄**轉換，您應該會看到另一個藍色的連接器。 將以該藍色連接器拖曳**結合正確和已更正的記錄**。  
  
     ![更正連接至 結合正確與更正](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "更正連接至結合正確與更正")  
  
7.  這**connector**標題應該為**更正**。 因為您有只有兩個條件**更正**並**更正**，和已使用一個條件，則**輸入輸出選擇**對話方塊不會顯示這段。 如果連接器重疊，請將連接器往左或往右拖曳，將其中一個往左移，將另一個往右移。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 10:加入模糊群組轉換來識別重複項目](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
