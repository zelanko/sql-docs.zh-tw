---
title: sp_dropdynamicsnapshot_job & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 19b99c9dc43f34863df7b33b433dbf14e97826b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718106"
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用參數化的資料列篩選器來移除發行集的篩選資料快照集作業。 這個預存程序執行於發行集資料庫的發行者端。 刪除作業時，所有相關的資料會在從刪除[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md)系統資料表。  
  
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
 這是移除篩選之資料快照集作業的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 這是移除篩選之資料快照集作業的名稱。 *dynamic_snapshot_jobname*是 sysname，以及如果不提供的預設值給任何工作名稱與相關聯*dynamic_snapshot_jobid*。  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 這是移除篩選之資料快照集作業的識別碼。 *dynamic_snapshot_jobid*已**uniqueidentifier**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  只有*dynamic_snapshot_jobid*或是*dynamic_snapshot_jobname*可以指定。 如果值不會提供適用於*dynamic_snapshot_jobid*或是*dynamic_snapshot_jobname*，會移除所有發行集的動態快照集作業。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor*已**位元**，預設值是**0**。 這個參數可在不執行散發者清除工作的情況下，用來卸除動態快照集作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropdynamicsnapshot**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropdynamicsnapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_adddynamicsnapshot_job &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
