---
title: CHANGE_TRACKING_MIN_VALID_VERSION (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CLEANUP_VERSION
- CHANGE_TRACKING_CLEANUP_VERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGE_TRACKING_MIN_VALID_VERSION
- change tracking [SQL Server], CHANGE_TRACKING_MIN_VALID_VERSION
ms.assetid: 5a43d23f-adcf-4c0b-95ad-07cee03c1f9d
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2858c61ea7316b1bafa06a1181b31e97b0724b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766636"
---
# <a name="changetrackingminvalidversion-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回的最小版本，適用於取得變更追蹤資訊從指定的資料表，當您使用用戶端[CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)函式。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>引數  
 *table_object_id*  
 這是資料表的物件識別碼。 *table_object_id*已**int**。  
  
## <a name="return-type"></a>傳回類型  
 **bigint**  
  
## <a name="remarks"></a>備註  
 若要驗證的值使用此函式*last_sync_version* CHANGETABLE 參數。 如果*last_sync_version*小於會報告此函式，從稍後呼叫 CHANGETABLE 所傳回的結果可能不是有效的值。  
  
 CHANGE_TRACKING_MIN_VALID_VERSION 會使用下列資訊判斷傳回值：  
  
-   針對變更追蹤啟用資料表時。  
  
-   執行背景清除工作來移除早於您為資料庫指定之保留期的變更追蹤資訊時。  
  
-   資料表遭到截斷時。 這樣會移除與資料表相關聯的所有變更追蹤資訊。  
  
 如果下列任一條件成立，函數會傳回 NULL：  
  
-   資料庫未啟用變更追蹤。  
  
-   指定的資料表物件識別碼不適用於目前的資料庫。  
  
-   物件識別碼指定的資料表權限不足。  
  
## <a name="examples"></a>範例  
 下列範例會判斷指定的版本是否為有效版本。 此範例會取得 `dbo.Employees` 資料表的最小有效版本，然後將該版本與 `@last_sync_version` 變數的值相比較。 如果 `@last_sync_version` 的值小於 `@min_valid_version` 的值，已變更資料列的清單將無效。  
  
> [!NOTE]  
>  您通常會從您儲存同步資料所使用之最後一個版本號碼所在的資料表或其他位置取得值。  
  
```  
-- The tracked change is tagged with the specified context   
DECLARE @min_valid_version bigint, @last_sync_version bigint;  
  
SET @min_valid_version =   
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('dbo.Employees'));  
  
SET @last_sync_version = 11  
IF (@last_sync_version < @min_valid_version)  
-- Error � do not obtain changes  
ELSE  
-- Obtain changes using CHANGETABLE(CHANGES ...)  
```  
  
## <a name="see-also"></a>另請參閱  
 [變更追蹤函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
