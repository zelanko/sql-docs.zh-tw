---
title: sys.fn_cdc_map_time_to_lsn (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95ee3e6306b47f74d0787bf62e4bfe3ecd5e07c6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回記錄序號 (lsn) 值，從**start_lsn**中的資料行[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)系統資料表。 指定的時間。 您可以使用此函式，有系統地將日期時間範圍對應至異動資料擷取列舉函數所需的 LSN 架構範圍[cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)和[cdc.fn_cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)傳回該範圍內的資料變更。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>引數  
 **'**< relational_operator >**'** {小於比最大 | 較不超過最大或等於 | 最小大於 | 最小大於或等於}  
 用來識別中的不同 LSN 值內**cdc.lsn_time_mapping**資料表相關之**tran_end_time** ，可滿足此關聯性，相較於*tracking_time*值。  
  
 *relational_operator*是**nvarchar （30)**。  
  
 *tracking_time*  
 這是要比對的日期時間值。 *tracking_time*是**datetime**。  
  
## <a name="return-type"></a>傳回類型  
 **binary(10)**  
  
## <a name="remarks"></a>備註  
 若要了解如何**sys.fn_cdc_map_time_lsn**可用來將日期時間範圍對應至 LSN 範圍，請考慮下列案例。 假設某位取用者想要每天擷取變更資料。 也就是說，該取用者只需要指定當天的變更 (直到且包括午夜)。 此時間範圍的下限應該是直到但不包括前一天的午夜。 其上限應該是直到且包括指定當天的午夜。 下列範例會示範如何函式**sys.fn_cdc_map_time_to_lsn**可用於有系統地將這個時間架構範圍對應至異動資料擷取列舉函數傳回所有所需的 LSN 架構範圍該範圍內的變更。  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 關係運算子 '`smallest greater than`' 是用來限制前一天午夜之後所發生的變更。 如果多個項目含有不同 LSN 值的共用**tran_end_time**識別為下限值[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表，此函數會傳回的最小 LSN，如此可確保所有項目都包含在內。 為上限，關係運算子 '`largest less than or equal to`' 用來確保此範圍包括所有項目，包括以午夜做為一天其**tran_end_time**值。 如果多個項目含有不同 LSN 值的共用**tran_end_time**值識別為上限，此函式會傳回確保所有項目都包括在內的最大 LSN。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會使用`sys.fn_cdc_map_time_lsn`函式來判斷是否有任何資料列中的[cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表具有**tran_end_time**大於或等於午夜的值。 例如，這個查詢可用來判斷擷取處理序是否已經處理了直到前一天午夜所認可的變更，如此當天的變更資料擷取才能繼續進行。  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>另請參閱  
 [cdc.lsn_time_mapping &#40;Transact SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
