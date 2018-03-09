---
title: "sp_check_subset_filter (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3341c4f5fc6c637f74dabf913730e6c6e30dfcea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這用來檢查任何資料表的篩選子句，以判斷資料表的篩選子句是否有效。 這個預存程序會傳回所提供之篩選的相關資訊，其中包括篩選是否能夠搭配預先計算的資料分割來使用。 這個預存程序執行於發行集所在資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@filtered_table** =] **'***filtered_table***'**  
 這是篩選的資料表名稱。 *filtered_table*是**nvarchar （400)**，沒有預設值。  
  
 [  **@subset_filterclause**  =] **'***subset_filterclause***'**  
 這是正在測試的篩選子句。 *subset_filterclause*是**nvarchar （1000)**，沒有預設值。  
  
 [  **@has_dynamic_filters** =] *has_dynamic_filters*  
 這是指篩選子句是否為參數化資料列篩選器。 *has_dynamic_filters*是**元**，預設值是 NULL，這是輸出參數。 傳回值的**1**當篩選子句是參數化資料列篩選器。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是發行集是否使用預先計算的資料分割;其中**1**預先計算的資料分割可以使用，表示和**0**表示，無法使用。|  
|**has_dynamic_filters**|**bit**|提供的篩選子句包含至少一個參數化資料列篩選器。其中**1**表示會使用參數化資料列篩選，和**0**表示，不會使用這類函式。|  
|**dynamic_filters_function_list**|**nvarchar （500)**|篩選子句中動態篩選發行項的函數清單，其中每個函數都以分號加以區隔。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函數是否用於篩選子句中，其中**1**表示存在於此函式。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函數是否用於篩選子句中，其中**1**表示存在於此函式。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_check_subset_filter**用於合併式複寫中。  
  
 **sp_check_subset_filter**可以針對任何資料表執行，即使資料表不發行。 在定義篩選的發行項之前，您可以使用這個預存程序，先驗證篩選子句。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_check_subset_filter**。  
  
## <a name="see-also"></a>請參閱＜  
 [最佳化參數化的篩選效能與預先計算資料分割](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
