---
title: sp_check_subset_filter （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3c1510260a5b381b91a399984121834ca4ce30b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771309"
---
# <a name="sp_check_subset_filter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  這用來檢查任何資料表的篩選子句，以判斷資料表的篩選子句是否有效。 這個預存程序會傳回所提供之篩選的相關資訊，其中包括篩選是否能夠搭配預先計算的資料分割來使用。 這個預存程序執行於發行集所在資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @filtered_table = ] 'filtered_table'`這是已篩選資料表的名稱。 *filtered_table*是**Nvarchar （400）**，沒有預設值。  
  
`[ @subset_filterclause = ] 'subset_filterclause'`這是要測試的篩選子句。 *subset_filterclause*是**Nvarchar （1000）**，沒有預設值。  
  
`[ @has_dynamic_filters = ] has_dynamic_filters`這是指篩選子句是否為參數化資料列篩選器。 *has_dynamic_filters*是**bit**，預設值是 Null，而則是輸出參數。 當篩選子句是參數化資料列篩選器時，傳回**1**的值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|如果發行集符合使用預先計算資料分割的資格，則為，其中**1**表示可以使用預先計算的資料分割，而**0**表示無法使用它們。|  
|**has_dynamic_filters**|**bit**|這是指提供的篩選子句是否至少包含一個參數化資料列篩選器;其中**1**表示使用參數化資料列篩選器， **0**表示不使用這類函數。|  
|**dynamic_filters_function_list**|**Nvarchar （500）**|篩選子句中動態篩選發行項的函數清單，其中每個函數都以分號加以區隔。|  
|**uses_host_name**|**bit**|如果在篩選子句中使用[HOST_NAME （）](../../t-sql/functions/host-name-transact-sql.md)函數，其中**1**表示此函數存在。|  
|**uses_suser_sname**|**bit**|如果在篩選子句中使用[SUSER_SNAME （）](../../t-sql/functions/suser-sname-transact-sql.md)函數，其中**1**表示此函數存在。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_check_subset_filter**用於合併式複寫中。  
  
 即使資料表尚未發行，也可以針對任何資料表執行**sp_check_subset_filter** 。 在定義篩選的發行項之前，您可以使用這個預存程序，先驗證篩選子句。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_check_subset_filter**。  
  
## <a name="see-also"></a>另請參閱  
 [使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
