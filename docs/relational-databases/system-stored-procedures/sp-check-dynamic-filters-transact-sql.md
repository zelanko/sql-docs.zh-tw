---
title: "sp_check_dynamic_filters (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords: sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 096c6ff70b712b283191afeddbb7e9d9c6afd36a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示發行集之參數化資料列篩選器屬性的相關資訊，尤其是用來產生發行集篩選資料分割的函數，以及發行集是否適合使用預先計算的資料分割。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication** =] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是發行集是否使用預先計算的資料分割;其中**1**預先計算的資料分割可以使用，表示和**0**表示，無法使用。|  
|**has_dynamic_filters**|**bit**|是在發行集; 如果已定義至少一個參數化資料列篩選器其中**1**表示一或多個參數化資料列篩選器存在，及**0**表示沒有動態篩選。|  
|**dynamic_filters_function_list**|**nvarchar （500)**|用來篩選發行集中的發行項之函數清單，每個函數都用分號來分開。|  
|**validate_subscriber_info**|**nvarchar （500)**|用來篩選發行集中的發行項之函數清單，每個函數都用加號 (+) 來分開。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函式是否用於參數化資料列篩選器，其中**1**表示，此函式來進行動態篩選。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函式是否用於參數化資料列篩選器，其中**1**表示，此函式來進行動態篩選。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_check_dynamic_filters**用於合併式複寫中。  
  
 如果發行集已定義為使用預先計算的資料分割， **sp_check_dynamic_filters**會檢查是否有任何違規的預先計算資料分割的限制。 如果找到任何違反限制的情況，便會傳回錯誤。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 如果已將發行集定義為有參數化資料列篩選器，但找不到參數化資料列篩選器，便會傳回錯誤。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_check_dynamic_filters**。  
  
## <a name="see-also"></a>請參閱＜  
 [管理合併式發行集使用參數化篩選的資料分割](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
