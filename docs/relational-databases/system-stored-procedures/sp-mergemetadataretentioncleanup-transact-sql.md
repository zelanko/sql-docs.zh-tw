---
title: sp_mergemetadataretentioncleanup (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1797200ce5369f49035f1a950d606e34e584edc2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526220"
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行手動清除中繼資料[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)， [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)， [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)， [MSmerge_past_partition_對應](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)，並[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)系統資料表。 這個預存程序執行於拓撲中的每個發行者和訂閱者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>引數  
`[ @num_genhistory_rows = ] num_genhistory_rows OUTPUT` 傳回的資料列清除的數目[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)資料表。 *num_genhistory_rows*已**int**，預設值是**0**。  
  
`[ @num_contents_rows = ] num_contents_rows OUTPUT` 傳回的資料列清除的數目[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)資料表。 *num_contents_rows*已**int**，預設值是**0**。  
  
`[ @num_tombstone_rows = ] num_tombstone_rows OUTPUT` 傳回的資料列清除的數目[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)資料表。 *num_tombstone_rows*已**int**，預設值是**0**。  
  
`[ @aggressive_cleanup_only = ] aggressive_cleanup_only` 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果有多個發行集資料庫上，而且任何一個發行集都會使用無限期的發行保留期限，執行**sp_mergemetadataretentioncleanup**就不會清除合併式複寫變更追蹤資料庫的中繼資料。 因此，在使用無限期的發行期限時，一定要特別小心。 若要判斷發行集是否有無限的保留期限，請執行[sp_helpmergepublication &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)結果中的任何發行集設定的值在 「 發行者 」 和附註**0** for**保留**。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**固定資料庫角色或發行集存取清單中的使用者可以執行已發行的資料庫**sp_mergemetadataretentioncleanup**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
