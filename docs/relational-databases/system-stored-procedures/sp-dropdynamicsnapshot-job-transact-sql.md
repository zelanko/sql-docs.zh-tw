---
title: sp_dropdynamicsnapshot_job (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6a0e47c9fc680895cacc0c2e68585a354391b98f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用參數化的資料列篩選器來移除發行集的篩選資料快照集作業。 這個預存程序執行於發行集資料庫的發行者端。 刪除作業時，所有相關資料會刪除從[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系統資料表。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 這是移除篩選之資料快照集作業的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 這是移除篩選之資料快照集作業的名稱。 *dynamic_snapshot_jobname*是 sysname，如果不提供的預設值給任何工作名稱是與*dynamic_snapshot_jobid*。  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 這是移除篩選之資料快照集作業的識別碼。 *dynamic_snapshot_jobid*是**uniqueidentifier**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  只有*dynamic_snapshot_jobid*或*dynamic_snapshot_jobname*可以指定。 如果值未提供任何*dynamic_snapshot_jobid*或*dynamic_snapshot_jobname*，就會移除所有發行集的動態快照集作業。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor*是**元**，預設值是**0**。 這個參數可在不執行散發者清除工作的情況下，用來卸除動態快照集作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropdynamicsnapshot**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropdynamicsnapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_adddynamicsnapshot_job &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
