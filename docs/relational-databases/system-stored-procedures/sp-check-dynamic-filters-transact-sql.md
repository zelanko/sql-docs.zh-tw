---
title: sp_check_dynamic_filters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
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
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc961ef5f3c22d8da7a97f53b387cd1d0c09c679
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533386"
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
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是如果發行集符合使用預先計算的資料分割;其中**1**表示可以使用資料分割，預先計算並**0**表示，無法使用。|  
|**has_dynamic_filters**|**bit**|會在發行集中; 是否已定義至少一個參數化資料列篩選器其中**1**意謂著一或多個參數化資料列篩選器存在，以及**0**表示沒有動態篩選。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|用來篩選發行集中的發行項之函數清單，每個函數都用分號來分開。|  
|**validate_subscriber_info**|**nvarchar(500)**|用來篩選發行集中的發行項之函數清單，每個函數都用加號 (+) 來分開。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函式是否用於參數化資料列篩選器，其中**1**表示此函式，來進行動態篩選。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函式是否用於參數化資料列篩選器，其中**1**表示此函式，來進行動態篩選。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_check_dynamic_filters**用於合併式複寫中。  
  
 如果發行集已定義為使用預先計算的資料分割**sp_check_dynamic_filters**會檢查是否有任何違規，預先計算資料分割的限制。 如果找到任何違反限制的情況，便會傳回錯誤。 如需詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 如果已將發行集定義為有參數化資料列篩選器，但找不到參數化資料列篩選器，便會傳回錯誤。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_check_dynamic_filters**。  
  
## <a name="see-also"></a>另請參閱  
 [合併式發行集使用參數化篩選管理資料分割](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
