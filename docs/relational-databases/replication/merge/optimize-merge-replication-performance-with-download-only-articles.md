---
title: "使用僅限下載的發行項最佳化合併式複寫效能 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b82a117316022f7c30920d9174855522d374f1b
ms.lasthandoff: 04/11/2017

---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>使用僅限下載的發行項最佳化合併式複寫效能
  合併式複寫提供兩種不同類型的發行項，以滿足不同應用程式的需求。 發行集可包含這兩種類型的一種或兩種，以符合應用程式：  
  
-   標準發行項  
  
-   僅限下載的發行項  
  
 僅限下載的發行項所提供的效能比之標準發行項要好，應在適當的地方使用。  
  
> [!NOTE]  
>  若要使用僅限下載發行項，發行集的相容性層級必須至少為 90RTM。  
  
## <a name="standard-articles"></a>標準發行項  
 標準發行項為預設值，提供全部合併式複寫範圍內的所有功能，包括各種衝突偵測和解決方案。 標準發行項適合於由多個「訂閱者」更新的資料表；始終將除資料表以外的物件 (例如預存程序和檢視) 做為標準發行項來發行。  
  
## <a name="download-only-articles"></a>僅限下載的發行項  
 僅限下載的發行項是為不在「訂閱者」端更新資料的應用程式所設計，例如包含於產品目錄中的一組發行項。 產品目錄一般在「發行者」端而不在「訂閱者」端更新。 因為僅限下載的發行項不能在訂閱者端進行更新，追蹤中繼資料不會傳送給訂閱者。 如此可減少訂閱者上的儲存體並提高效能，特別是網路連接緩慢時。  
  
 僅限下載的發行項結合客訂閱一起使用：如果發行項被設計為僅限下載，則將無法在使用客訂閱的「訂閱者」端插入、更新或刪除這個發行項的資料列。 使用主訂閱類型的「發行者」與「訂閱者」 (一般是重新發行資料到其他「訂閱者」的「訂閱者」) 可插入、更新和刪除資料。 如需用戶端訂閱的詳細資訊，請參閱[訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)。  
  
 若要指定發行項為僅限下載，請參閱＜ [Specify That a Merge Table Article is Download-Only](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)＞。  
  
## <a name="using-different-article-types-in-your-applications"></a>在應用程式中使用不同的發行項類型  
 透過了解應用程式的需求，您可以在最具彈性與最佳效能之間權衡取捨。 例如，在「發行者」端與「訂閱者」端有大量衝突與變更處理的應用程式，將使用由標準發行項組成的發行集。 某些應用程式，例如銷售人員自動化應用程式，含有一些可能發生衝突的發行項，以及另一些做為查閱資料表的發行項，可被指定為僅限下載。 資料項目應用程式 (例如銷售系統各點和現場服務自動化應用程式) 通常使用嚴格地分割資料這一方式來消除衝突，來自某個「訂閱者」的資料決不會流到其他「訂閱者」處。 在這些情況下，不重疊資料分割的組合、僅限下載的發行項和預先計算的資料分割會提供最佳的效能和延展性。 如需不重疊資料分割和預先計算資料分割的詳細資訊，請參閱＜ [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的發行項選項](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [使用條件式刪除追蹤最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
