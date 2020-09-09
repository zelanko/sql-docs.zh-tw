---
description: sp_showrowreplicainfo (Transact-SQL)
title: sp_showrowreplicainfo (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a46fd42c9caa69e808635fc9dcc5125403697a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543030"
---
# <a name="sp_showrowreplicainfo-transact-sql"></a>sp_showrowreplicainfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @ownername = ] 'ownername'` 這是資料表擁有者的名稱。 *ownername* 是 **sysname**，預設值是 Null。 如果資料庫包含多份同名資料表，但每一份都有不同的擁有者，便可以利用這個參數來區分資料表。  
  
`[ @tablename = ] 'tablename'` 這是包含傳回信息之資料列的資料表名稱。 *tablename* 是 **sysname**，預設值是 Null。  
  
`[ @rowguid = ] rowguid` 這是資料列的唯一識別碼。 *rowguid* 是 **uniqueidentifier**，沒有預設值。  
  
`[ @show = ] 'show'` 判斷要在結果集中傳回的資訊量。 *顯示* 為 **Nvarchar (20) ** ，預設值為兩者。 如果為數據 **列**，則只傳回資料列版本資訊。 如果是資料 **行**，則只會傳回資料行版本資訊。 如果 **同時**傳回，則會傳回資料列和資料行資訊。  
  
## <a name="result-sets-for-row-information"></a>資料列資訊的結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|建立資料列版本項目之主控資料庫的伺服器名稱。|  
|**db_name**|**sysname**|建立這個項目的資料庫名稱。|  
|**db_nickname**|**binary(6)**|建立這個項目的資料庫暱稱。|  
|**version**|**int**|項目的版本。|  
|**current_state**|**Nvarchar (9) **|傳回資料列目前狀態的相關資訊。<br /><br /> **y** 資料列資料表示資料列的目前狀態。<br /><br /> **n** 資料列資料不代表資料列的目前狀態。<br /><br /> **\<n/a>** -不適用。<br /><br /> **\<unknown>** -無法判斷目前的狀態。|  
|**rowversion_table**|**Nchar (17) **|指出資料列版本是否儲存在 [MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 資料表或 [MSmerge_tombstone](../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 資料表中。|  
|**評論**|**nvarchar(255)**|這個資料列版本項目的其他相關資訊。 這個欄位通常是空的。|  
  
## <a name="result-sets-for-column-information"></a>資料行資訊的結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**server_name**|**sysname**|建立資料行版本項目之主控資料庫的伺服器名稱。|  
|**db_name**|**sysname**|建立這個項目的資料庫名稱。|  
|**db_nickname**|**binary(6)**|建立這個項目的資料庫暱稱。|  
|**version**|**int**|項目的版本。|  
|**colname**|**sysname**|資料行版本項目所代表之發行項資料行的名稱。|  
|**評論**|**nvarchar(255)**|這個資料行版本項目的其他相關資訊。 這個欄位通常是空的。|  
  
## <a name="result-set-for-both"></a>這兩者的結果集  
 如果為 [*顯示*] 選擇**兩個**值，則會傳回資料列和資料行結果集。  
  
## <a name="remarks"></a>備註  
 **sp_showrowreplicainfo** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 **sp_showrowreplicainfo** 只能由發行集資料庫上 **db_owner** 固定資料庫角色的成員，或是發行集資料庫 (PAL) 之發行集存取清單的成員執行。  
  
## <a name="see-also"></a>另請參閱  
 [偵測及解決合併式複寫衝突](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
