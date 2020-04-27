---
title: 檢視或變更資料庫的屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10ad92286011f6f81fbaff5ab4908007e16bdd45
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870948"
---
# <a name="view-or-change-the-properties-of-a-database"></a>檢視或變更資料庫的屬性
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視或變更資料庫的屬性。 變更資料庫屬性之後，修改會立即生效。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法檢視或變更資料庫的屬性：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   當 AUTO_CLOSE 是 ON 時， [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視中的某些資料行及 DATABASEPROPERTYEX 函數會傳回 NULL，因為資料庫無法擷取資料。 若要解決這個問題，請執行 USE 陳述式來開啟資料庫。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>檢視或變更資料庫的屬性  
  
1.  在**物件總管**中，連接到的實例[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，然後展開該實例。  
  
2.  展開 [資料庫]****，並以滑鼠右鍵按一下要檢視的資料庫，然後按一下 [屬性]****。  
  
3.  在 **[資料庫屬性]** 對話方塊中，選取一個頁面以檢視對應的資訊。 例如，選取 **[檔案]** 頁面以檢視資料和記錄檔資訊。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-property-of-a-database-by-using-databasepropertyex"></a>透過使用 DATABASEPROPERTYEX 檢視資料庫的屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例使用 [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) 系統函數傳回 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之 AUTO_SHRINK 資料庫選項的狀態。 傳回值為 1 表示選項設定為 ON，傳回值為 0 表示選項設定為 OFF。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
GO  
  
```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>透過查詢 sys.databases 檢視資料庫的屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會查詢 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視，以查看 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的數個屬性。 這個範例會傳回資料庫識別碼 (`database_id`)、資料庫是唯讀還是讀寫 (`is_read_only`)、資料庫定序 (`collation_name`)，以及資料庫相容性層級 (`compatibility_level`)。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT database_id, is_read_only, collation_name, compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-properties-of-a-database"></a>變更資料庫的屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中。 此範例判斷 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫上快照集隔離的狀態、變更屬性狀態，然後驗證變更。  
  
     若要判斷快照集隔離的狀態，請選取第一個 `SELECT` 陳述式並按一下 **[執行]**。  
  
     若要變更快照集隔離的狀態，請選取 `ALTER DATABASE` 陳述式並按一下 **[執行]**。  
  
     若要驗證變更，請選取第二個 `SELECT` 陳述式並按一下 **[執行]**。  
  
 [!code-sql[DatabaseDDL#AlterDatabase9](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase9)]  
  
## <a name="see-also"></a>另請參閱  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE SET HADR &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [ALTER DATABASE SET 選項 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [ALTER DATABASE 資料庫鏡像 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [ALTER DATABASE 相容性層級 &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
  
