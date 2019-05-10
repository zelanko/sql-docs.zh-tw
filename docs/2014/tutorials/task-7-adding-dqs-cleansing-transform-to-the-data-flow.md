---
title: 工作 7：將 DQS 清理轉換加入資料流程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 209659609c2cf19196cc35050fb32e39e079d1c7
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488947"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>工作 7：將 DQS 清理轉換新增至資料流程
  在這項工作中，您將使用 DQS 將 DQS 清理轉換加入至資料流程來清理輸入供應商資料。 請參閱 **[DQS 清理轉換](https://msdn.microsoft.com/library/ee677619.aspx)** 如需有關轉換的詳細資訊。  
  
1.  以滑鼠右鍵按一下**DQS 清理**中**資料流程**索引標籤，然後按一下**重新命名**。 型別**清理供應商資料**，然後按**ENTER**。  
  
2.  選取 **從 Excel 檔案讀取供應商資料**; 以藍色連接器拖曳到**清理供應商資料**。 現在已連接這些元件。  
  
     ![讀取供應商資料-> 清理供應商資料](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "讀取供應商資料-> 清理供應商資料")  
  
3.  按兩下**清理供應商資料**。  
  
4.  在  **DQS 清理轉換編輯器**，按一下**新增**旁**資料品質連接管理員下拉式清單**。  
  
5.  在 [ **DQS 清理連接管理員**] 對話方塊中，輸入 **(local)** 或**期間**（.） 來連接到本機伺服器。 本課程假設您已經在本機伺服器上安裝 DQS。  
  
6.  按一下 **測試連接**來測試連接到 DQS 伺服器。  
  
7.  按一下 **[確定]** ，關閉對話方塊。  
  
8.  選取 **供應商**for**資料品質知識庫**。  
  
     ![DQS 清理轉換編輯器-供應商知識庫](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "DQS 清理轉換編輯器-供應商知識庫")  
  
9. 若要切換**對應**頂端索引標籤。  
  
10. 從**可用的輸入資料行**，選取**Supplier Name**， **ContactEmailAddress**，**地址行**， **縣（市)**，**狀態**，**國家/地區**，和**郵遞區號**選取核取方塊。  
  
     ![DQS 清理轉換編輯器-對應](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "DQS 清理轉換編輯器-對應")  
  
11. 在底部窗格中，請使用下拉式清單中的，這些資料行對應**網域**資料行：  
  
    |「資料行」|網域|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |[地址行]|[地址行]|  
    |[縣/市]|[縣/市]|  
    |State|State|  
    |Country|Country|  
    |Zip Code|[郵遞區號]|  
  
12. 按一下 [ **[確定]** 以關閉**DQS 清理轉換編輯器**] 對話方塊。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 8:加入條件式分割轉換來分割清理輸出](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
