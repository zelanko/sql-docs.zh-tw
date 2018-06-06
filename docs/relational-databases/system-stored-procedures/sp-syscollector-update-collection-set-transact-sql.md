---
title: sp_syscollector_update_collection_set (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 62867f22c044a42c40499e0a1143557621931db8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spsyscollectorupdatecollectionset-transact-sql"></a>sp_syscollector_update_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用來修改使用者定義之收集組的屬性，或是用來重新命名使用者定義的收集組。  
  
> [!WARNING]  
>  如果設定為 Proxy 的 Windows 帳戶為非互動使用者或是尚未登入的互動使用者，則設定檔目錄不會存在，而且暫存目錄的建立將會失敗。 因此，如果您在網域控制站上使用 Proxy 帳戶，則必須指定已至少使用一次的互動帳戶，以確保設定檔目錄已經建立。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@collection_set_id =** ] *collection_set_id*  
 這是收集組的唯一本機識別碼。 *collection_set_id*是**int**而且必須具有值，如果*名稱*是 NULL。  
  
 [ **@name =** ] '*name*'  
 這是收集組的名稱。 *名稱*是**sysname**而且必須具有值，如果*collection_set_id*是 NULL。  
  
 [ **@new_name =** ] '*new_name*'  
 這是收集組的新名稱。 *new_name*是**sysname**，而且如果使用，不能是空字串。 *new_name*必須是唯一的。 如需目前的收集組名稱清單，請查詢 syscollector_collection_sets 系統檢視表。  
  
 [  **@target =** ] '*目標*'  
 保留供日後使用。  
  
 [ **@collection_mode =** ] *collection_mode*  
 這是要使用的資料收集類型。 *collection_mode*是**smallint** ，而且可以有下列值之一：  
  
 0 - 快取模式。 資料收集和上傳會依照不同的排程。 指定連續收集的快取模式。  
  
 1 - 非快取模式。 資料收集和上傳位於相同的排程上。 針對特定收集或快照集收集指定非快取模式。  
  
 如果從非快取模式變更為快取模式 (0)，您也必須指定*schedule_uid*或*schedule_name*。  
  
 [ **@days_until_expiration=** ] *days_until_expiration*  
 這是已收集的資料儲存在管理資料倉儲中的天數。 *days_until_expiration*是**smallint**。 *days_until_expiration*必須是 0 或正整數。  
  
 [ **@proxy_id =** ] *proxy_id*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶的唯一識別碼。 *proxy_id*是**int**。  
  
 [ **@proxy_name =** ] '*proxy_name*'  
 這是 Proxy 的名稱。 *proxy_name*是**sysname**而且可為 null。  
  
 [ **@schedule_uid** = ] '*schedule_uid*'  
 這是指向排程的 GUID。 *schedule_uid*是**uniqueidentifier**。  
  
 若要取得*schedule_uid*，查詢 sysschedules 系統資料表。  
  
 當*collection_mode*設為 0， *schedule_uid*或*schedule_name*必須指定。 當*collection_mode*設為 1， *schedule_uid*或*schedule_name*如果指定，會被忽略。  
  
 [  **@schedule_name =** ] '*schedule_name*'  
 這是排程的名稱。 *schedule_name*是**sysname**而且可為 null。 如果指定， *schedule_uid*必須是 NULL。 若要取得*schedule_name*，查詢 sysschedules 系統資料表。  
  
 [ **@logging_level =** ] *logging_level*  
 這是記錄層級。 *logging_level*是**smallint**具有下列值之一：  
  
 0 - 記錄執行資訊和追蹤的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 事件：  
  
-   開始/停止收集組  
  
-   開始/停止封裝  
  
-   錯誤資訊  
  
 1 - 層級 0 記錄和：  
  
-   執行統計資料  
  
-   持續執行的收集進度  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 的警告事件  
  
 2 - 層級 1 記錄和 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 的詳細事件資訊。  
  
 預設值為*logging_level*為 1。  
  
 [  **@description =** ] '*描述*'  
 這是收集組的描述。 *描述*是**nvarchar （4000)**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_syscollector_update_collection_set 必須在 msdb 系統資料庫的內容中執行。  
  
 任一*collection_set_id*或*名稱*必須有值，不能同時為 NULL。 若要取得這些值，請查詢 syscollector_collection_sets 系統檢視表。  
  
 如果收集組正在執行，您只能更新*schedule_uid*和*描述*。 若要停止此收集組，使用[sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 dc_admin 或 dc_operator (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。 雖然 dc_operator 可以執行此預存程序，但是這個角色的成員會受限於他們可以變更的屬性。 下列屬性只能由 dc_admin 變更：  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>範例  
  
### <a name="a-renaming-a-collection-set"></a>A. 重新命名收集組  
 下列範例會重新命名使用者定義的收集組。  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. 將收集模式從非快取變更為快取  
 下列範例會將收集模式從非快取模式變更為快取模式。 這項變更會要求您指定排程識別碼或排程名稱。  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>C. 變更其他收集組參數  
 下列範例會更新名為 "Simple collection set test 2" 之收集組的各個屬性。  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysjobschedules &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
