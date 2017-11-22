---
title: "sys.fn_hadr_distributed_ag_replica (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_hadr_distributed_ag_replica
- sys.fn_hadr_distributed_ag_replica_TSQL
- fn_hadr_distributed_ag_replica
- fn_hadr_distributed_ag_replica_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.fn_hadr_distributed_ag_replica
ms.assetid: a1e5f9cb-c350-4bb4-a04f-7394f6f25d62
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fe90c7a863b70dc2d40994a333e80d620640d1f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnhadrdistributedagreplica-transact-sql"></a>sys.fn_hadr_distributed_ag_replica (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  用來對應至本機可用性群組的分散式的可用性群組中的複本。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_hadr_distributed_ag_replica( lag_Id, replica_id )  
```  
  
## <a name="arguments"></a>引數  
 '*lag_Id*'  
 是分散式的可用性群組的識別碼。 *lag_Id*是型別**uniqueidentifier**。  
  
 '*replica_id*'  
 是分散式的可用性群組複本的識別碼。 *replica_id*是型別**uniqueidentifier**。  
  
## <a name="tables-returned"></a>傳回的資料表  
 傳回下列資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|本機可用性群組的唯一識別碼 (GUID)。|  
  
## <a name="examples"></a>範例  
  
### <a name="using-sysfnhadrdistributedagreplica"></a>使用 sys.fn_hadr_distributed_ag_replica  
 下列範例會傳回具有指定的分散式的可用性群組和複本相關聯的本機可用性群組識別碼的資料表。  
  
```  
DECLARE @lagId uniqueidentifier = '4A03D1A8-4AE6-B153-E7E9-ED22A546008D'  
DECLARE @replicaId uniqueidentifier = 'D5517513-04A8-FD82-14C6-E684EC913935'  
  
SELECT * FROM sys.fn_hadr_distributed_ag_replica(@lagId, @replicaId)  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [AlwaysOn 可用性群組功能 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/always-on-availability-groups-functions-transact-sql.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [分散式的可用性群組 &#40;AlwaysOn 可用性群組 &#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
