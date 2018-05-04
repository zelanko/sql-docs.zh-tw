---
title: sp_showrowreplicainfo (TRANSACT-SQL) |Microsoft 文件
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
- sp_showrowreplicainfo_TSQL
- sp_showrowreplicainfo
helpviewer_keywords:
- sp_showrowreplicainfo
ms.assetid: 6a9dbc1a-e1e1-40c4-97cb-8164a2288f76
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 80e50ddc736ee63c893fdd3b6a785503c2f17c7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
 [ **@ownername**=] **'***ownername***'**  
 這是資料表擁有者的名稱。 *ownername*是**sysname**，預設值是 NULL。 如果資料庫包含多份同名資料表，但每一份都有不同的擁有者，便可以利用這個參數來區分資料表。  
  
 [  **@tablename =**] **'***tablename***'**  
 這是包含傳回資訊之資料列的資料表名稱。 *tablename*是**sysname**，預設值是 NULL。  
  
 [  **@rowguid =**] *rowguid*  
 這是資料列的唯一識別碼。 *rowguid*是**uniqueidentifier**，沒有預設值。  
  
 [ **@show**=] **'***顯示***'**  
 決定結果集所傳回的資訊量。 *顯示*是**nvarchar （20)** 兩者的預設值。 如果**列**，就會傳回資料列版本資訊。 如果**資料行**，就會傳回資料行版本資訊。 如果**兩者**，資料列，並傳回資料行資訊。  
  
## <a name="result-sets-for-row-information"></a>資料列資訊的結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|建立資料列版本項目之主控資料庫的伺服器名稱。|  
|**db_name**|**sysname**|建立這個項目的資料庫名稱。|  
|**db_nickname**|**binary(6)**|建立這個項目的資料庫暱稱。|  
|**version**|**int**|項目的版本。|  
|**current_state**|**nvarchar(9)**|傳回資料列目前狀態的相關資訊。<br /><br /> **y** -資料列代表的資料列的目前狀態。<br /><br /> **n** -資料列的資料不是資料列的目前狀態。<br /><br /> **\<n/a >** -不適用。<br /><br /> **\<未知 >** -無法判斷目前的狀態。|  
|**rowversion_table**|**nchar(17)**|指出是否要將資料列版本儲存在[MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)資料表或[MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)資料表。|  
|**註解**|**nvarchar(255)**|這個資料列版本項目的其他相關資訊。 這個欄位通常是空的。|  
  
## <a name="result-sets-for-column-information"></a>資料行資訊的結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|建立資料行版本項目之主控資料庫的伺服器名稱。|  
|**db_name**|**sysname**|建立這個項目的資料庫名稱。|  
|**db_nickname**|**binary(6)**|建立這個項目的資料庫暱稱。|  
|**version**|**int**|項目的版本。|  
|**colname**|**sysname**|資料行版本項目所代表之發行項資料行的名稱。|  
|**註解**|**nvarchar(255)**|這個資料行版本項目的其他相關資訊。 這個欄位通常是空的。|  
  
## <a name="result-set-for-both"></a>這兩者的結果集  
 如果值**兩者**會選擇*顯示*，則會傳回資料列和資料行的結果集。  
  
## <a name="remarks"></a>備註  
 **sp_showrowreplicainfo**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 **sp_showrowreplicainfo**的成員，才可執行**db_owner**發行集資料庫之發行集存取清單 (PAL) 的成員或發行集資料庫上的固定的資料庫角色。  
  
## <a name="see-also"></a>另請參閱  
 [偵測及解決合併式複寫衝突](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
