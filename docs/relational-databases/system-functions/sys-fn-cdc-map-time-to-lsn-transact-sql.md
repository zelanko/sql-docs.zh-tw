---
title: sys.databases fn_cdc_map_time_to_lsn （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bba5095587b8ddbb4c06d3334ad60e16cb2f5e35
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395730"
---
# <a name="sysfn_cdc_map_time_to_lsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對指定的時間，從[cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)系統資料表中的**start_lsn**資料行傳回記錄序號（LSN）值。 您可以使用此函式，有系統地將日期時間範圍對應至變更資料捕獲列舉函數 cdc 所需的 LSN 型範圍[fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)和[cdc。 fn_cdc_get_net_changes_](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)<capture_instance>傳回該範圍內的資料變更。  
  
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
 **'**<relational_operator>**'** {大於最大小於或等於最小大於或等於} 的最 \| \| 小值 \|  
 在與*tracking_time*值相較之下，用來識別**cdc. lsn_time_mapping**資料表內的相異 LSN 值，其中包含符合關聯性的**tran_end_time** 。  
  
 *relational_operator*是**Nvarchar （30）**。  
  
 *tracking_time*  
 這是要比對的日期時間值。 *tracking_time*為**datetime**。  
  
## <a name="return-type"></a>傳回類型  
 **binary(10)**  
  
## <a name="remarks"></a>備註  
 若要瞭解如何使用**fn_cdc_map_time_lsn sys.databases**將日期時間範圍對應至 lsn 範圍，請考慮下列案例。 假設某位取用者想要每天擷取變更資料。 也就是說，該取用者只需要指定當天的變更 (直到且包括午夜)。 此時間範圍的下限應該是直到但不包括前一天的午夜。 其上限應該是直到且包括指定當天的午夜。 下列範例示範如何使用**fn_cdc_map_time_to_lsn**的函式，將這個以時間為基礎的範圍，有系統地對應到變更資料捕獲列舉函數所需的 lsn 範圍，以傳回該範圍內的所有變更。  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 關係運算子 '`smallest greater than`' 是用來限制前一天午夜之後所發生的變更。 如果具有不同 LSN 值的多個專案共用[lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表中識別為下限的**tran_end_time**值，函數會傳回最小的 lsn，確保包含所有的專案。 若為上限，則會使用關聯式運算子 ' `largest less than or equal to` ' 來確保範圍包含一天中的所有專案，包括以午夜做為其**tran_end_time**值的時間。 如果具有不同 LSN 值的多個專案共用識別為上限的**tran_end_time**值，函數會傳回最大的 lsn，確保包含所有的專案。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例 `sys.fn_cdc_map_time_lsn` 會使用函數來判斷[cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)資料表中是否有任何資料列的**tran_end_time**值大於或等於午夜。 例如，這個查詢可用來判斷擷取處理序是否已經處理了直到前一天午夜所認可的變更，如此當天的變更資料擷取才能繼續進行。  
  
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
 [lsn_time_mapping &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [fn_cdc_map_lsn_to_time &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
