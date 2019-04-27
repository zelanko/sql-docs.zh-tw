---
title: 重建索引工作 (維護計畫) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reindex.f1
- reindex
helpviewer_keywords:
- Rebuild Index Task dialog box
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34bd5a607998c6e37f688ccbadcd4d612d3daea7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806980"
---
# <a name="rebuild-index-task-maintenance-plan"></a>重建索引工作 (維護計畫)
  使用 [重建索引工作] 對話方塊，以新的填滿因數重新建立資料庫資料表上的索引。 填滿因數會決定索引中每頁的空白數量，以配合未來擴充需要。 將資料加入資料表時，因為沒有維護填滿因數，所以可用空間都會填滿。 重新組織資料與索引頁面可以重新建立可用空間。  
  
 [重建索引工作] 會使用 ALTER INDEX 陳述式。  
  
## <a name="options"></a>選項。  
 **[連接]**  
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
  
 **使用預設的可用空間量重新組織頁面**  
 將資料庫中的資料表索引卸除，並以建立索引時指定的填滿因數重新建立它們。  
  
 **每頁的百分比，以可用空間變更**  
 將資料庫中的資料表索引卸除，並以新的、自動計算的填滿因數重新建立它們，以在索引頁面上保留指定的可用空間。 百分比愈高，在索引頁面上保留的可用空間就愈多，而索引也愈大。 有效的數值範圍為 0 到 100。  
  
 **在 tempdb 中排序結果**  
 使用`SORT_IN_TEMPDB`選項，決定索引建立期間產生的中繼排序結果要暫時儲存。 如果排序作業不是必要項目，或是可以在記憶體中執行排序，則會忽略 `SORT_IN_TEMPDB`選項。  
  
 **索引保留在線上時重新編製索引**  
 使用 `ONLINE` 選項，而這個選項可讓使用者在索引作業期間存取基礎資料表或叢集索引資料以及任何相關的非叢集索引。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都無法使用線上索引作業。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 **檢視 T-SQL**  
 根據選取的選項，檢視此工作在伺服器上執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  受影響的物件數目較為大量時，會多花一些時間才會顯示。  
  
## <a name="new-connection-dialog-box"></a>新增連接對話方塊  
 **連接名稱**  
 輸入新連接的名稱。  
  
 **選取或輸入伺服器名稱**  
 選取執行此工作時要連接的伺服器。  
  
 **[重新整理]**  
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
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [索引的 SORT_IN_TEMPDB 選項](../indexes/indexes.md)   
 [線上索引作業的指導方針](../indexes/guidelines-for-online-index-operations.md)   
 [線上索引作業如何運作](../indexes/how-online-index-operations-work.md)   
 [線上執行索引作業](../indexes/perform-index-operations-online.md)  
  
  
