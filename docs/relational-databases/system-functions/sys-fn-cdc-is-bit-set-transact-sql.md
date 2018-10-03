---
title: sys.fn_cdc_is_bit_set (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_cdc_is_bit_set
- sys.fn_cdc_is_bit_set_TSQL
- sys.fn_cdc_is_bit_set
- fn_cdc_is_bit_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_cdc_is_bit_set
- fn_cdc_is_bit_set
ms.assetid: 792fe7cf-b3b8-4f25-8329-78d63f0e6921
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0796f25396d4c5303fb0de1762f6f04a18035fa9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705626"
---
# <a name="sysfncdcisbitset-transact-sql"></a>sys.fn_cdc_is_bit_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  透過檢查擷取資料行的序數位置是否設定於提供的位元遮罩內，指出該擷取資料行是否已經更新。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_cdc_is_bit_set ( position , update_mask )  
```  
  
## <a name="arguments"></a>引數  
 *position*  
 這是遮罩中要檢查的序數位置。 *位置*已**int**。  
  
 *update_mask*  
 這是識別更新資料行的遮罩。 *update_mask*已**varbinary(128)**。  
  
## <a name="return-type"></a>傳回類型  
 **bit**  
  
## <a name="remarks"></a>備註  
 這個函數通常會當做變更資料查詢的一部分使用，以便指出資料行是否已經變更。 在此案例中，此函式[sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)用於在查詢之前取得必要的資料行序數。 **sys.fn_cdc_is_bit_set**接著會套用到每個會傳回，提供傳回的結果集的一部分的資料行特定資訊的變更資料列。  
  
 我們建議使用此函式，而不函式[sys.fn_cdc_has_column_changed](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)判斷傳回的結果集的所有資料列是否已變更資料行時。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會使用 `sys.fn_cdc_is_bit_set` 搭配預先計算的資料行序數和 `cdc.fn_cdc_get_all_changes_HR_Department` 的值做為要呼叫的引數，在 `IsGroupNmUpdated` 查詢函數所產生的結果集前面加上 '`__$update_mask`' 資料行。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @GroupNm_ordinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @GroupNm_ordinal = sys.fn_cdc_get_column_ordinal('HR_Department','GroupName');  
  
SELECT sys.fn_cdc_is_bit_set(@GroupNm_ordinal,__$update_mask) as 'IsGroupNmUpdated', *  
FROM cdc.fn_cdc_get_all_changes_HR_Department( @from_lsn, @to_lsn, 'all')  
WHERE __$operation = 4;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [異動資料擷取函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [sys.fn_cdc_get_column_ordinal &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)   
 [sys.fn_cdc_has_column_changed &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
