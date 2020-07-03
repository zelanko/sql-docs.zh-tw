---
title: sys.databases sp_cdc_scan （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 558a2fd9ff62baa3448609eb42e5f31883fbac53
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891058"
---
# <a name="syssp_cdc_scan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  執行異動資料擷取記錄掃描作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>引數  
`[ @maxtrans = ] max_trans`每個掃描迴圈中要處理的交易數目上限。 *max_trans*是**int** ，預設值是500。  
  
`[ @maxscans = ] max_scans`要執行的掃描迴圈數目上限，以便從記錄檔中解壓縮所有資料列。 *max_scans*是**int** ，預設值是10。  
  
`[ @continuous = ] continuous`指出預存程式是否應在執行單一掃描迴圈（0）或連續執行時結束，並在暫停掃描週期（1）之前，暫停*polling_interval*所指定的時間。 *連續*是**Tinyint** ，預設值是0。  
  
`[ @pollinginterval = ] polling_interval`記錄掃描迴圈之間的秒數。 *polling_interval*是**Bigint** ，預設值是0。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擷取作業正由異動資料擷取使用中，sys.sp_MScdc_capture_job 就會在內部呼叫 sys.sp_cdc_scan。 當異動資料擷取記錄掃描作業已經在使用中，或者資料庫已啟用異動複寫時，就無法明確執行此程序。 想要自訂自動設定擷取作業之行為的管理員應該使用這個預存程序。  
  
## <a name="permissions"></a>權限  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [dbo. cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
