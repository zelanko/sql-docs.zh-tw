---
title: Enable Stretch Database for a table
ms.date: 08/05/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, enabling table
- enabling table for Stretch Database
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 49d3f7fa266be69c767b0fb0450cc6898351f39b
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843812"
---
# <a name="enable-stretch-database-for-a-table"></a>Enable Stretch Database for a table
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  若要設定 Stretch Database 的資料表，請在 SQL Server Management Studio 中為資料表選取 [延展 | 啟用]  ，開啟 [對資料表啟用延展精靈]  。 您也可以使用 Transact-SQL 對現有的資料表啟用 Stretch Database，或建立已啟用 Stretch Database 的新資料表。  
  
-   如果您將原始資料儲存在個別的資料表中，可以遷移整個資料表。  
  
-   若您的資料表同時包含作用及原始資料，您可以指定篩選函數，以選取要移轉的資料列。    
 
 **必要條件**。 如果您為資料表選取了 [延展 | 啟用]  ，卻未針對資料庫啟用 Stretch Database，精靈會先設定 Stretch Database 資料庫。 請遵循[開始執行 [啟用資料庫的延展功能精靈]](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) 的步驟著手，而不是本文中的步驟。  
  
 **權限**。 在資料庫或資料表上啟用 Stretch Database 需要 db_owner 權限。 在資料表上啟用 Stretch Database 也需要資料表的 ALTER 權限。  

 > [!NOTE]
 > 稍後，如果您停用 Stretch Database，請記住針對資料表或資料庫停用 Stretch Database，並不會刪除遠端物件。 若您想要刪除遠端資料表或遠端資料庫，則必須使用 Azure 管理入口網站將其卸除。 遠端物件會繼續產生 Azure 成本，直到您手動將其刪除為止。
 
##  <a name="EnableWizardTable"></a> 使用精靈在資料表上啟用 Stretch Database  
 **啟動精靈**  
 1.  在 SQL Server Management Studio 的 [物件總管] 中，選取要啟用 Stretch 的資料表。  
  
2.  按一下滑鼠右鍵並選取 [延展]  ，然後選取 [啟用]  來啟動精靈。  
  
 **簡介**  
 檢閱精靈的用途及必要條件。  
  
 **選取資料庫資料表**  
 確認已顯示並選取您要啟用的資料表。  
  
 您可以移轉整個資料表，也可以在精靈中指定簡單的篩選函數。 如果您想要使用不同類型的篩選函數來選取要移轉的資料列，請執行下列其中一項操作。  
  
-   結束精靈，然後執行 ALTER TABLE 陳述式來啟用資料表的延展功能以及指定篩選函數。  
  
-   結束精靈之後，請執行 ALTER TABLE 陳述式來指定篩選函數。 如需必要的步驟，請參閱 [Add a filter function after running the Wizard](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz)(在執行精靈後新增篩選函數)。  
  
 本文稍後將描述 ALTER TABLE 語法。  
  
 **摘要**  
 檢閱您輸入的值和在精靈中選取的選項。 然後選取 [完成]  以啟用 Stretch。  
  
 **結果**  
 檢閱結果。  
  
##  <a name="EnableTSQLTable"></a> 使用 Transact-SQL 在資料表上啟用 Stretch Database  
 您可以對現有的資料表啟用 Stretch Database，或使用 Transact-SQL 建立已啟用 Stretch Database 的新資料表。  
  
### <a name="options"></a>選項。  
 當您執行 CREATE TABLE 或 ALTER TABLE 在資料表上啟用 Stretch Database 時，請使用下列選項。  
  
-   如果資料表同時包含作用及原始資料，您可以選擇使用 `FILTER_PREDICATE = <function>` 子句指定函數來選取要遷移的資料列。 此述詞必須呼叫內嵌資料表值函數。 如需詳細資訊，請參閱 [Select rows to migrate by using a filter function](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)(使用篩選函數選取要移轉的資料列)。 若您未指定篩選函數，則會移轉整個資料表。  
  
    > [!IMPORTANT]  
    > 若您提供執行狀況不佳的篩選函數，資料移轉也無法順利執行。 Stretch Database 使用 CROSS APPLY 運算子，將篩選函數套用至資料表。  
  
-   指定 `MIGRATION_STATE = OUTBOUND` 立即啟動資料移轉，或指定  `MIGRATION_STATE = PAUSED` 延後啟動資料移轉。  
  
### <a name="enable-stretch-database-for-an-existing-table"></a>為現有的資料表啟用 Stretch Database  
 若要設定現有的 Stretch Database 資料表，請執行 ALTER TABLE 命令。  
  
 以下是移轉整份資料表，並立即開始移轉資料的範例。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 下例只移轉 `dbo.fn_stretchpredicate` 內嵌資料表值函數所識別的資料列，並延後資料移轉。 如需有關篩選函數的詳細資訊，請參閱 [Select rows to migrate by using a filter function](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)(使用篩選函數選取要移轉的資料列)。  
  
```sql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
### <a name="create-a-new-table-with-stretch-database-enabled"></a>建立已啟用 Stretch Database 的新資料表  
 若要建立已啟用 Stretch Database 的新資料表，請執行 CREATE TABLE 命令。  
  
 以下是移轉整份資料表，並立即開始移轉資料的範例。  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 下例只移轉 `dbo.fn_stretchpredicate` 內嵌資料表值函數所識別的資料列，並延後資料移轉。 如需有關篩選函數的詳細資訊，請參閱 [Select rows to migrate by using a filter function](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)(使用篩選函數選取要移轉的資料列)。  
  
```sql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
