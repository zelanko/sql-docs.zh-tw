---
title: core.sp_create_snapshot (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_create_snapshot
- sp_create_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- management data warehouse, data collector stored procedures
- data collector [SQL Server], stored procedures
- core.sp_create_snapshot stored procedure
- sp_create_snapshot
ms.assetid: ff297bda-0ee2-4fda-91c8-7000377775e3
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33ba9d69763a9d07cc9907aef60397b6c5b37eee
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="corespcreatesnapshot-transact-sql"></a>core.sp_create_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在管理資料倉儲的 core.snapshots 檢視表中，插入資料列。 每次上傳封裝開始將資料上傳至管理資料倉儲時，就會呼叫這個程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
core.sp_create_snapshot [ @collection_set_uid = ] 'collection_set_uid'  
    , [ @collector_type_uid = ] 'collector_type_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @log_id = ] log_id  
    , [ @snapshot_id = ] snapshot_id OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [ @collection_set_uid = ] '*collection_set_uid*'  
 收集組的 GUID。 *collection_set_uid*是**uniqueidentifier** ，沒有預設值。 若要取得 GUID，請查詢 msdb 資料庫中的 dbo.syscollector_collection_sets 檢視表。  
  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 收集器類型的 GUID。 *collector_type_uid 是否*是**uniqueidentifier** ，沒有預設值。 若要取得 GUID，請查詢 msdb 資料庫中的 dbo.syscollector_collector_types 檢視表。  
  
 [ @machine_name=] '*machine_name*'  
 收集組所在的伺服器名稱。 *machine_name*是**sysname**，沒有預設值。  
  
 [ @named_instance=] '*named_instance*'  
 收集組的執行個體名稱。 *named_instance*是**sysname**，沒有預設值。  
  
 [ @log_id = ] *log_id*  
 在收集資料的伺服器上對應至收集組事件記錄檔的唯一識別碼。 *g _ i d*是**bigint** ，沒有預設值。 若要取得的值*log_id*，請查詢 msdb 資料庫中的 dbo.syscollector_execution_log 檢視。  
  
 [ @snapshot_id = ] *snapshot_id*  
 插入 core.snapshots 檢視資料列的唯一識別碼。 *snapshot_id*是**int**而且會當做 OUTPUT 傳回。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 每次上傳封裝開始將資料上傳至管理資料倉儲時，資料收集器執行階段元件就會呼叫 core.sp_create_snapshot。  
  
 這個程序會查看：  
  
-   collection_set_uid 是否符合 core.source_info_internal 資料表中的現有項目。  
  
-   collector_type_uid 是否符合 core.supported_collector_types 檢視表中的現有項目。  
  
 如果上述其中一項檢查失敗，此程序就會失敗並傳回錯誤。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**mdw_writer** （具有 EXECUTE 權限） 固定的資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會針對「磁碟使用量」收集組建立快照集、將它加入到管理資料倉儲中，並傳回快照集識別碼。 此範例中會使用預設執行個體。  
  
```  
USE <management_data_warehouse>;  
DECLARE @snapshot_id int;  
EXEC core.sp_create_snapshot   
    @collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
    @collector_type_uid = '302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @machine_name = '<computername>',  
    @named_instance = 'MSSQLSERVER',  
    @log_id = 11, -- ID of the log for the collection set  
    @snapshot_id = @snapshot_id OUTPUT;  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理資料倉儲](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
