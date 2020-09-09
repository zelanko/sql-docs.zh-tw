---
description: sys.sp_cdc_scan (Transact-SQL)
title: sys. sp_cdc_scan (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e73993a2f5d1a9d8635a55cb476a56fb6914390
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551143"
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
`[ @maxtrans = ] max_trans` 每個掃描迴圈中要處理的最大交易數目。 *max_trans* 是 **int** ，預設值是500。  
  
`[ @maxscans = ] max_scans` 要從記錄檔中提取所有資料列時要執行的掃描迴圈數目上限。 *max_scans* 是 **int** ，預設值是10。  
  
`[ @continuous = ] continuous` 指出在執行單一掃描迴圈之後，預存程式是否應該結束 (0) 或連續執行、暫停 *polling_interval* 所指定的時間，然後再暫停掃描週期 (1) 。 *連續* 是 **Tinyint** ，預設值是0。  
  
`[ @pollinginterval = ] polling_interval` 記錄檔掃描迴圈之間的秒數。 *polling_interval* 是 **Bigint** ，預設值是0。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擷取作業正由異動資料擷取使用中，sys.sp_MScdc_capture_job 就會在內部呼叫 sys.sp_cdc_scan。 當異動資料擷取記錄掃描作業已經在使用中，或者資料庫已啟用異動複寫時，就無法明確執行此程序。 想要自訂自動設定擷取作業之行為的管理員應該使用這個預存程序。  
  
## <a name="permissions"></a>權限  
 需要 db_owner 固定資料庫角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [dbo. cdc_jobs &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
