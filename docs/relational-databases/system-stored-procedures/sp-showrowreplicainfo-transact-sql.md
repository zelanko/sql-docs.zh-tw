---
title: sp_showrowreplicainfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0d009b05fea2a2c587f97dc4b2416588932ad0bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447986"
---
# <a name="spshowrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示有關資料表中之資料列的資訊，用來作為合併式複寫的發行項。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_showrowreplicainfo [ [ @ownername = ] 'ownername' ]  
    [ , [ @tablename =] 'tablename' ]   
        , [ @rowguid =] rowguid   
    [ , [ @show = ] 'show' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @ownername = ] 'ownername'` 是資料表擁有者名稱。 *ownername*已**sysname**，預設值是 NULL。 如果資料庫包含多份同名資料表，但每一份都有不同的擁有者，便可以利用這個參數來區分資料表。  
  
`[ @tablename = ] 'tablename'` 是包含傳回的資訊的資料列名稱。 *tablename*已**sysname**，預設值是 NULL。  
  
`[ @rowguid = ] rowguid` 是資料列的唯一識別碼。 *rowguid*已**uniqueidentifier**，沒有預設值。  
  
`[ @show = ] 'show'` 決定要在結果集中傳回資料的量。 *顯示*已**nvarchar(20)** 兩者的預設值。 如果**資料列**，就會傳回資料列版本資訊。 如果**資料行**，就會傳回資料行版本資訊。 如果**兩者**、 資料列，並傳回資料行資訊。  
  
## <a name="result-sets-for-row-information"></a>資料列資訊的結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|建立資料列版本項目之主控資料庫的伺服器名稱。|  
|**db_name**|**sysname**|建立這個項目的資料庫名稱。|  
|**db_nickname**|**binary(6)**|建立這個項目的資料庫暱稱。|  
|**version**|**int**|項目的版本。|  
|**current_state**|**nvarchar(9)**|傳回資料列目前狀態的相關資訊。<br /><br /> **y** -資料列的資料代表資料列的目前狀態。<br /><br /> **n** -資料列的資料不代表資料列的目前狀態。<br /><br /> **\<n/a >** -不適用。<br /><br /> **\<不明 >** -無法判定目前的狀態。|  
|**rowversion_table**|**nchar(17)**|指出是否將資料列版本儲存在[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)資料表或[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)資料表。|  
|**comment**|**nvarchar(255)**|這個資料列版本項目的其他相關資訊。 這個欄位通常是空的。|  
  
## <a name="result-sets-for-column-information"></a>資料行資訊的結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|建立資料行版本項目之主控資料庫的伺服器名稱。|  
|**db_name**|**sysname**|建立這個項目的資料庫名稱。|  
|**db_nickname**|**binary(6)**|建立這個項目的資料庫暱稱。|  
|**version**|**int**|項目的版本。|  
|**colname**|**sysname**|資料行版本項目所代表之發行項資料行的名稱。|  
|**comment**|**nvarchar(255)**|這個資料行版本項目的其他相關資訊。 這個欄位通常是空的。|  
  
## <a name="result-set-for-both"></a>這兩者的結果集  
 如果該值**兩者**為選擇*顯示*，則會傳回資料列和資料行的結果集。  
  
## <a name="remarks"></a>備註  
 **sp_showrowreplicainfo**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 **sp_showrowreplicainfo**的成員，才可執行**db_owner**固定的資料庫角色，發行集資料庫，或發行集資料庫之發行集存取清單 (PAL) 的成員。  
  
## <a name="see-also"></a>另請參閱  
 [偵測及解決合併式複寫衝突](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
