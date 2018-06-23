---
title: 工作 5： 匯出清理結果到 Excel 檔案 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f8a716d3b6c0007ceb89f36f23584bb4adb4f706
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023454"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>工作 5：將清理結果匯出到 Excel 檔案
  在這項工作中，您會將清理活動的結果匯出到 Excel 檔案。 請參閱[匯出階段](http://msdn.microsoft.com/library/hh213061.aspx#Export)如需詳細資訊。  
  
1.  在右窗格中，選取**Excel**如**目的型別**。  
  
2.  按一下**瀏覽**，將輸出檔案名稱指定為**Cleansed Supplier List.xls**，然後按一下 **開啟**。  
  
3.  選取**Data Only**如**輸出**格式匯出已清理的資料。 第二個選項，**資料和清理資訊**，可讓您匯出清理活動詳細資料，連同已清理的資料。 **標準化格式**選項可讓您套用任何您定義的值，該網域的網域的輸出格式。 在本教學課程中，您尚未在任何定義域定義輸出格式。  
  
     ![匯出清理結果頁面](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "匯出清理結果頁面")  
  
4.  按一下**匯出**，匯出的資料。 不要在上面按一下**完成**尚未。  
  
5.  按一下**關閉**上**匯出** 對話方塊。  
  
6.  按一下**完成**完成的活動。 如果您忘記匯出結果後，再按一下**完成**，按一下 **開啟資料品質專案**中的主頁面**DQS 用戶端**，選取**清理供應商清單**從專案中，然後按一下清單**下一步**移至畫面底部**匯出**試清理程序的階段。 您也可以切換到**管理和檢視結果** 索引標籤，即可**回** 按鈕。  
  
7.  開啟**Cleansed Supplier List.xls**並執行下列動作：  
  
    1.  在工作表中搜尋 adventure-work.com，以確定沒有任何電子郵件地址的結尾為 adventure-work.com (沒有 ‘s’ 字元)。  
  
    2.  沒有，請參閱沒有**USA**值**國家/地區**資料行。  
  
    3.  搜尋**洛杉磯**並查看**狀態**設**CA**。  
  
    4.  確認沒有任何條款**Co.**， **Corp.**，和**Inc.**。  
  
    5.  刪除**地址驗證**從試算表，並儲存 excel 檔案的資料行。 此額外資料行對應至「地址驗證」複合定義域。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 6： 匯入的值從 Cleanse Supplier List 專案](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  