---
title: 檢視資料庫快照集 (SQL Server) | Microsoft 文件
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL 檢視 SQL Server 資料庫快照集。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
ms.openlocfilehash: a7ba50746752b0c3531d1ae3a0b1b9d4820dea82
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727537"
---
# <a name="view-a-database-snapshot-sql-server"></a>檢視資料庫快照集 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題說明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料庫快照集。  
  
> [!NOTE]  
>  若要建立、刪除或還原為資料庫快照集，都必須使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 **本主題內容**  
  
-   **若要檢視資料庫快照集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要檢視資料庫快照集**  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  展開 **[資料庫]** 。  
  
3.  展開 **[資料庫快照集]** ，然後選取想要檢視的快照集。  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要檢視資料庫快照集**  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  若要列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的資料庫快照集，請查詢 **sys.databases** 目錄檢視的 [source_database_id](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 資料行看看是否有非 NULL 值。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [建立資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [將資料庫還原成資料庫快照集](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
