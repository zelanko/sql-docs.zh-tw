---
title: sys.fn_hadr_distributed_ag_database_replica (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_database_replica
- sys.fn_hadr_distributed_ag_database_replica_TSQL
- fn_hadr_distributed_ag_database_replica
- fn_hadr_distributed_ag_database_replica_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_hadr_distributed_ag_database_replica
ms.assetid: 0e6202a1-e872-4f53-99d7-c16b6f712efc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ff99c2b63ad3f104b5bae4f6378af2e4fe0575bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640322"
---
# <a name="sysfnhadrdistributedagdatabasereplica-transact-sql"></a>sys.fn_hadr_distributed_ag_database_replica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  用來對應至本機可用性群組中資料庫的分散式的可用性群組中的資料庫。  
   
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_hadr_distributed_ag_database_replica( lag_Id, database_id )  
```  
  
## <a name="arguments"></a>引數  
 '*lag_Id*'  
 是分散式的可用性群組的識別碼。 *lag_Id*是型別**uniqueidentifier**。  
  
 '*database_id*'  
 是分散式的可用性群組中識別碼。 *database_id*是型別**uniqueidentifier**。  
  
## <a name="tables-returned"></a>傳回的資料表  
 傳回下列資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**group_database_id**|**uniqueidentifier**|本機可用性群組中資料庫的識別碼。|  
  
## <a name="examples"></a>範例  
  
### <a name="using-sysfnhadrdistributedagdatabasereplica"></a>使用 sys.fn_hadr_distributed_ag_database_replica  
 下列範例會傳入分散式的可用性群組中的資料庫識別碼。 它會傳回本機可用性群組相關聯的資料庫識別碼的資料表。  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @databaseId uniqueidentifier = '3FFA882A-C4C3-5B9E-A203-8F44BD9659F7'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_database_replica(@lagId, @databaseId)  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Always On 可用性群組功能&#40;Transact SQL&#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [分散式可用性群組&#40;Always On 可用性群組&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
