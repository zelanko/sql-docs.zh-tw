---
title: 工作 1:定義比對原則 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 6f89a720-fce5-4f60-bef3-a159bbc9f25c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 55739fd6cf7b6c395c2e7a66c3d80fad22607a83
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394191"
---
# <a name="task-1-defining-a-matching-policy"></a>工作 1:定義比對原則
  在這項工作中，您會建立包含一個規則的比對原則。 此規則將會有一個必要條件：**Supplier ID**，也就是說，Supplier Id 必須符合才能使用規則中的其他定義域。 此規則會使用其他兩個定義域：**Supplier Name**與**相似度**值設定為**70%** 並**Contact Email**使用**相似度**值設定為**30%**。  
  
1.  中的主頁面**DQS 用戶端**，按一下**向右箭號**旁**供應商**知識，然後選取**比對原則**。  
  
     ![比對原則 功能表，在主要頁面](../../2014/tutorials/media/et-definingamatchingpolicy-01.jpg "比對原則 功能表，在主要頁面")  
  
2.  在 **地圖**頁面上，選取**Excel 檔案**如**資料來源**。  
  
3.  按一下 **瀏覽**，請確定該篩選條件設定為**Excel 活頁簿**，然後選取**Cleansed Supplier List.xls**檔案執行清理活動之後匯出。  
  
    > [!NOTE]  
    >  在此活動結束時，您將無法匯出結果，因為此活動主要著重於定義比對原則。 您將會針對比對活動建立資料品質專案，並在下一課使用這個比對原則來執行專案，以便從供應商清單中移除重複項。  
  
4.  地圖**SupplierID**資料行**Supplier ID**網域**Supplier Name**資料行**Supplier Name**網域， **ContactEmailAddress**資料行**Contact Email**網域。 您只需要將來源資料行對應至定義比對原則所要使用的定義域。 在此情況下，您會提供 Supplier ID、Supplier Name 和 Contact Email 等定義域給比對原則活動使用。  
  
     ![[對應] 頁面的比對原則定義程序](../../2014/tutorials/media/et-definingamatchingpolicy-02.jpg "對應的比對原則定義程序的頁面")  
  
5.  按一下 **下一步**移至**比對原則**其中您要定義具有一個規則的比對原則中的頁面。  
  
6.  按一下 [**建立比對規則**原則中建立規則] 工具列上的按鈕。  
  
     ![建立比對規則 工具列按鈕](../../2014/tutorials/media/et-definingamatchingpolicy-03.jpg "建立相符的 [規則] 工具列按鈕")  
  
7.  在**規則詳細資料**右邊的窗格輸入**移除重複的供應商**for**規則名稱**。  
  
8.  按一下 **加入新的定義域項目**右窗格的工具列中。  
  
     ![規則詳細資料-加入新的網域項目 按鈕](../../2014/tutorials/media/et-definingamatchingpolicy-04.jpg "規則詳細資料-加入新的網域項目 按鈕")  
  
9. 選取  **Supplier ID** for**網域**，然後選取**必要條件**核取方塊。 請注意，**相似度**會自動設為**精確**。 藉由設定**Supplier ID**作為**必要條件**，您可以指定兩筆記錄中此欄位的值必須傳回 100%相符，否則這些記錄不被視為比對和中的其他子句會略過規則。  
  
     ![移除重複的供應商規則定義](../../2014/tutorials/media/et-definingamatchingpolicy-05.jpg "移除重複的供應商規則定義")  
  
10. 按一下 **加入新的定義域項目**再次從工具列。  
  
11. 選取**Supplier Name**網域，選取**類似**如**相似度**，並輸入**70**的**權數**.  您在此指定供應商名稱不需要完全相同但可以類似，以便讓記錄視為相符。 加權表示此欄位的分數之整體符合分數的比重。  
  
12. 重複上述兩個步驟來加入**Contact Email**網域**30** for**權數**。  
  
13. 請注意，**最小符合分數**設為**80%**，這是您在中看到值**一般**索引標籤**組態**頁面**DQS 管理**。 您在這裡只能增加這個分數，使其高於此臨界值。  
  
14. 請注意，**重疊的叢集**選項。 有了這個選項，記錄就會出現在多個叢集中。 如果您將設定變更為 [非重疊的叢集]，具有共同記錄的叢集就會結合到單一叢集中。  
  
15. **啟動**此頁面上的按鈕可讓您分別測試原則中的每個規則而在下一個頁面的 [開始] 按鈕可讓您測試整個原則 （所有規則的原則中）。  
  
16. 按一下 **下一步**轉為**比對結果**頁面。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 2:測試和發行比對原則](../../2014/tutorials/task-2-testing-and-publishing-the-matching-policy.md)  
  
  
