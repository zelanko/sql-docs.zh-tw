---
title: 工作6：從清理供應商清單專案匯入值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cb3e7a85254cac96b8b8541de57b494e96b8928f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061072"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>工作 6：從清理供應商清單專案匯入值
  在這項工作中，您會匯入清理程序期間所收集的資料品質知識。 如需詳細資訊，請參閱[將清理專案值匯入定義域](https://msdn.microsoft.com/library/hh479581.aspx)主題。 您也會將知識庫匯出到 DQS 檔案，然後再發行更新的**供應商**知識庫。  
  
1.  在**DQS 用戶端**的主頁面中，按一下 [**最近使用的知識庫**] 底下 [**供應商**] 旁**的向右箭**號，然後按一下 [**定義域管理**]。  
  
2.  按一下網域清單中的 [**連絡人電子郵件**]，然後切換至右窗格中的 [**定義域值**] 索引標籤。  
  
3.  按一下工具列上 [匯**入值**] 圖示旁的**向下箭**號，然後按一下 [匯**入專案值**]。  
  
     ![[匯入專案值] 工具列按鈕](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "[匯入專案值] 工具列按鈕")  
  
4.  在 [匯**入專案值**] 對話方塊中，選取 [**清理供應商清單**] 專案，然後按一下 **[確定]**。  
  
5.  請注意，所有電子郵件都會匯入，連同您在互動式清理過程中所做的兩項更正。 請捲動來查看這兩項更正。  
  
    |值|更正為|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  重複先前的步驟來匯入**Country**定義域的專案值，並注意是否已新增專案以將**美國**更正為美國 **（含**' s '）。  
  
    |值|更正為|  
    |-----------|----------------|  
    |United State|美國|  
  
7.  若要查看舊的定義域值，請清除 [**只顯示新**的] 核取方塊。  
  
8.  重複先前的步驟，為**供應商名稱**網域匯入專案值。 根據預設，您在匯入之後只會看到新值。 若要查看所有值，請清除 [**只顯示新**的] 核取方塊。 您已使用從清理活動中學到的內容，擴充了**供應商**知識庫。 當知識庫越來越強大，清理結果就會越好。  
  
    > [!NOTE]  
    >  它不可能是複合定義域的匯入值。  
  
9. 按一下工具列上的 [**匯出知識庫**] 圖示，然後按一下 [**匯出知識庫**]。  
  
     ![[匯出知識庫] 功能表](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "[匯出知識庫] 功能表")  
  
10. 流覽至 [教學課程] 資料夾，在 [**檔案名**] 中輸入 [**供應商. dqs** ]，然後按一下 [**儲存**]。 您可以使用這個 DQS 檔案，根據它來建立新的知識庫。  
  
11. 按一下 **[確定]** 以關閉 [**匯出知識庫-供應商**] 訊息方塊。  
  
12. 按一下 **[完成]** 以完成活動。  
  
13. 按一下 **[發行]**。  
  
14. 在訊息方塊上按一下 **[確定]** 。  
  
## <a name="next-step"></a>後續步驟  
 [第 3 課：比對資料，以便從供應商清單中移除重複項](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
