---
title: sys.databases sp_cdc_get_ddl_history （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
author: rothja
ms.author: jroth
ms.openlocfilehash: bb4622b36901afc7ff04eacbfe840a9adda5b214
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083729"
---
# <a name="syssp_cdc_get_ddl_history-transact-sql"></a>sys.sp_cdc_get_ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回自從針對指定的擷取執行個體啟用變更資料擷取以來，與該擷取執行個體相關聯的資料定義語言 (DDL) 變更記錄。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>引數  
 [ @capture_instance = ]'*capture_instance*'  
 這是與來源資料表相關聯之擷取執行個體的名稱。 *capture_instance*是**sysname** ，不能是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|來源資料表結構描述的名稱。|  
|source_table|**sysname**|來源資料表的名稱。|  
|capture_instance|**sysname**|擷取執行個體的名稱。|  
|required_column_update|**bit**|指出 DDL 變更要求更改變更資料表中的資料行，以便反映對來源資料行所做的資料類型變更。|  
|ddl_command|**nvarchar(max)**|套用至來源資料表的 DDL 陳述式。|  
|ddl_lsn|**binary(10)**|與 DDL 變更相關聯的記錄序號 (LSN)。|  
|ddl_time|**datetime**|與 DDL 變更相關聯的時間。|  
  
## <a name="remarks"></a>備註  
 變更來源資料表資料行結構之來源資料表的 DDL 修改（例如，加入或卸載資料行，或變更現有資料行的資料類型）會在[cdc. ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)資料表中進行維護。 您可以使用這個預存程序來報告這些變更。 cdc.ddl_history 中的項目是在擷取處理序讀取記錄中的 DDL 交易時完成的。  
  
## <a name="permissions"></a>權限  
 需要 db_owner 固定資料庫角色中的成員資格，才能針對資料庫中的所有擷取執行個體傳回資料列。 若為所有其他使用者，則需要來源資料表中所有擷取資料行的 SELECT 權限，而且如果定義了擷取執行個體的控制角色，便需要該資料庫角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會將資料行加入至 `HumanResources.Employee` 來源資料表，然後執行 `sys.sp_cdc_get_ddl_history` 預存程序來報告 DDL 變更 (套用至與 `HumanResources_Employee` 擷取執行個體相關聯的來源資料表)。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
