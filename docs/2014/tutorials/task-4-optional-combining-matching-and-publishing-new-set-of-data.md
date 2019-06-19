---
title: 工作 4 (選擇性)：結合、 比對及發行新的資料集 |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489275"
---
# <a name="task-4-optional-combining-matching-and-publishing-new-set-of-data"></a>工作 4 (選擇性)：結合、比對及發行新的資料集
  經過一段時間後，您需要將更多的資料加入至 MDS 儲存機制。 然後再新增資料，它可用來比較新資料與已在 MDS 中，以確保，您不會加入重複或不正確的資料中受管理的資料。 在適用於 Excel 的 Master Data Services 增益集中，您可以結合兩個工作表中的資料然後比較資料，以識別重複項並加以移除，之後再將資料發行到 MDS。 MDS Excel 增益集的比對功能會使用 DQS 比對功能來識別資料中的相符內容。 在這項工作中，您會將兩個工作表中的資料結合到一個工作表，然後執行比對活動來識別重複項並加以移除，之後再將資料發行到 MDS。 請參閱[資料品質比對 MDS 增益集中適用於 Excel](https://msdn.microsoft.com/library/hh548681.aspx)並[結合資料](https://msdn.microsoft.com/library/hh548680.aspx)主題以取得詳細資料。  
  
1.  啟動新執行個體**Excel**。 按一下**開始**，指向**執行**，型別**Excel**，然後按一下**確定**。  
  
2.  切換至**Master Data**索引標籤中的按一下**主要資料**功能表列上。  
  
3.  按一下  **Connect**在功能區上**連接和載入**群組來連接到**MDS 伺服器**。 您在這一課的稍早已經設定這個連接。  
  
     ![Excel-[主要資料] 索引標籤上顯示總管按鈕](../../2014/tutorials/media/et-combinematchandpublishnewsod-01.jpg "Excel-[主要資料] 索引標籤上顯示總管按鈕")  
  
4.  您應該會看到**主資料總管**右邊的窗格。 如果您看不到主資料總管，按一下**顯示總管**功能區上的按鈕。  
  
5.  在 **主資料總管**視窗中，選取**供應商**下拉式清單中**模型**。 您應該會看到此模型有一個實體：**供應商**。  
  
     ![Excel-[主資料總管] 視窗](../../2014/tutorials/media/et-combinematchandpublishnewsod-02.jpg "Excel-[主資料總管] 視窗")  
  
6.  按兩下**供應商**載入 Excel 工作表中的實體成員的實體清單中。  
  
7.  按一下 [ **Sheet2**切換至底部**Sheet2** ] 索引標籤。如果您看不見**Sheet2**，加入新的工作表。  
  
8.  開啟**Suppliers.xls**檔案 （教學課程檔案中包含原始輸入的檔），並將複製的所有 （三個） 的資料列**CombineAndCleanse**工作表**Sheet2**。  
  
9. 切換回**供應商**工作表**Book 1-Microsoft Excel** (不**Cleansed and Matched Supplier 清單**Excel)，連接到**MDS**.  
  
10. 按一下 **主要資料**功能表列上。  
  
11. 按一下 **結合資料**功能區上。 您會看到**結合資料** 對話方塊。  
  
12. 在 **合併資料**對話方塊方塊中，按一下  按鈕旁**要與 MDS 資料結合的範圍**文字方塊中，如下圖所示。  
  
     ![Excel-[結合資料] 對話方塊](../../2014/tutorials/media/et-combinematchandpublishnewsod-03.jpg "Excel-[結合資料] 對話方塊")  
  
13. 您現在應該會看到縮小的對話方塊。 現在，按一下 [ **Sheet2**轉為**Sheet2**具有 4 個資料列 （包括一個標頭資料列） 的新供應商資料] 索引標籤。  
  
14. 在  **Sheet2**，選取**包括標頭資料列的所有資料列**（即使它們似乎已被選取）。 您應該會看到**要與 MDS 資料結合的範圍**會自動更新。  
  
     ![Excel-[結合資料] 對話方塊-最小化](../../2014/tutorials/media/et-combinematchandpublishnewsod-04.jpg "Excel-[結合資料] 對話方塊-最小化")  
  
15. 切換回**供應商**索引標籤上，不需關閉**結合資料** 對話方塊。  
  
16. 按一下 [ **] 按鈕**旁**文字方塊中**。 您現在應該會看到對話方塊已放大。 您應該會看到的資料行之間的所有對應**供應商**MDS**實體**來**Excel**會自動填入資料行。  
  
     ![Excel-[結合資料] 對話方塊以資料填入](../../2014/tutorials/media/et-combinematchandpublishnewsod-05.jpg "Excel-[結合資料] 對話方塊中填入資料")  
  
17. 請確認**程式碼**實體的資料行對應至**SupplierID**工作表中的資料行並**郵遞區號**實體的資料行對應至**郵遞區號**工作表中的資料行。  
  
18. 在 [**合併資料**] 對話方塊中，按一下**結合**。  
  
19. 確認三個資料列已加入至工作表底部，而且應該有色彩標示。  
  
     ![Excel-結合之後的新項目](../../2014/tutorials/media/et-combinematchandpublishnewsod-06.jpg "Excel-結合之後的新項目")  
  
20. 按一下 **數學資料**來識別重複項目功能區上。 此功能會使用 DQS 的比對功能。  
  
21. 在 **比對資料**對話方塊中，選取**供應商**for **DQS 知識庫**。  
  
     ![Excel-比對 [資料] 對話方塊](../../2014/tutorials/media/et-combinematchandpublishnewsod-07.jpg "Excel-比對 [資料] 對話方塊")  
  
22. 將工作表資料行對應至定義域，如下表所示。  
  
    |工作表資料行|Domain|  
    |----------------------|------------|  
    |Code (您已上傳供應商識別碼當做 MDS 中供應商實體的代碼)|Supplier ID|  
    |Name (您已上傳供應商名稱當做 MDS 中供應商實體的名稱)|Supplier Name|  
    |ContactEmailAddress|ContactEmail|  
  
23. 選取 **先決條件**for**程式碼**資料行對應。  
  
24. 輸入**70%** 做為**權數**如**Supplier Name**和**30%** 為**權數**針對**Contact Email**映像所示。  
  
25. 按一下 [確定]  。  
  
26. 比對程序應該識別出具有**程式碼：S1**。  
  
     ![Excel-比對結果](../../2014/tutorials/media/et-combinematchandpublishnewsod-08.jpg "Excel-比對結果")  
  
27. 選取 **重複的資料列 （橘色）** ，按一下滑鼠右鍵，然後按一下**刪除**刪除的資料列。  
  
28. 刪除**CLUSTER_ID**資料行，因為您不再需要它。  
  
29. 按一下 **發佈**發行其他兩筆新記錄**S66**並**S57**至 MDS。  
  
30. 在**發行並註解**對話方塊方塊中，加入**註釋**，然後按一下**發行**。  
  
31. 若要切換**主資料管理員 Web 應用程式**。  
  
32. 在首頁上，確定**供應商**選取**模型**，然後按一下**總管**。 如果您已經有**總管**開啟，請重新整理網際網路瀏覽器。  
  
33. **排序**清單**程式碼**，並尋找記錄**S57**並**S66**碼。 您也可以使用**篩選**來搜尋特定的記錄，在清單中的工具列上的按鈕。  
  
34. 現在，關閉**Book1-Microsoft Excel**視窗，而不用儲存檔案。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 5：從 Excel 建立的網域屬性](../../2014/tutorials/task-5-creating-a-domain-based-attribute-from-excel.md)  
  
  
