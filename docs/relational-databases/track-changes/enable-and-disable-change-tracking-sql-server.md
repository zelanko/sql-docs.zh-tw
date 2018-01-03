---
title: "啟用和停用變更追蹤 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change tracking [SQL Server], disabling
- data changes [SQL Server]
- change tracking [SQL Server], enabling
- tracking data changes [SQL Server]
- change tracking [SQL Server], configuring
- data [SQL Server], changing
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 41bac509d07c7aaeea93ab34ee19aecf653fa2e6
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="enable-and-disable-change-tracking-sql-server"></a>啟用和停用變更追蹤 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  此主題描述如何針對資料庫和資料表啟用及停用變更追蹤。  
  
## <a name="enable-change-tracking-for-a-database"></a>為資料庫啟用變更追蹤  
 在您可以使用變更追蹤之前，必須先在資料庫層級啟用變更追蹤。 下列範例將示範如何使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md)來啟用變更追蹤。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 資料庫屬性 &#40;變更追蹤頁面&#41; [資料庫屬性 &amp;#40;變更追蹤頁面&amp;#41;](../../relational-databases/databases/database-properties-changetracking-page.md) 中的變更追蹤。  
  
 當您啟用變更追蹤時，可以指定 CHANGE_RETENTION 和 AUTO_CLEANUP 選項，而且您可以在啟用變更追蹤之後的任何時間變更這些值。  
  
 變更保留值會指定保存變更追蹤資訊的期間。 早於此期間的變更追蹤資訊會定期遭到移除。 當您設定這個值時，應該考量應用程式與資料庫資料表同步處理的頻率。 指定的保留期間至少必須與同步處理之間的期間上限一樣長。 如果應用程式在較長的間隔上取得變更，所傳回的結果可能會不正確，因為變更資訊的某部分可能已遭到移除。 為了避免取得不正確的結果，應用程式可以使用 CHANGE_TRACKING_MIN_VALID_VERSION 系統函數來判斷同步處理之間的間隔是否已經過長。  
  
 您可以使用 AUTO_CLEANUP 選項來啟用或停用移除老舊變更追蹤資訊的清除工作。 當有暫時性的問題阻礙應用程式同步處理時，這樣的處理方式會很實用，而且在問題解決之前，必須先暫停用來移除早於保留期間之變更追蹤資訊的程序。  
  
 如果是使用變更追蹤的任何資料庫，請注意以下事項：  
  
-   若要使用變更追蹤，資料庫相容性層級必須設定為 90 以上 (含)。 如果資料庫的相容性層級低於 90，您也可以設定變更追蹤。 不過，用來取得變更追蹤資訊的 CHANGETABLE 函數將會傳回錯誤。  
  
-   若要確保所有變更追蹤資訊都一致，使用快照隔離是最簡單的方式。 基於這個原因，我們強烈建議您將資料庫的快照隔離設定為 ON。 如需詳細資訊，請參閱[使用變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)。  
  
## <a name="enable-change-tracking-for-a-table"></a>為資料表啟用變更追蹤  
 您必須針對您要追蹤的每一個資料表啟用變更追蹤。 啟用變更追蹤時，系統會針對資料表中受到 DML 作業影響的所有資料列維護變更追蹤資訊。  
  
 下列範例示範如何使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)，為資料表啟用變更追蹤。  
  
```sql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 資料庫屬性 &#40;變更追蹤頁面&#41; [資料庫屬性 &amp;#40;變更追蹤頁面&amp;#41;](../../relational-databases/databases/database-properties-changetracking-page.md) 中的變更追蹤。  
  
 當 TRACK_COLUMNS_UPDATED 選項設定為 ON 時， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會將哪些資料行已更新的相關額外資訊儲存到內部變更追蹤資料表。 資料行追蹤只能讓應用程式同步處理已經更新的那些資料行。 這樣可以改善效率與效能。 但是，由於維護資料行追蹤資訊會增加額外的儲存負擔，所以此選項預設為 OFF。  
  
## <a name="disable-change-tracking-for-a-database-or-table"></a>為資料庫或資料表停用變更追蹤  
 在可以針對資料庫將變更追縱設定為 OFF 之前，必須先針對所有變更追蹤的資料表停用變更追蹤。 若要判斷已針對資料庫啟用變更追蹤的資料表，請使用 [sys.change_tracking_tables](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md) 目錄檢視。  
  
 當資料庫中沒有任何資料表追蹤變更時，您可以為此資料庫停用變更追蹤。 下列範例將示範如何使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md)，為資料庫停用變更追蹤。  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 下列範例示範如何使用 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)，為資料表停用變更追蹤。  
  
```sql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫屬性 &#40;變更追蹤頁面&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [關於變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [使用變更資料 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [管理變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
  
