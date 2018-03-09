---
title: sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_backup_is_preferred_replica_TSQL
- sys.fn_hadr_backup_is_preferred_replica
- fn_hadr_backup_is_preferred_replica_TSQL
- fn_hadr_backup_is_preferred_replica
dev_langs:
- TSQL
helpviewer_keywords:
- backup on secondary replicas
- active secondary replicas [SQL Server], backup on secondary replicas
- sys.fn_hadr_backup_is_preferred_replica function
ms.assetid: 61b9be77-e2f6-4da1-b2ae-a62cbe226145
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 86dd2be162ab29587589bd4388387da7cf171f6e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysfnhadrbackupispreferredreplica--transact-sql"></a>sys.fn_hadr_backup_is_preferred_replica  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  用於判斷目前的複本是否為慣用的備份複本。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>引數  
 '*dbname*'  
 這是要備份的資料庫名稱。 *dbname*為 sysname 型別。  
  
## <a name="returns"></a>傳回值  
 如果目前執行個體上的資料庫為慣用複本，則傳回 1， 否則傳回 0。  
  
## <a name="remarks"></a>備註  
 在備份指令碼中使用這個函數，以判斷目前的資料庫是否在備份所慣用的複本上。 您可以在每一個可用性複本上執行指令碼。 每一個作業都會查看相同的資料，以判斷應該執行哪一個作業，如此一來，只有其中一個排程作業會實際進行到備份階段。 範例程式碼可能如下所示。  
  
```  
If sys.fn_hadr_backup_is_preferred_replica( @dbname ) <> 1   
BEGIN  
-- If this is not the preferred replica, exit (probably without error).  
END  
-- If this is the preferred replica, continue to do the backup.  
  
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-sysfnhadrbackupispreferredreplica"></a>A. 使用 sys.fn_hadr_backup_is_preferred_replica  
 如果目前資料庫是慣用的備份複本，下列範例會傳回 1。  
  
```  
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [設定可用性複本 &#40; 的備份SQL Server &#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組功能 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [建立可用性群組 &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [作用中次要： 在備份上的次要複本 &#40;Always On 可用性群組 &#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) [Always On 可用性群組目錄檢視 &#40;TRANSACT-SQL &#41;    ](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)  
  
  
