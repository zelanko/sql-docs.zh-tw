---
title: 工作 6： 匯入的值從 Cleanse Supplier List 專案 |Microsoft 文件
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
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7a915013d779392d585bd5609384fab7bffd2800
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031134"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>工作 6：從 Cleanse Supplier List 專案匯入值
  在這項工作中，您會匯入清理程序期間所收集的資料品質知識。 請參閱[清理專案值匯入定義域](http://msdn.microsoft.com/library/hh479581.aspx)如需詳細資訊。 您也將知識庫匯出到 DQS 檔案之前發行更新**供應商**知識庫。  
  
1.  中的主頁面**DQS 用戶端**，按一下 **向右箭號**旁**供應商**下**最近使用的知識庫**按一下**定義域管理**。  
  
2.  按一下**Contact Email**清單中的網域，並切換到**定義域值**右窗格中的索引標籤。  
  
3.  按一下**向下箭號**旁**匯入值** 工具列上按一下圖示**匯入專案值**。  
  
     ![匯入專案值 工具列按鈕](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "匯入專案值 工具列按鈕")  
  
4.  在**匯入專案值**對話方塊中，選取**Cleanse Supplier List**專案，然後按一下**確定**。  
  
5.  請注意，所有電子郵件都會匯入，連同您在互動式清理過程中所做的兩項更正。 請捲動來查看這兩項更正。  
  
    |ReplTest1|更正為|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  重複上述步驟來匯入專案值**國家/地區**網域，請注意，加入新項目修正**United State**至**美國**(與 's')。  
  
    |ReplTest1|更正為|  
    |-----------|----------------|  
    |United State|United States|  
  
7.  若要查看舊的定義域值，請清除**只顯示新**核取方塊。  
  
8.  重複上述步驟來匯入專案值**Supplier Name**網域。 根據預設，您在匯入之後只會看到新值。 若要查看所有值，請清除**只顯示新**核取方塊。 您具有豐富**供應商**與您從清理活動學到的知識庫。 當知識庫越來越強大，清理結果就會越好。  
  
    > [!NOTE]  
    >  它不可能是複合定義域的匯入值。  
  
9. 按一下**匯出知識庫**工具列，然後按一下圖示**匯出知識庫**。  
  
     ![匯出知識庫 功能表](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "匯出知識庫 功能表")  
  
10. 巡覽至教學課程的資料夾，輸入**Suppliers.dqs**如**檔案名稱**，然後按一下**儲存**。 您可以使用這個 DQS 檔案，根據它來建立新的知識庫。  
  
11. 按一下**確定**關閉**匯出知識庫-供應商**訊息方塊。  
  
12. 按一下**完成**完成的活動。  
  
13. 按一下 [發行]。  
  
14. 按一下**確定**訊息方塊上。  
  
## <a name="next-step"></a>下一個步驟  
 [第 3 課： 比對資料來移除重複項從供應商清單](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  