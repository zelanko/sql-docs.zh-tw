---
title: "重建索引工作 (維護計畫) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- reindex
- sql13.swb.maint.reindex.f1
helpviewer_keywords:
- Rebuild Index Task dialog box
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d8dd428e1aded14e6e75c338b12c8b04cf722a8
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="rebuild-index-task-maintenance-plan"></a>重建索引工作 (維護計畫)
  使用 [重建索引工作] 對話方塊，以新的填滿因數重新建立資料庫資料表上的索引。 填滿因數會決定索引中每頁的空白數量，以配合未來擴充需要。 將資料加入資料表時，因為沒有維護填滿因數，所以可用空間都會填滿。 重新組織資料與索引頁面可以重新建立可用空間。  
  
 [重建索引工作] 會使用 ALTER INDEX 陳述式。 如需此頁面所描述之選項的詳細資訊，請參閱 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)。  
  
## <a name="options"></a>選項  
 **連接**  
 選取執行此工作時要使用的伺服器連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 下面會描述 **[新增連接]** 對話方塊。  
  
 **資料庫**  
 指定受此工作影響的資料庫。  
  
-   **所有資料庫**  
  
     產生維護計畫，針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行維護工作，但 tempdb 除外。  
  
-   **所有系統資料庫**  
  
     產生維護計畫，針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行維護工作，但 tempdb 除外。 不會針對使用者建立的資料庫執行維護工作。  
  
-   **所有使用者資料庫**  
  
     產生維護計畫，針對所有使用者建立的資料庫執行維護工作。 不會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行任何維護工作。  
  
-   **這些特定的資料庫**  
  
     產生維護計畫，只針對選取的資料庫執行維護工作。 如果選擇此選項，則必須在清單中至少選取一個資料庫。  
  
    > [!NOTE]  
    >  維護計畫只針對相容性層級設為 80 (含) 以上的資料庫來執行。 不會顯示相容性層級設為 70 或更低的資料庫。  
  
 **物件**  
 限制 [選取範圍] 格線僅顯示資料表、檢視或兩者。  
  
 **選取範圍**  
 指定受此工作影響的資料表或索引。 [物件] 方塊中的 **[資料表和檢視]** 為選取狀態時無法使用。  
  
 **預設每頁可用空間**  
 將資料庫中的資料表索引卸除，並以建立索引時指定的填滿因數重新建立它們。  
  
 **將每頁可用空間變更為**  
 將資料庫中的資料表索引卸除，並以新的、自動計算的填滿因數重新建立它們，以在索引頁面上保留指定的可用空間。 百分比愈高，在索引頁面上保留的可用空間就愈多，而索引也愈大。 有效的數值範圍為 0 到 100。  
  
 **在 tempdb 中排序結果**  
 使用 `SORT_IN_TEMPDB` 選項，決定索引建立期間產生的中繼排序結果要暫時儲存的位置。 如果排序作業不是必要項目，或是可以在記憶體中執行排序，則會忽略 `SORT_IN_TEMPDB`選項。  
  
 **索引頁預留空間**  
 指定索引填補  
  
 **索引保留在線上**  
 使用 `ONLINE` 選項，而這個選項可讓使用者在索引作業期間存取基礎資料表或叢集索引資料以及任何相關的非叢集索引。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都無法使用線上索引作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 **不要重建索引 | 離線重建索引**  
 指定如何處理無法在線上重建的索引類型。  
  
 **MAXDOP**  
 指定一個值來限制執行平行計畫所用的處理器數目。  
  
 **使用低優先權**  
 選取此選項以等候低優先權鎖定。  
  
 **在等候之後中止**  
 指定經過 [持續時間上限] 所指定的時間之後該怎麼做。  
  
 **持續時間上限**  
 指定等候低優先權鎖定的時間上限。  
  
 **檢視 T-SQL**  
 根據選取的選項，檢視此工作在伺服器上執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  受影響的物件數目較為大量時，會多花一些時間才會顯示。  
  
## <a name="new-connection-dialog-box"></a>新增連接對話方塊  
 **連接名稱**  
 輸入新連接的名稱。  
  
 **選取或輸入伺服器名稱**  
 選取執行此工作時要連接的伺服器。  
  
 **重新整理**  
 重新整理可用的伺服器清單。  
  
 **輸入要登入到伺服器的資訊**  
 指定如何對伺服器進行驗證。  
  
 **使用 Windows 整合式安全性**  
 使用 Windows 驗證連接 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
 **使用特定的使用者名稱和密碼**  
 使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 驗證，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 無法使用此選項。  
  
 **使用者名稱**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)   
 [線上索引作業的指導方針](../../relational-databases/indexes/guidelines-for-online-index-operations.md)   
 [線上索引作業如何運作](../../relational-databases/indexes/how-online-index-operations-work.md)   
 [線上執行索引作業](../../relational-databases/indexes/perform-index-operations-online.md)  
  
  

