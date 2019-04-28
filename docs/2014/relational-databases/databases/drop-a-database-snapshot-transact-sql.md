---
title: 卸除資料庫快照集 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1387b6321ace59ec8a0c13ed03444553f4adf85
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871913"
---
# <a name="drop-a-database-snapshot-transact-sql"></a>卸除資料庫快照集 (Transact-SQL)
  卸除資料庫快照集，就會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 刪除資料庫快照集，並刪除快照集所使用的疏鬆檔案。 卸除資料庫快照集後，快照集的所有使用者連接都會結束。  
  
## <a name="security"></a>安全性  
  
###  <a name="Permissions"></a> 權限  
 具有 DROP DATABASE 權限的任何使用者都可以卸除資料庫快照集。  
  
##  <a name="TsqlProcedure"></a> 如何卸除資料庫快照集 (使用 Transact-SQL)  
 **若要卸除資料庫快照集**  
  
1.  識別您想要卸除的資料庫快照集。 您可以檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中之資料庫的快照集。 如需詳細資訊，請參閱 [檢視資料庫快照集 &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)中之資料庫的快照集。  
  
2.  發出 [DROP DATABASE](/sql/t-sql/statements/drop-database-audit-specification-transact-sql) 陳述式，並指定所要卸除之資料庫快照集的名稱。 其語法如下：  
  
     DROP DATABASE *database_snapshot_name* [ **,**...*n* ]  
  
     其中， *database_snapshot_name* 是所要卸除之資料庫快照集的名稱。  
  
####  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 下列範例會卸除名為 SalesSnapshot0600 的資料庫快照集，而不會影響來源資料庫。  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 SalesSnapshot0600 的任何使用者連接都會結束，而且快照集所使用的所有 NTFS 檔案系統疏鬆檔案也都會被刪除。  
  
> [!NOTE]  
>  如需資料庫快照集使用疏鬆檔案的相關資訊，請參閱 [資料庫快照集 &#40;SQL Server&#41;](database-snapshots-sql-server.md)中之資料庫的快照集。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立資料庫快照集 &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [檢視資料庫快照集 &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [將資料庫還原成資料庫快照集](revert-a-database-to-a-database-snapshot.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [資料庫快照集 &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
