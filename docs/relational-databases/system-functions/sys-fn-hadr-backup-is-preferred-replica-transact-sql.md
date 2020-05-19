---
title: sys.databases fn_hadr_backup_is_preferred_replica （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 287acb7986b3e518260f82278f8079391932ab6f
ms.sourcegitcommit: bfb5e79586fd08d8e48e9df0e9c76d1f6c2004e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82262140"
---
# <a name="sysfn_hadr_backup_is_preferred_replica--transact-sql"></a>sys.databases fn_hadr_backup_is_preferred_replica （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  用於判斷目前的複本是否為慣用的備份複本。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_hadr_backup_is_preferred_replica ( 'dbname' )  
```  
  
## <a name="arguments"></a>引數  
 '*dbname*'  
 這是要備份的資料庫名稱。 *dbname*的類型為 sysname。  
  
## <a name="returns"></a>傳回  
 如果目前實例上的資料庫是在慣用複本上，則傳回資料類型**bool**：1，否則為0。  
  
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
  
### <a name="a-using-sysfn_hadr_backup_is_preferred_replica"></a>A. 使用 sys.fn_hadr_backup_is_preferred_replica  
 如果目前資料庫是慣用的備份複本，下列範例會傳回 1。  
  
```  
SELECT sys.fn_hadr_backup_is_preferred_replica ('TestDB');  
GO  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [設定可用性複本的備份 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組函數 &#40;Transact-sql&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-sql&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-sql&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 使用[中次要：在次要複本上備份 &#40;Always On 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) [Always On 可用性群組目錄 Views &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)      
  
  
