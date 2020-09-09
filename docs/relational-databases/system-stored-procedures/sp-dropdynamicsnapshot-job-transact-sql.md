---
description: sp_dropdynamicsnapshot_job (Transact-SQL)
title: sp_dropdynamicsnapshot_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 932ca55e93c039c918302cb52026dd5051cbb551
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543460"
---
# <a name="sp_dropdynamicsnapshot_job-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  利用參數化的資料列篩選器來移除發行集的篩選資料快照集作業。 這個預存程序執行於發行集資料庫的發行者端。 刪除作業時，會從 [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) 系統資料表刪除所有相關資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是要移除已篩選資料快照集作業的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` 這是要移除之已篩選資料快照集作業的名稱。 *dynamic_snapshot_jobname*為 sysname，如果未提供，則預設為任何與 *dynamic_snapshot_jobid*相關聯的工作名稱。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` 這是要移除之已篩選資料快照集作業的識別碼。 *dynamic_snapshot_jobid*是 **uniqueidentifier**，預設值是 Null。  
  
> [!IMPORTANT]  
>  只能指定 *dynamic_snapshot_jobid*或 *dynamic_snapshot_jobname* 。 如果沒有為 *dynamic_snapshot_jobid*或 *dynamic_snapshot_jobname*提供值，則會移除發行集的所有動態快照集作業。  
  
`[ @ignore_distributor = ] ignore_distributor`*ignore_distributor*是**bit**，預設值是**0**。 這個參數可在不執行散發者清除工作的情況下，用來卸除動態快照集作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_dropdynamicsnapshot** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_dropdynamicsnapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_adddynamicsnapshot_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
