---
title: 顯示資料庫的資料和記錄空間資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], space
- status information [SQL Server], space
- displaying space information
- disk space [SQL Server], displaying
- databases [SQL Server], space used
- viewing space information
- space allocation [SQL Server], displaying
- data space [SQL Server]
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1beb8cdedbc2b72eadeeb350ee1c3b6d16218205
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970041"
---
# <a name="display-data-and-log-space-information-for-a-database"></a>顯示資料庫的資料和記錄空間資訊
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中顯示資料庫的資料和記錄檔空間資訊。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **使用下列方法，顯示資料庫的資料和記錄空間資訊：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 執行 **sp_spaceused** 的權限會授與 **public** 角色。 只有 **db_owner** 固定資料庫角色的成員，才能夠指定 **@updateusage** 參數。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-display-data-and-log-space-information-for-a-database"></a>若要顯示資料庫的資料和記錄空間資訊  
  
1.  在物件總管中，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** 。  
  
3.  以滑鼠右鍵按一下資料庫，然後依序指向 [報表]****、[標準報表]****，再按一下 [磁碟使用量]****。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-using-sp_spaceused"></a>使用 sp_spaceused 顯示資料庫的資料和記錄空間資訊  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例使用 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) 系統預存程序來報告 `Vendor` 資料表及其索引的磁碟空間資訊。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-querying-sysdatabase_files"></a>透過查詢 sys.database_files 來顯示資料庫的資料和記錄空間資訊  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會查詢 [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) 目錄檢視，以傳回有關 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中資料和記錄檔的特定資訊。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [database_files &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sp_spaceused &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)   
 [將資料或記錄檔加入至資料庫](add-data-or-log-files-to-a-database.md)   
 [刪除資料庫的資料或記錄檔](delete-data-or-log-files-from-a-database.md)  
  
  
