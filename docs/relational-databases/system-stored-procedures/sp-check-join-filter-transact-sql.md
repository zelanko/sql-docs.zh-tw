---
title: sp_check_join_filter （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28589be83c62f705457e990b328be98e88905568
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771266"
---
# <a name="sp_check_join_filter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  用來驗證兩個資料表之間的聯結篩選，以判斷聯結篩選子句是否有效。 這個預存程序也會傳回有關所提供之聯結篩選的資訊，包括它是否能夠搭配使用給定資料表之預先計算的資料分割。 這個預存程序執行於發行集的發行者端。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>引數  
`[ @filtered_table = ] 'filtered_table'`這是已篩選資料表的名稱。 *filtered_table*是**Nvarchar （400）**，沒有預設值。  
  
`[ @join_table = ] 'join_table'`這是聯結至*filtered_table*之資料表的名稱。 *join_table*是**Nvarchar （400）**，沒有預設值。  
  
`[ @join_filterclause = ] 'join_filterclause'`這是正在測試的聯結篩選子句。 *join_filterclause*是**Nvarchar （1000）**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|如果發行集符合預先計算資料分割的資格，則為，其中**1**表示可以使用 precomupted 的資料分割，而**0**表示無法使用它們。|  
|**has_dynamic_filters**|**bit**|這是指提供的篩選子句是否至少包含一個參數化篩選函數;其中**1**表示使用參數化篩選函數， **0**表示不使用這類函數。|  
|**dynamic_filters_function_list**|**Nvarchar （500）**|篩選子句中定義發行項參數化篩選的函數清單，其中每個函數皆以分號加以分隔。|  
|**uses_host_name**|**bit**|如果在篩選子句中使用[HOST_NAME （）](../../t-sql/functions/host-name-transact-sql.md)函數，其中**1**表示此函數存在。|  
|**uses_suser_sname**|**bit**|如果在篩選子句中使用[SUSER_SNAME （）](../../t-sql/functions/suser-sname-transact-sql.md)函數，其中**1**表示此函數存在。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_check_join_filter**用於合併式複寫中。  
  
 即使尚未發行，也可以針對任何相關的資料表執行**sp_check_join_filter** 。 在定義兩個發行項之間的聯結篩選之前，您可以使用這個預存程序，先驗證聯結篩選子句。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_check_join_filter**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
