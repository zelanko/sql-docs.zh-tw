---
title: 工作 1： 定義比對原則 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b0ccf6217899b5368cf27f93951e0a7ddc0cf48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035353"
---
# <a name="task-1-defining-a-matching-policy"></a>工作 1：定義比對原則
  在這項工作中，您會建立包含一個規則的比對原則。 此規則將會有一個必要條件： **Supplier ID**，也就是說，Supplier Id 必須符合才能使用規則中的其他定義域。 此規則會使用其他兩個定義域： **Supplier Name**與**相似度**值設定為**70%** 和**Contact Email**與**相似度**值設定為**30%**。  
  
1.  中的主頁面**DQS 用戶端**，按一下 **向右箭號**旁**供應商**知識，然後選取**比對原則**。  
  
     ![比對原則 功能表上的主要頁面](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "比對原則 功能表上的主要頁面")  
  
2.  在**對應**頁面上，選取**Excel 檔案**如**資料來源**。  
  
3.  按一下**瀏覽**，請確定該篩選條件設定為**Excel 活頁簿**，然後選取**Cleansed Supplier List.xls**檔案執行清理活動之後匯出。  
  
    > [!NOTE]  
    >  在此活動結束時，您將無法匯出結果，因為此活動主要著重於定義比對原則。 您將會針對比對活動建立資料品質專案，並在下一課使用這個比對原則來執行專案，以便從供應商清單中移除重複項。  
  
4.  地圖**SupplierID**資料行**Supplier ID**網域**Supplier Name**資料行**Supplier Name**網域**ContactEmailAddress**欄**Contact Email**網域。 您只需要將來源資料行對應至定義比對原則所要使用的定義域。 在此情況下，您會提供 Supplier ID、Supplier Name 和 Contact Email 等定義域給比對原則活動使用。  
  
     ![[對應] 頁面的比對原則定義程序](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "對應頁面的比對原則定義程序")  
  
5.  按一下**下一步**移至**比對原則**其中您要定義具有一個規則的比對原則中的頁面。  
  
6.  按一下**建立比對規則**原則中建立規則 工具列上的按鈕。  
  
     ![建立比對的規則 工具列按鈕](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "建立比對的規則 工具列按鈕")  
  
7.  在**規則詳細資料**窗格的右邊輸入**移除重複的供應商**如**規則名稱**。  
  
8.  按一下**加入新的定義域項目**在右窗格的工具列中。  
  
     ![規則詳細資料-加入新的定義域項目按鈕](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "規則詳細資料-加入新的定義域項目 按鈕")  
  
9. 選取**Supplier ID**如**網域**選取**必要條件**核取方塊。 請注意，**相似度**會自動設為**精確**。 藉由設定**Supplier ID**為**必要條件**，您可以指定兩筆記錄中此欄位的值必須傳回 100%相符，否則這些記錄不被視為比對和中的其他子句會略過規則。  
  
     ![移除重複的供應商規則定義](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "移除重複的供應商規則定義")  
  
10. 按一下**加入新的定義域項目**再次從工具列。  
  
11. 選取**Supplier Name**網域中，選取**類似**的**相似度**，並輸入**70**的**加權**.  您在此指定供應商名稱不需要完全相同但可以類似，以便讓記錄視為相符。 加權表示此欄位的分數佔整體比對分數的比重。  
  
12. 重複上述兩個步驟來加入**Contact Email**網域**30**如**加權**。  
  
13. 請注意，**最小符合分數**設**80%**，這是您在中看到的值**一般** 索引標籤**組態**頁面**DQS 管理**。 您在這裡只能增加這個分數，使其高於此臨界值。  
  
14. 請注意，**重疊的叢集**選取選項。 有了這個選項，記錄就會出現在多個叢集中。 如果您將設定變更為 [非重疊的叢集]，具有共同記錄的叢集就會結合到單一叢集中。  
  
15. **啟動**此頁面上的按鈕可讓您分別測試原則中的每個規則而下一頁的 [開始] 按鈕可讓您測試整個原則 （中的所有規則的原則）。  
  
16. 按一下**下一步**切換至**比對結果**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 2： 測試和發行比對原則](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  