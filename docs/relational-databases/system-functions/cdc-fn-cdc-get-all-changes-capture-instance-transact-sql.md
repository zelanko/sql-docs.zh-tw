---
title: "cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
dev_langs: TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
caps.latest.revision: "31"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 111fab345e7679745e72ebe874dabcca3bed62fb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="cdcfncdcgetallchangesltcaptureinstancegt--transact-sql"></a>cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對在指定之記錄序號 (LSN) 範圍內套用至來源資料表的每個變更，各傳回一個資料列。 如果來源資料列在間隔期間具有多個變更，就會在傳回的結果集中表示每個變更。 除了傳回變更資料以外，四個中繼資料資料行會提供讓您將變更套用至其他資料來源所需的資訊。 資料列篩選選項會管理結果集中傳回的中繼資料資料行以及資料列內容。 當您指定了 'all' 資料列篩選選項時，每個變更都剛好具有一個資料列來識別變更。 當您指定了 'all update old' 選項時，更新作業會表示成兩個資料列：其中一個資料列包含更新之前擷取資料行的值，而另一個資料列則包含更新之後擷取資料行的值。  
  
 當來源資料表啟用異動資料擷取時，就會建立此列舉函數。 函式名稱衍生自並採用格式**cdc.fn_cdc_get_all_changes_***capture_instance*其中*capture_instance*是擷取指定的值當來源資料表啟用異動資料擷取執行個體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>引數  
 *from_lsn*  
 LSN 值，代表要包含在結果集之 LSN 範圍的低端點。 *from_lsn*是**binary （10)**。  
  
 只有當資料列中[cdc。 &#91;capture_instance &#93; _CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)變更資料表中的值**__ $start_lsn**大於或等於*from_lsn*隨附於結果集。  
  
 *to_lsn*  
 LSN 值，代表要包含在結果集之 LSN 範圍的高端點。 *to_lsn*是**binary （10)**。  
  
 只有當資料列中[cdc。 &#91;capture_instance &#93; _CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)變更資料表中的值**__ $start_lsn**小於或等於*from_lsn*或等於*to_lsn*會包含在結果集中。  
  
 <row_filter_option> ::= { all | all update old }  
 管理結果集中傳回之中繼資料資料行以及資料列內容的選項。  
  
 可以是下列其中一個選項：  
  
 all  
 傳回指定之 LSN 範圍內的所有變更。 若為由於更新作業所造成的變更，這個選項就只會傳回包含套用更新之後之新值的資料列。  
  
 all update old  
 傳回指定之 LSN 範圍內的所有變更。 若為由於更新作業所造成的變更，這個選項就會同時傳回包含更新之前之資料行值的資料列以及包含更新之後之資料行值的資料列。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|說明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|與變更相關聯的認可 LSN，其中保留變更的認可順序。 在相同交易中認可的變更都會共用相同的認可 LSN 值。|  
|**__$seqval**|**binary(10)**|用於排序交易內資料列變更的序列值。|  
|**__$operation**|**int**|識別將變更資料的資料列套用至目標資料來源所需的資料操作語言 (DML) 作業。 可以是下列其中一項：<br /><br /> 1 = 刪除<br /><br /> 2 = 插入<br /><br /> 3 = 更新 (擷取的是更新作業之前的資料行值)。 只有在您指定了 'all update old' 資料列篩選選項時，這個值才適用。<br /><br /> 4 = 更新 (擷取的是更新作業之後的資料行值)。|  
|**__$update_mask**|**varbinary(128)**|位元遮罩，其中含有對應至針對擷取執行個體所識別之每個擷取資料行的位元。 這個值會將所有定義設定為 1 的位元**__ $operation** = 1 或 2。 當**__ $operation** = 3 或 4，只有變更的資料行的對應位元才會設定為 1。|  
|**\<擷取來源資料表資料行 >**|變化|這個函數所傳回的其餘資料行都是建立擷取執行個體時所識別的擷取資料行。 如果擷取的資料行清單中沒有指定任何資料行，就會傳回來源資料表中的所有資料行。|  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色。 若為所有其他使用者，則需要來源資料表中所有擷取資料行的 SELECT 權限，而且如果定義了擷取執行個體的控制角色，便需要該資料庫角色的成員資格。 如果呼叫端沒有檢視來源資料的權限，此函數會傳回錯誤 229 (「 SELECT 權限遭拒的物件 'fn_cdc_get_all_changes_...' 沒有，資料庫 '\<資料庫名稱 >'，結構描述 'cdc'。")。  
  
## <a name="remarks"></a>備註  
 如果指定的 LSN 範圍不在擷取執行個體的變更追蹤時間表內，此函數會傳回錯誤 208 (「提供給程序或函數 cdc.fn_cdc_get_all_changes 的引數數量不足」)。  
  
 資料類型的資料行**映像**，**文字**，和**ntext**一定會指派 NULL 值時**__ $operation** = 1 或**__ $作業**= 3。 資料類型的資料行**varbinary （max)**， **varchar （max)**，或**nvarchar （max)**都會指派 NULL 值時**__ $operation** = 3除非在更新期間變更的資料行。 當**__ $operation** = 1，這些資料行會在刪除時指定其值。 包含在擷取執行個體中的計算資料行，一律使用 NULL 值。  
  
## <a name="examples"></a>範例  
 數個[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]範本可用，顯示如何使用異動資料擷取查詢函數。 這些範本位於**檢視**功能表[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 如需詳細資訊，請參閱[範本總管](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)。  
  
 此範例示範 `Enumerate All Changes for Valid Range Template`。 它會使用此函式`cdc.fn_cdc_get_all_changes_HR_Department`報告所有目前可用的變更，針對擷取執行個體`HR_Department`，定義來源資料表中的 HumanResources.Department[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫。  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance& &#62;&#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
