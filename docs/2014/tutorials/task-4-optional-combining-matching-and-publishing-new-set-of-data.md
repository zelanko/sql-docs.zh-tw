---
title: 工作4（選擇性）：結合、比對及發行新的資料集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13a13f03-b307-4555-8e33-6d98c459d994
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2d27a5bcd87ffd84b33de229d955dc9494846a72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489275"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>工作 4 (選擇性)：結合、比對及發行新的資料集
  經過一段時間後，您需要將更多的資料加入至 MDS 儲存機制。 在加入資料之前，比較新資料與已在 MDS 中管理的資料可能會很有用，以確保您不會加入重複或不正確的資料。 在適用於 Excel 的 Master Data Services 增益集中，您可以結合兩個工作表中的資料然後比較資料，以識別重複項並加以移除，之後再將資料發行到 MDS。 MDS Excel 增益集的比對功能會使用 DQS 比對功能來識別資料中的相符內容。 在這項工作中，您會將兩個工作表中的資料結合到一個工作表，然後執行比對活動來識別重複項並加以移除，之後再將資料發行到 MDS。 如需詳細資訊，請參閱[適用于 Excel 的 MDS 增益集中的資料品質](https://msdn.microsoft.com/library/hh548681.aspx)比對和[合併資料](https://msdn.microsoft.com/library/hh548680.aspx)主題。  
  
1.  啟動新的**Excel**實例。 按一下 [**開始**]，指向 [**執行**]，輸入**Excel**，然後按一下 **[確定]**。  
  
2.  按一下功能表列上的 [**主要資料**]，切換至 [**主要資料**] 索引標籤。  
  
3.  在 [**連接和載入]** 群組中，按一下功能區上的 **[連接**]，連接到**MDS 伺服器**。 您在這一課的稍早已經設定這個連接。  
  
     ![Excel - [主要資料] 索引標籤上的 [顯示總管] 按鈕](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel - [主要資料] 索引標籤上的 [顯示總管] 按鈕")  
  
4.  您應該會在右側看到 [**主要資料總管**] 窗格。 如果您看不到主要資料總管，請按一下功能區上的 [**顯示瀏覽器**] 按鈕。  
  
5.  在 [**主資料總管**] 視窗中，選取**模型**下拉式清單中的 [**供應商**]。 您應該會看到此模型有一個實體：**供應商**。  
  
     ![Excel - [主資料總管] 視窗](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel - [主資料總管] 視窗")  
  
6.  按兩下 [實體] 清單中的 [**供應商**]，將實體成員載入至 Excel 工作表。  
  
7.  按一下底部的 [ **sheet2** ] 以切換至 [ **sheet2** ] 索引標籤。如果您沒有看到 [ **Sheet2**]，請加入新的工作表。  
  
8.  開啟**供應商 .xls**檔案（包含在教學課程檔案中的原始輸入檔），並將所有（三個）資料列從**CombineAndCleanse**工作表複製到**Sheet2**。  
  
9. 切換回已連接至**MDS**的**第1冊-Microsoft Excel** （而非**清理和相符的供應商清單**Excel）中的**供應商**工作表。  
  
10. 按一下功能表列上的 [**主要資料**]。  
  
11. 按一下功能區上的 [**合併資料**]。 您會看到 [**結合資料**] 對話方塊。  
  
12. 在 [**結合資料**] 對話方塊中，按一下 [**要與 MDS 資料結合的範圍**] 文字方塊旁邊的按鈕，如下圖所示。  
  
     ![Excel - [結合資料] 對話方塊](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel - [結合資料] 對話方塊")  
  
13. 您現在應該會看到縮小的對話方塊。 現在，按一下 [ **sheet2** ] 以切換至 [ **sheet2** ] 索引標籤，其中包含4個數據列（包括一個標頭資料列）的新供應商資料。  
  
14. 在 [ **Sheet2**] 中，選取**包含標頭資料列的所有資料列**（即使它們看似已選取）。 您應該會看到 [**要與 MDS 資料結合的範圍**] 已自動更新。  
  
     ![Excel - [結合資料] 對話方塊 - 最小化](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel - [結合資料] 對話方塊 - 最小化")  
  
15. 切換回 [**供應商**] 索引標籤，而不關閉 [**結合資料**] 對話方塊。  
  
16. 按一下**文字方塊**旁邊的**按鈕**。 您現在應該會看到對話方塊已放大。 您應該會看到 [**供應商**MDS**實體**] 資料行與**Excel**資料行之間的所有對應都會自動填入。  
  
     ![Excel - 有資料填入的 [結合資料] 對話方塊](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel - 有資料填入的 [結合資料] 對話方塊")  
  
17. 請確定 [程式**代碼**實體] 資料行對應至工作表中的 [已**供應**專案] 資料行，而且 [**郵遞區號**] 實體資料行對應至工作表中的 [**郵遞區號**] 資料行。  
  
18. 在 [**結合資料**] 對話方塊中，按一下 [**合併**]。  
  
19. 確認三個資料列已加入至工作表底部，而且應該有色彩標示。  
  
     ![Excel - 結合之後的新元素](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel - 結合之後的新元素")  
  
20. 按一下功能區上的 [**數學資料**] 以識別重複專案。 此功能會使用 DQS 的比對功能。  
  
21. 在 [比對**資料**] 對話方塊中，選取 [適用于**DQS 知識庫**的**供應商**]。  
  
     ![Excel - [比對資料] 對話方塊](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel - [比對資料] 對話方塊")  
  
22. 將工作表資料行對應至定義域，如下表所示。  
  
    |工作表資料行|網域|  
    |----------------------|------------|  
    |Code (您已上傳供應商識別碼當做 MDS 中供應商實體的代碼)|Supplier ID|  
    |Name (您已上傳供應商名稱當做 MDS 中供應商實體的名稱)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. 針對 [程式**代碼**資料**行對應]** 選取 [必要條件]。  
  
24. 輸入 [ **70%** ] 作為 [**供應商名稱**] 的**權數**，而**30%** 作為 [**連絡人電子郵件**] 的**權數**（如圖所示）。  
  
25. 按一下 [確定]  。  
  
26. 比對程式應該會為供應商識別一個重複的**代碼： S1**。  
  
     ![Excel - 比對結果](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel - 比對結果")  
  
27. 選取 [**重複的資料列（橙色）**]，按一下滑鼠右鍵，然後按一下 [**刪除**] 來刪除資料列。  
  
28. 刪除**CLUSTER_ID**的資料行，因為您不再需要它。  
  
29. 按一下 [**發佈**]，將具有**代碼 S66**和**S57**的其他兩個新記錄發佈到 MDS。  
  
30. 在 [**發行並批註**] 對話方塊中，加入**批註**，然後按一下 [**發佈**]。  
  
31. 切換至**主資料管理員 Web 應用程式**。  
  
32. 在 [首頁] 頁面上，確定已針對**模型**選取 [**供應商**]，然後按一下 [ **Explorer**]。 如果您已經開啟**Explorer** ，請重新整理網際網路瀏覽器。  
  
33. 依程式**代碼****排序**清單，並使用**S57**和**S66**做為程式碼尋找記錄。 您也可以使用工具列上的 [**篩選**] 按鈕來搜尋清單中的特定記錄。  
  
34. 現在，關閉**Book1-Microsoft Excel**視窗，而不儲存檔案。  
  
## <a name="next-step"></a>後續步驟  
 [工作 5：從 Excel 建立定義域屬性](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
