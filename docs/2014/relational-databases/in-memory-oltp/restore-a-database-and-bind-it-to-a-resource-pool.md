---
title: 還原資料庫並將其繫結至資源集區 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cac1e775d5cccaccca90b03104de4132e651284e
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535210"
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>還原資料庫並將其繫結至資源集區
  即使您有足夠的記憶體來還原含有記憶體最佳化資料表的資料庫，建議您還是依照最佳做法，將資料庫繫結至具名資源集區。 因為資料庫必須先存在，然後您才能將它繫結至集區，而且還原資料庫是一項具有多重步驟的程序。 本主題會逐步引導您完成該程序。  
  
##  <a name="restore-with-norecovery"></a>使用 NORECOVERY 還原  
 當您還原資料庫時，NORECOVERY 會建立資料庫並還原磁碟映像，但不會耗用任何記憶體。  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
##  <a name="create-the-resource-pool"></a>建立資源集區  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會建立名為 Pool_IMOLTP 的資源集區，而且有 50% 的記憶體可供它使用。  建立集區之後，資源管理員會重新設定為包含 Pool_IMOLTP。  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bind-the-database-and-resource-pool"></a>繫結資料庫和資源集區  
 您可以使用系統函數 `sp_xtp_bind_db_resource_pool` ，將資料庫繫結至資源集區。 此函數會採用兩個參數：資料庫名稱，後面接著資源集區名稱。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會定義 IMOLTP_DB 資料庫與 Pool_IMOLTP 資源集區的繫結。 在您完成下一個步驟之前，此繫結不會生效。  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
##  <a name="restore-with-recovery"></a>使用 RECOVERY 還原  
 當您使用 RECOVERY 來還原資料庫時，資料庫就會重新上線並且還原所有資料。  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
##  <a name="monitor-the-resource-pool-performance"></a>監視資源集區效能  
 一旦將資料庫繫結至具名資源集區並使用復原功能還原之後，請監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Resource Pool Stats 物件。 如需詳細資訊，請參閱＜ [SQL Server、Resource Pool Stats 物件](../performance-monitor/sql-server-resource-pool-stats-object.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [將包含記憶體最佳化資料表的資料庫繫結至資源集區](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [SQL Server、Resource Pool Stats 物件](../performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)  
  
  
