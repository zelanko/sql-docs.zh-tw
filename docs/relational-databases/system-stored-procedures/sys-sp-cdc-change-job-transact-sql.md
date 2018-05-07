---
title: sys.sp_cdc_change_job (TRANSACT-SQL) |Microsoft 文件
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
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ca1b4bf87be7b0b102bb139aad650dfa16e5c3a1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysspcdcchangejob-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改目前資料庫中異動資料擷取清除或擷取作業的組態。 若要檢視作業的目前組態，請查詢[dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)資料表，或使用[sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>引數  
 [  **@job_type=** ] **'***job_type***'**  
 要修改的作業類型。 *job_type*是**nvarchar （20)** 預設值是 'capture'。 有效的輸入是 'capture' 和 'cleanup'。  
  
 [ **@maxtrans** ] **= * * * max_trans*  
 每個掃描循環中要處理的交易數目上限。 *max_trans*是**int** ，預設值是 NULL，代表此參數沒有異動。 如果已指定，該值必須是正整數。  
  
 *max_trans*只適用於擷取作業。  
  
 [ **@maxscans** ] **= * * * max_scans*  
 要執行以便從記錄中擷取所有資料列的掃描循環數目上限。 *max_scans*是**int** ，預設值是 NULL，代表此參數沒有異動。  
  
 *max_scan*只適用於擷取作業。  
  
 [ **@continuous** ] **= * * * 連續*  
 指出擷取作業是連續執行 (1)，還是僅執行一次 (0)。 *連續*是**元**，預設值是 NULL，代表此參數沒有異動。  
  
 當*連續*= 1， [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)工作掃描記錄並且最多處理 (*max_trans* \* *max_scans*)交易。 然後它會等候中指定的秒數*polling_interval*再開始下一個記錄檔掃描。  
  
 當*連續*= 0， **sp_cdc_scan**作業最多會執行*max_scans*掃描的記錄檔中，最多處理*max_trans*交易而且在每次掃描，然後結束。  
  
 如果**@continuous**從 1 變更為 0， **@pollinginterval**自動設定為 0。 值，指定**@pollinginterval**以外 0 會被忽略。  
  
 如果**@continuous**省略或明確設定為 NULL 和**@pollinginterval**明確設定的值大於 0， **@continuous**會自動設定為 1。  
  
 *連續*只適用於擷取作業。  
  
 [ **@pollinginterval** ] **= * * * polling_interval*  
 記錄掃描循環之間的秒數。 *polling_interval*是**bigint** ，預設值是 NULL，代表此參數沒有異動。  
  
 *polling_interval*只適用於擷取作業時*連續*設為 1。  
  
 [ **@retention** ] **= * * * 保留*  
 變更資料列要保留在變更資料表中的分鐘數。 *保留*是**bigint** ，預設值是 NULL，代表此參數沒有異動。 最大值為 52494800 (100 年)。 如果已指定，該值必須是正整數。  
  
 *保留*只適用於清除作業。  
  
 [  **@threshold=** ] **'***刪除閾值***'**  
 可以使用單一清除陳述式來刪除的最大刪除項目數。 *刪除閾值*是**bigint** ，預設值是 NULL，代表此參數沒有異動。 *刪除閾值*只適用於清除作業。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 如果省略參數，則相關聯的值在[dbo.cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)資料表不會更新。 明確設定為 NULL 的參數會被視為省略的參數。  
  
 指定對作業類型無效的參數將導致此陳述式失敗。  
  
 變更工作未生效之前工作已停止使用[sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md)並重新啟動使用[sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-a-capture-job"></a>A. 變更擷取作業  
 下列範例會更新`@job_type`， `@maxscans`，和`@maxtrans`中擷取作業參數`AdventureWorks2012`資料庫。 擷取作業其他有效的參數 (`@continuous` 和 `@pollinginterval`) 被省略，而且其值不會進行修改。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>B. 變更清除作業  
 下列範例會在 `AdventureWorks2012` 資料庫中更新清除作業。 所有有效參數，此作業類型，除了**@threshold**，所指定。 值**@threshold**則不會修改。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [dbo.cdc_jobs &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
