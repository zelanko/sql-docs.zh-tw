---
title: sys.databases sp_cdc_add_job （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68737e96c3c2c90592b1cccf807675ae5518ee4d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891195"
---
# <a name="syssp_cdc_add_job-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @job_type = ] 'job\_type'`要加入的作業類型。 *job_type*是**Nvarchar （20）** ，而且不可以是 Null。 有效的輸入為「 **capture** 」和「**清除**」。  
  
`[ @start_job = ] start_job`旗標，指出工作是否應該在新增之後立即啟動。 *start_job*是**bit** ，預設值是1。  
  
`[ @maxtrans ] = max_trans`每個掃描迴圈中要處理的交易數目上限。 *max_trans*是**int** ，預設值是500。 如果已指定，該值必須是正整數。  
  
 *max_trans*只對 capture 作業有效。  
  
`[ @maxscans ] = max\_scans_`要執行的掃描迴圈數目上限，以便從記錄檔中解壓縮所有資料列。 *max_scans*是**int** ，預設值是10。  
  
 *max_scan*只對 capture 作業有效。  
  
`[ @continuous ] = continuous_`指出 capture 作業是連續執行（1），還是只執行一次（0）。 [*連續*] 是**bit** ，預設值是1。  
  
 當*連續*= 1 時， [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)作業會掃描記錄，並處理最多（*max_trans* \* *max_scans*）的交易。 然後，它會先等候*polling_interval*中指定的秒數，再開始下一次的記錄檔掃描。  
  
 當*連續*= 0 時， **sp_cdc_scan**作業會執行到記錄檔的*max_scans*掃描，處理每次掃描期間的*max_trans*交易，然後結束。  
  
 「*連續*」只對「捕獲」作業有效。  
  
`[ @pollinginterval ] = polling\_interval_`記錄掃描迴圈之間的秒數。 *polling_interval*是**Bigint** ，預設值是5。  
  
 *polling_interval*只有在*連續*設定為1時，才會對 capture 作業有效。 若已指定，這個值不可能是負值，而且不可能超過 24 小時。 若已指定 0 值，記錄檔掃描之間不會有等待時間。  
  
`[ @retention ] = retention_`變更資料列要保留在變更資料表中的分鐘數。 *保留期*為**Bigint** ，預設值為4320（72小時）。 最大值為 52494800 (100 年)。 如果已指定，該值必須是正整數。  
  
 *保留*僅適用于清除作業。  
  
`[ @threshold = ] 'delete\_threshold'`可以使用單一清除語句來刪除的最大刪除專案數。 *delete_threshold*是**Bigint** ，預設值是5000。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 當資料庫中的第一份資料表啟用異動資料擷取時，系統就會使用預設值來建立清除作業。 當資料庫中的第一份資料表啟用異動資料擷取，而且該資料庫不存在任何交易式發行集時，系統就會使用預設值來建立擷取作業。 當交易式發行集存在時，交易式記錄讀取器就會用於驅動擷取機制，而且不需要也不允許使用個別的擷取作業。  
  
 由於系統預設會建立清除和擷取作業，因此只有在作業已經明確卸除而且必須重新建立時，這個預存程序才是必要項目。  
  
 作業的名稱是**cdc。** _\<database\_name\>_** \_ 清除**或**cdc。** _\<database\_name\>_** \_ capture**，其中 *<database_name>* 是目前資料庫的名稱。 如果已經存在相同名稱的作業，名稱會附加一個句點（**.**），後面接著一個唯一識別碼，例如： **cdc。AdventureWorks_capture。A1ACBDED-13FC-428C-8302-10100EF74F52**。  
  
 若要查看清除或 capture 作業的目前設定，請使用[sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)。 若要變更作業的設定，請使用[sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 需要**db_owner**固定資料庫角色中的成員資格。  
  
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
 [dbo. cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sp_cdc_enable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
