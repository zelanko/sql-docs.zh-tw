---
title: "建立及管理全文檢索目錄 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "全文檢索目錄 [SQL Server], 建立"
  - "全文檢索搜尋 [SQL Server], 使用 SQL Server Management Studio"
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# 建立及管理全文檢索目錄
  全文檢索目錄是不屬於任何檔案群組的虛擬物件。它是參考一組全文檢索索引的邏輯概念。  
  
##  <a name="creating"></a> 建立全文檢索目錄  
  
#### 建立全文檢索目錄  
  
1.  在物件總管中，展開伺服器，並展開 [資料庫]，然後展開您要在其中建立全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]，然後以滑鼠右鍵按一下 [全文檢索目錄]。  
  
3.  選取 [新增全文檢索目錄]。  
  
4.  在 [新增全文檢索目錄] 對話方塊中，為您要重新建立的目錄指定資訊。 如需詳細資訊，請參閱[全文檢索搜尋](../Topic/New%20Full-Text%20Catalog%20\(General%20Page\).md)。  
  
    > [!NOTE]  
    >  全文檢索目錄識別碼從 00005 開始，每次新增一個目錄時識別碼便增加一號。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
   
  
##  <a name="props"></a> 檢視全文檢索目錄的屬性  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數 (例如 FULLTEXTCATALOGPROPERTY) 可以用來取得各種全文檢索索引相關屬性的值。 此資訊適用於管理和疑難排解全文檢索搜尋。  
  
 下表列出與全文檢索目錄相關的屬性。  
  
|屬性|描述|函數|  
|--------------|-----------------|--------------|  
|**AccentSensitivity**|區分腔調字設定。|[FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)|  
|**ImportStatus**|是否正在匯入全文檢索目錄。|FULLTEXTCATALOGPROPERTY|  
|**IndexSize**|全文檢索目錄的大小 (以 MB 為單位)。|FULLTEXTCATALOGPROPERTY|  
|**ItemCount**|目前在全文檢索目錄中的全文檢索索引項目數。|FULLTEXTCATALOGPROPERTY|  
|**MergeStatus**|主要合併是否正在進行中。|FULLTEXTCATALOGPROPERTY|  
|**PopulateCompletionAge**|前次全文檢索索引母體擴展完成和 01/01/1990 00:00:00 之間的時差 (以秒為單位)。|FULLTEXTCATALOGPROPERTY|  
|**PopulateStatus**|擴展狀態。<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|FULLTEXTCATALOGPROPERTY|  
|**UniqueKeyCount**|全文檢索目錄中唯一索引鍵的數目。|FULLTEXTCATALOGPROPERTY|  
  
   
  
##  <a name="rebuildone"></a> 重建全文檢索目錄  
  
#### 重建全文檢索目錄  
  
1.  在物件總管中，展開伺服器，再展開 [資料庫]，然後展開含有您要重建其全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]，然後展開 [全文檢索目錄]。  
  
3.  以滑鼠右鍵按一下要重建的全文檢索目錄名稱，然後選取 [重建]。  
  
4.  出現 [您要刪除全文檢索目錄，並重建目錄嗎?] 問題時，按一下 [確定]。  
  
5.  在 [重建全文檢索目錄] 對話方塊中，按一下 [關閉]。  
  
   
  
##  <a name="rebuildall"></a> 重建資料庫的所有全文檢索目錄  
  
#### 重建資料庫的全文檢索目錄  
  
1.  在物件總管中，展開伺服器，再展開 [資料庫]，然後展開含有您要重建之全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]，然後以滑鼠右鍵按一下 [全文檢索目錄]。  
  
3.  選取 [全部重建]。  
  
4.  出現 [您要刪除所有全文檢索目錄，並重建這些目錄嗎?] 問題時，按一下 [確定]。  
  
5.  在 [重建所有全文檢索目錄] 對話方塊中，按一下 [關閉]。  
  
  
  
##  <a name="removing"></a> 移除資料庫中的全文檢索目錄  
  
#### 從資料庫移除全文檢索目錄  
  
1.  在物件總管中，依序展開 [伺服器]、[資料庫]，並展開含有您要移除之全文檢索目錄的資料庫。  
  
2.  展開 [儲存體]，再展開 [全文檢索目錄]。  
  
3.  以滑鼠右鍵按一下要移除的全文檢索目錄，然後選取 [刪除]。  
  
4.  在 **[刪除物件]** 對話方塊中，按一下 **[確定]**。  
  
  
## 另請參閱  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
  