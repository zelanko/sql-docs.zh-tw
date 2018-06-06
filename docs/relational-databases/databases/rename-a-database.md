---
title: 重新命名資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f6ffe861f520bd0d580b3be540ad39b622cf4918
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="rename-a-database"></a>重新命名資料庫
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中重新命名使用者定義資料庫。 資料庫的名稱可以包含任何依照識別碼規則的字元。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **使用下列方法重新命名資料庫：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After renaming a database](#FollowUp)  

> [!NOTE]
> 若要重新命名 Azure SQL Database 中的資料庫，請使用 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md) 陳述式。 若要重新命名 Azure SQL 資料倉儲或平行處理資料倉儲中的資料庫，請使用 [RENAME (Transact-SQL)](/t-sql/statements/rename-transact-sql) 陳述式。
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您無法重新命名系統資料庫。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-database"></a>若要重新命名資料庫  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  確定沒有人使用此資料庫，然後[將資料庫設定為單一使用者模式](../../relational-databases/databases/set-a-database-to-single-user-mode.md)。  
  
3.  展開 [資料庫]，以滑鼠右鍵按一下要重新命名的資料庫，然後按一下 [重新命名]。  
  
4.  輸入新的資料庫名稱，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-rename-a-database"></a>若要重新命名資料庫  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會將 `AdventureWorks2012` 資料庫的名稱變更為 `Northwind`。  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
###  <a name="TsqlExample"></a>   
##  <a name="FollowUp"></a> 待處理：重新命名資料庫之後  
 重新命名任何資料庫之後，請備份 **master** 資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [資料庫識別碼](../../relational-databases/databases/database-identifiers.md)  
  
  
