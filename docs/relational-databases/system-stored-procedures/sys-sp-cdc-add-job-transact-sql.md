---
title: sys.sp_cdc_add_job (TRANSACT-SQL) |Microsoft 文件
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
- sp_cdc_add_job_TSQL
- sys.sp_cdc_add_job
- sys.sp_cdc_add_job_TSQL
- sp_cdc_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_add_job
ms.assetid: c4458738-ed25-40a6-8294-a26ca5a05bd9
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7c42d2150a148f1a288c1fa447f4bb1d9020fe09
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysspcdcaddjob-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立目前資料庫中的異動資料擷取清除或擷取作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_add_job [ @job_type = ] 'job_type'  
    [ , [ @start_job = ] start_job ]   
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ , [ @threshold ] = 'delete_threshold' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@job_type=** ] **'***job_type***'**  
 要加入的作業類型。 *job_type*是**nvarchar （20)** 不能是 NULL。 有效輸入如下： **'capture'** 和 **'cleanup'**。  
  
 [  **@start_job=** ] *start_job*  
 旗標，指出作業是否應該在加入之後立即啟動。 *start_job*是**元**預設值是 1。  
  
 [ **@maxtrans** ] = *max_trans*  
 每個掃描循環中要處理的交易數目上限。 *max_trans*是**int**預設值為 500。 如果已指定，該值必須是正整數。  
  
 *max_trans*只適用於擷取作業。  
  
 [ **@maxscans** ] **= * * * max_scans*  
 要執行以便從記錄中擷取所有資料列的掃描循環數目上限。 *max_scans*是**int**預設值是 10。  
  
 *max_scan*只適用於擷取作業。  
  
 [ **@continuous** ] **= * * * 連續*  
 指出擷取作業是連續執行 (1)，還是僅執行一次 (0)。 *連續*是**元**預設值是 1。  
  
 當*連續*= 1， [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)工作掃描記錄並且最多處理 (*max_trans* \* *max_scans*)交易。 然後它會等候中指定的秒數*polling_interval*再開始下一個記錄檔掃描。  
  
 當*連續*= 0， **sp_cdc_scan**作業最多會執行*max_scans*掃描的記錄檔中，最多處理*max_trans*交易而且在每次掃描，然後結束。  
  
 *連續*只適用於擷取作業。  
  
 [ **@pollinginterval** ] **= * * * polling_interval*  
 記錄掃描循環之間的秒數。 *polling_interval*是**bigint**預設值是 5。  
  
 *polling_interval*只適用於擷取作業時*連續*設為 1。 若已指定，這個值不可能是負值，而且不可能超過 24 小時。 若已指定 0 值，記錄檔掃描之間不會有等待時間。  
  
 [ **@retention** ] **= * * * 保留*  
 變更資料列要保留在變更資料表中的分鐘數。 *保留*是**bigint**預設值為 4320 （72 小時）。 最大值為 52494800 (100 年)。 如果已指定，該值必須是正整數。  
  
 *保留*只適用於清除作業。  
  
 [  **@threshold =** ] **'***delete_threshold***'**  
 可以使用單一清除陳述式來刪除的最大刪除項目數。 *delete_threshold*是**bigint**預設值為 5000。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 當資料庫中的第一份資料表啟用異動資料擷取時，系統就會使用預設值來建立清除作業。 當資料庫中的第一份資料表啟用異動資料擷取，而且該資料庫不存在任何交易式發行集時，系統就會使用預設值來建立擷取作業。 當交易式發行集存在時，交易式記錄讀取器就會用於驅動擷取機制，而且不需要也不允許使用個別的擷取作業。  
  
 由於系統預設會建立清除和擷取作業，因此只有在作業已經明確卸除而且必須重新建立時，這個預存程序才是必要項目。  
  
 作業的名稱是**cdc。***< 資料庫名稱 >***_cleanup**或**cdc。***< 資料庫名稱 >***_capture**，其中 *< 資料庫名稱 >* 是目前資料庫的名稱。 如果已經存在具有相同名稱的作業，名稱會附加以句號 (**。**) 後面的唯一識別碼，例如： **cdc。AdventureWorks_capture。A1ACBDED-13FC-428C-8302-10100EF74F52**。  
  
 若要檢視清除或擷取作業的目前組態，請使用[sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)。 若要變更作業的組態，請使用[sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-capture-job"></a>A. 建立擷取作業  
 下列範例會建立一個擷取作業。 這則範例會假設現有的清除作業已明確卸除而且必須重新建立。 系統會使用預設值來建立作業。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>B. 建立清除作業  
 下列範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中建立清除作業。 參數 `@start_job` 設定為 0 而且 `@retention` 設定為 5760 分鐘 (96 小時)。 這則範例會假設現有的清除作業已明確卸除而且必須重新建立。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>另請參閱  
 [dbo.cdc_jobs &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
