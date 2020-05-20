---
title: sp_dropdynamicsnapshot_job （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0c9f33c4f50f77ed8ded47b6d7f69a2476f49227
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830157"
---
# <a name="sp_dropdynamicsnapshot_job-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用參數化的資料列篩選器來移除發行集的篩選資料快照集作業。 這個預存程序執行於發行集資料庫的發行者端。 刪除作業時，會從[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系統資料表中刪除所有相關資料。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是要從中移除已篩選之資料快照集作業的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`這是要移除之已篩選資料快照集作業的名稱。 *dynamic_snapshot_jobname*是 sysname，如果未提供，則預設為與*dynamic_snapshot_jobid*相關聯的任何工作名稱。  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`這是要移除之已篩選資料快照集作業的識別碼。 *dynamic_snapshot_jobid*是**uniqueidentifier**，預設值是 Null。  
  
> [!IMPORTANT]  
>  只能指定*dynamic_snapshot_jobid*或*dynamic_snapshot_jobname* 。 如果未提供*dynamic_snapshot_jobid*或*dynamic_snapshot_jobname*的值，則會移除發行集的所有動態快照集作業。  
  
`[ @ignore_distributor = ] ignore_distributor`*ignore_distributor*是**bit**，預設值是**0**。 這個參數可在不執行散發者清除工作的情況下，用來卸除動態快照集作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropdynamicsnapshot**用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_dropdynamicsnapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_adddynamicsnapshot_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
