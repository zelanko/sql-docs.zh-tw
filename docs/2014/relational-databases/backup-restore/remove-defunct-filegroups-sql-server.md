---
title: 移除無用的檔案群組 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- piecemeal restores [SQL Server], defunct filegroups
- defunct filegroups
- restoring filegroups [SQL Server]
- deferred transactions
- filegroups [SQL Server], defunct
- unrestored filegroups
ms.assetid: 055f9c6a-5c18-4942-98e7-ec918f0ff975
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2a59277110d91ffd40a2db7d62fd3a01aa109dfc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921550"
---
# <a name="remove-defunct-filegroups-sql-server"></a>移除無用的檔案群組 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來移除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中無用的檔案群組。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要使用下列項目移除無用的檔案群組：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   本主題與包含多個檔案或檔案群組而且在簡單模式下僅供唯讀之檔案群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關。  
  
-   當移除了離線檔案群組，在檔案群組中的所有檔案就會變成無用。  
  
###  <a name="Recommendations"></a> 建議  
  
-   如果未還原的檔案群組永遠都不需要還原，您可以從資料庫中將它移除，讓檔案群組成為 *「無用」* 。 無用的檔案群組永遠都不能還原至此資料庫，但其中繼資料繼續保留在資料庫中。 檔案群組變成無用之後，資料庫可以重新啟動，復原會讓資料庫在已還原的檔案群組之間保持一致。  
  
     例如，讓檔案群組成為無用是解決因資料庫中不再需要的離線群組而造成之延遲交易的一項選擇。 因檔案群組離線而延遲的交易會在檔案群組變成無用之後移出延遲狀態。 如需詳細資訊，請參閱 [延遲交易 &#40;SQL Server&#41;](deferred-transactions-sql-server.md)中無用的檔案群組。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-remove-defunct-filegroups"></a>若要移除無用的檔案群組  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** ，以滑鼠右鍵按一下要從中刪除檔案的資料庫，再按一下 **[屬性]** 。  
  
3.  選取 **[檔案]** 頁面。  
  
4.  在 **[資料庫檔案]** 方格中，選取要刪除的檔案，按一下 **[移除]** ，然後按一下 **[確定]** 。  
  
5.  選取 **[檔案群組]** 頁面。  
  
6.  在 **[資料列]** 方格中，選取要刪除的檔案群組，按一下 **[移除]** ，然後按一下 **[確定]** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-defunct-filegroups"></a>若要移除無用的檔案群組  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 (**附註：** 此範例假設檔案和檔案群組已經存在。 若要建立這些物件，請參閱 [ALTER DATABASE 檔案及檔案群組選項](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)主題中的範例 B。)第一個範例會使用 `test1dat3` 陳述式搭配 `test1dat4` 子句，從無用的檔案群組中移除 `ALTER DATABASE` 和 `REMOVE FILE` 檔案。 第二個範例會使用 `Test1FG1` 子句，移除無用的檔案群組 `REMOVE FILEGROUP`。  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat3 ;  
ALTER DATABASE AdventureWorks2012  
REMOVE FILE test1dat4 ;  
GO  
  
```  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
REMOVE FILEGROUP Test1FG1 ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [延遲交易 &#40;SQL Server&#41;](deferred-transactions-sql-server.md)   
 [檔案還原 &#40;完整復原模式&#41;](file-restores-full-recovery-model.md)   
 [檔案還原 &#40;簡單復原模式&#41;](file-restores-simple-recovery-model.md)   
 [線上還原 &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [還原頁面 &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
