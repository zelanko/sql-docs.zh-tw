---
title: 工作 8： 加入條件式分割轉換來分割清理輸出 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6dc3b98e03a7940841bc97012c1a4e4220bb970d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132116"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>工作 8：加入條件式分割轉換來分割清理輸出
  在這項轉換中，您會將條件式分割轉換加入至資料流程。 「條件式分割」轉換可根據資料的內容，將資料列路由傳送至不同的輸出。 此教學課程中，您使用**記錄狀態**從 DQS 清理轉換的輸出資料行。 在本教學課程中，您只會將正確或已更正的記錄上傳到 MDS 伺服器。 因此您會先檢查**記錄狀態**是**更正**或**更正**，並結合記錄之前記錄上傳到 MDS。  
  
1.  拖放**條件式分割轉換**從**常見**一節中**SSIS 工具箱**至**資料流程** 索引標籤下**清理供應商資料**。  
  
2.  以滑鼠右鍵按一下**條件式分割**，然後按一下**重新命名**。 型別**挑選正確和已更正的記錄**按**ENTER**。  
  
3.  連接**清理供應商資料**和**挑選正確和已更正的記錄**使用藍色連接器。  
  
     ![清理供應商資料-> 挑選正確與更正](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "清理供應商資料-> 挑選正確與更正")  
  
4.  按兩下**挑選正確和已更正的記錄**中**資料流程** 索引標籤。  
  
5.  變更**預設輸出名稱**畫面底部**更正**。  
  
6.  展開**資料行**中**左上窗格**。  
  
     ![條件式分割轉換編輯器](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "條件式分割轉換編輯器")  
  
7.  拖放**記錄狀態**至**條件**資料行。  
  
8.  型別 **= ="Corrected"** 旁 **[記錄狀態]** 如**條件**資料行。  
  
9. 按一下**案例 1**中**輸出名稱資料行**，並將名稱變更為**更正**。  
  
10. 按一下**確定**關閉**條件式分割轉換編輯器** 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 9： 加入聯集全部轉換來結合正確和更正的記錄](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  