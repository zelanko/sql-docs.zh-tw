---
title: 工作 2： 測試和發行比對原則 |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8f67535e5ad4969983b06fcb710c1dfce1d97cb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134746"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>工作 2：測試和發行比對原則
  在這項工作、 測試和發佈**移除重複的供應商**比對原則。  
  
1.  在**比對結果**頁面上，按一下**啟動**測試整個原則。 在您的案例中，此原則只有一個規則，所以測試規則和原則的結果應該相同。  
  
2.  請在清單方塊中檢閱所有相符記錄及其比對分數。 有一筆記錄**綠色**與其相關聯的圖示是在它之前的樞紐記錄的複本。 以下是幾個範例：  
  
    1.  與記錄**記錄識別碼： 1000005**相符的記錄符合**記錄識別碼： 1000004**與**分數： 100%** 因為兩筆記錄有相同的值**SupplierID （必要條件）**， **Supplier Name**，和**ContactEmailAddress 資料行**。 DQS 會隨機挑選記錄當做叢集的樞紐記錄。  
  
    2.  記錄**1000023**會記錄符合**1000022**比對分數： 93%，因為兩筆記錄有相同的值**SupplierID （必要條件）** 和**Supplier Name**資料行，但是不同的值**ContactEmailAddress**資料行。  
  
    3.  若要查看兩筆記錄的記錄識別碼清單的底部的捲軸： **1000051**和**1000052**。 記錄**1000052**會被視為相符項目，其比對分數**91%** 因為兩筆記錄有相同的值**SupplierID**和**ContactEmailAddress**資料行，但是不同的值**Supplier Name**資料行。  
  
     ![原則定義-原則結果](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "原則定義-原則結果")  
  
3.  以滑鼠右鍵按一下任何相符的記錄 （有綠色圖示），然後按一下**檢視詳細資料**看到比對之整體符合分數的每個欄位分數的比重如需詳細資訊。  
  
     ![符合分數詳細資料對話方塊](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "符合分數詳細資料對話方塊")  
  
4.  按一下**關閉**關閉**符合分數詳細資料** 對話方塊。  
  
5.  按一下**比對結果**底部的頁面 索引標籤。 此索引標籤會提供詳細資料，例如相符記錄的數目、不相符記錄的數目、具有相符記錄的叢集數目、平均叢集大小、最小叢集大小和最大叢集大小。 請參閱[Create a Matching Policy](http://msdn.microsoft.com/library/hh270290.aspx)如需詳細資訊。 您無法從這個活動匯出結果。 您只會定義比對原則，方式是使用取樣資料來針對取樣資料測試規則和原則。  
  
     ![比對結果索引標籤](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "比對結果索引標籤")  
  
6.  按一下**完成**完成建立比對原則。  
  
    > [!NOTE]  
    >  您已經在這裡定義比對原則，因此無法將結果匯出到輸出檔。 您基本上已經使用範例輸入檔、建立規則，並針對取樣資料測試規則和原則 (目標是要定義原則)。  
  
7.  在 SQL Server Data Quality Services] 對話方塊中，按一下 [**發行**按一下**確定**訊息方塊上。 現在，您定義的比對原則會發佈至**供應商**知識庫。 您可以使用此知識庫，針對輸入檔執行比對程序，以識別並移除重複項。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 3： 建立和執行資料品質專案以進行比對](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  