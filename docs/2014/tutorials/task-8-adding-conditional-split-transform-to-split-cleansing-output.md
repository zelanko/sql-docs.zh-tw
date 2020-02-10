---
title: 工作8：新增條件式分割轉換來分割清理輸出 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5a55f0694094e6fe88a42946bcff34f420210f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489676"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>工作 8：加入條件式分割轉換來分割清理輸出
  在這項轉換中，您會將條件式分割轉換加入至資料流程。 「條件式分割」轉換可根據資料的內容，將資料列路由傳送至不同的輸出。 在本教學課程中，您會使用 DQS 清理轉換中的 [**記錄狀態**輸出] 資料行。 在本教學課程中，您只會將正確或已更正的記錄上傳到 MDS 伺服器。 因此，您會檢查**記錄狀態**是否**正確**或已**更正**，並在將記錄上傳至 MDS 之前，先合併記錄。  
  
1.  從 [ **SSIS 工具箱**] 中的 [**一般**] 區段，將 [**條件式分割轉換**] 拖放至 [**清理供應商資料**] 底下的 **[資料流程]**  
  
2.  以滑鼠右鍵按一下 [**條件式分割**]，然後按一下 [**重新命名**]。 輸入**挑選正確和已更正的記錄**，然後按**enter**。  
  
3.  連接**清理供應商資料**，並使用藍色連接器**挑選正確和已更正的記錄**。  
  
     ![清理供應商資料-> 挑選正確 & 更正](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "清理供應商資料 -> 挑選 [正確] 與 [更正]")  
  
4.  按兩下 [**資料流程**] 索引標籤中的 [**挑選正確和已更正的記錄**]。  
  
5.  將畫面底部的**預設輸出名稱**變更為 [**更正**]。  
  
6.  展開**左上方窗格**中的 [資料**行**]。  
  
     ![條件式分割轉換編輯器](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "條件式分割轉換編輯器")  
  
7.  將 [**記錄狀態**] 拖放至 [**條件**] 資料行。  
  
8.  在 [**條件**] 資料行的 **[記錄狀態]** 旁，輸入 **= = "已更正"** 。  
  
9. 在 [**輸出名稱**] 資料行中按一下 [**案例 1** ]，並將名稱變更為 [已**更正**]。  
  
10. 按一下 **[確定]** 以關閉 [**條件式分割轉換編輯器**] 對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 9：加入聯集全部轉換來結合正確和更正的記錄](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
