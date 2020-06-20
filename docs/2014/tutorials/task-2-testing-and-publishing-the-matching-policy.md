---
title: 工作2：測試和發行比對原則 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 434052f26f8cddcb818decdae42e573a10edc678
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006545"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>工作 2：測試和發行比對原則
  在這項工作中，您會測試併發布**移除重複的供應商**比對原則。  
  
1.  在 [比對**結果**] 頁面中，按一下 [**開始**] 測試整個原則。 在您的案例中，此原則只有一個規則，所以測試規則和原則的結果應該相同。  
  
2.  請在清單方塊中檢閱所有相符記錄及其比對分數。 具有相關聯**綠色**圖示的記錄，是其前面的樞紐分析表記錄的重複項。 以下是幾個範例：  
  
    1.  **記錄識別碼為 1000005**的記錄與記錄**識別碼： 1000004** （具有**分數： 100%** ）的記錄相符，因為這兩筆記錄的 [供貨**商（必要條件）**]、[**供應商名稱**] 和 [ContactEmailAddress] 資料**行**都有相同的值。 DQS 會隨機挑選記錄當做叢集的樞紐記錄。  
  
    2.  記錄**1000023**符合具有符合分數的記錄**1000022** ：93%，因為這兩筆記錄具有相同的 [已建立對應項 **（必要條件）** ] 和 [**供應商名稱**] 資料行的相同值，但 [ **ContactEmailAddress** ] 資料行的值不同。  
  
    3.  請滾動到清單底部，以查看具有記錄識別碼的兩筆記錄： **1000051**和**1000052**。 記錄**1000052**會視為符合分數**91%** 的相符項，因為這兩筆記錄的 [供貨**商**] 和 [ **ContactEmailAddress** ] 資料行具有相同的值，但 [**供應商名稱**] 資料行的值不同。  
  
     ![原則定義 - 原則結果](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "原則定義 - 原則結果")  
  
3.  以滑鼠右鍵按一下任何相符的記錄（含綠色圖示），然後按一下 [**查看詳細資料**] 以查看比對的詳細資料，例如每個欄位分數占整體符合分數的比重。  
  
     ![[符合分數詳細資料] 對話方塊](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "[符合分數詳細資料] 對話方塊")  
  
4.  按一下 [**關閉**] 以關閉 [**符合分數詳細資料**] 對話方塊。  
  
5.  按一下頁面底部的 [比對**結果**] 索引標籤。 此索引標籤會提供詳細資料，例如相符記錄的數目、不相符記錄的數目、具有相符記錄的叢集數目、平均叢集大小、最小叢集大小和最大叢集大小。 如需詳細資訊，請參閱建立比對[原則](https://msdn.microsoft.com/library/hh270290.aspx)。 您無法從這個活動匯出結果。 您只會定義比對原則，方式是使用取樣資料來針對取樣資料測試規則和原則。  
  
     ![比對結果索引標籤](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "比對結果索引標籤")  
  
6.  按一下 **[完成]** 完成比對原則的建立。  
  
    > [!NOTE]  
    >  您已經在這裡定義比對原則，因此無法將結果匯出到輸出檔。 您基本上已經使用範例輸入檔、建立規則，並針對取樣資料測試規則和原則 (目標是要定義原則)。  
  
7.  在 [SQL Server Data Quality Services] 對話方塊中，按一下 [**發佈**]，然後按一下訊息方塊上的 **[確定]** 。 現在，您所定義的比對原則會發佈到**供應商**知識庫。 您可以使用此知識庫，針對輸入檔執行比對程序，以識別並移除重複項。  
  
## <a name="next-step"></a>後續步驟  
 [工作 3：建立及執行資料品質專案以進行比對](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
