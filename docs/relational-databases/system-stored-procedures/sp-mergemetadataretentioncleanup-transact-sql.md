---
title: sp_mergemetadataretentioncleanup (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergemetadataretentioncleanup
- sp_mergemetadataretentioncleanup_TSQL
helpviewer_keywords:
- sp_mergemetadataretentioncleanup
ms.assetid: 4e8d6343-2a38-421d-a3f3-c37d437a0f88
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f0666a5fabbed29b6a9c29a67fb1dce5a20cc50d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spmergemetadataretentioncleanup-transact-sql"></a>sp_mergemetadataretentioncleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  執行中的中繼資料的手動清除[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)， [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)， [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)， [MSmerge_past_partition_對應](../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)，和[MSmerge_current_partition_mappings](../../relational-databases/system-tables/msmerge-current-partition-mappings.md)系統資料表。 這個預存程序執行於拓撲中的每個發行者和訂閱者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergemetadataretentioncleanup [ [ @num_genhistory_rows = ] num_genhistory_rows OUTPUT ]  
    [ , [ @num_contents_rows = ] num_contents_rows OUTPUT ]   
    [ , [ @num_tombstone_rows = ] num_tombstone_rows OUTPUT ]   
    [ , [ @aggressive_cleanup_only = ] aggressive_cleanup_only ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@num_genhistory_rows=** ] *num_genhistory_rows*輸出  
 傳回清除的資料列數目[MSmerge_genhistory](../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)資料表。 *num_genhistory_rows*是**int**，預設值是**0**。  
  
 [  **@num_contents_rows=** ] *num_contents_rows*輸出  
 傳回清除的資料列數目[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)資料表。 *num_contents_rows*是**int**，預設值是**0**。  
  
 [  **@num_tombstone_rows=** ] *num_tombstone_rows*輸出  
 傳回清除的資料列數目[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)資料表。 *num_tombstone_rows*是**int**，預設值是**0**。  
  
 [  **@aggressive_cleanup_only=** ] *aggressive_cleanup_only*  
 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果有多個發行集的資料庫上，而任何一個發行集都會使用無限期的發行保留期限，執行**sp_mergemetadataretentioncleanup**並不會清除合併式複寫變更追蹤資料庫的中繼資料。 因此，在使用無限期的發行期限時，一定要特別小心。 若要判斷發行集是否有無限保留週期，請執行[sp_helpmergepublication &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)結果中的任何發行集設定其值為 「 發行者 」 和附註**0**如**保留**。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**固定資料庫角色或發行集存取清單中的使用者，已發行的資料庫能夠執行**sp_mergemetadataretentioncleanup**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
