---
title: sys.databases sp_cdc_get_captured_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0bc087c6e55418a501459076a1f3f7862112a056
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82808198"
---
# <a name="syssp_cdc_get_captured_columns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對指定擷取執行個體所追蹤的擷取來源資料行，傳回異動資料擷取中繼資料資訊。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都無法異動資料擷取。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>引數  
 [ @capture_instance =] '*capture_instance*'  
 這是與來源資料表相關聯之擷取執行個體的名稱。 *capture_instance*是**sysname** ，不能是 Null。  
  
 若要報告資料表的 capture 實例，請執行[sys.databases sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)預存程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|來源資料表結構描述的名稱。|  
|source_table|**sysname**|來源資料表的名稱。|  
|capture_instance|**sysname**|擷取執行個體的名稱。|  
|column_name|**sysname**|擷取來源資料行的名稱。|  
|column_id|**int**|來源資料表中資料行的識別碼。|  
|column_ordinal|**int**|來源資料表中資料行的位置。|  
|data_type|**sysname**|資料行資料類型。|  
|character_maximum_length|**int**|以字元為基礎之資料行的最大字元長度，否則為 NULL。|  
|numeric_precision|**tinyint**|如果是以數值為基礎，就是資料行的有效位數，否則為 NULL。|  
|numeric_precision_radix|**smallint**|如果是以數值為基礎，就是資料行的有效位數基數，否則為 NULL。|  
|numeric_scale|**int**|如果是以數值為基礎，就是資料行的小數位數，否則為 NULL。|  
|datetime_precision|**smallint**|如果是以日期時間為基礎，就是資料行的有效位數，否則為 NULL。|  
  
## <a name="remarks"></a>備註  
 使用 sys.databases 來取得有關查詢 capture 實例查詢函式（ [cdc. fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)或 cdc）所傳回之已捕捉資料行的資料行資訊。 [fn_cdc_get_net_changes_<](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)capture_instance>sp_cdc_get_captured_columns。 在擷取執行個體的存留期間，資料行名稱、識別碼和位置會維持不變。 當追蹤資料表中基礎來源資料行的資料類型變更時，只有資料行資料類型會變更。 在來源資料表中加入或卸除的資料行對於現有擷取執行個體的擷取資料行不會造成任何影響。  
  
 使用[sp_cdc_get_ddl_history sys.databases](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)來取得已套用至來源資料表之資料定義語言（ddl）語句的相關資訊。 任何修改追蹤來源資料行之結構的 DDL 變更都會在結果集中傳回。  
  
## <a name="permissions"></a>權限  
 需要 db_owner 固定資料庫角色中的成員資格。 若為所有其他使用者，則需要來源資料表中所有擷取資料行的 SELECT 權限，而且如果定義了擷取執行個體的控制角色，便需要該資料庫角色的成員資格。 當呼叫端沒有檢視來源資料的權限時，此函數會傳回錯誤 22981 (物件不存在或存取遭到拒絕)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `HumanResources_Employee` 擷取執行個體中擷取資料行的相關資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
