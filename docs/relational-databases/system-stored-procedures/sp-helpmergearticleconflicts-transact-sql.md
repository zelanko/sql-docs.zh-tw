---
description: sp_helpmergearticleconflicts (Transact-SQL)
title: sp_helpmergearticleconflicts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 49ca95bebb40c13bf2044bef58e161bb2bacfdd2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535181"
---
# <a name="sp_helpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回發行集中發生衝突的發行項。 這個預存程序執行於發行集資料庫的發行者端，或合併訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是合併式發行集的名稱。*發行* 集是 **sysname**，預設值是 **%** ，它會傳回資料庫中有衝突的所有發行項。  
  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。*publisher* 是 **sysname**，預設值是 Null。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行者資料庫的名稱。*publisher_db* 是 **sysname**，預設值是 Null。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**文章**|**sysname**|發行項的名稱。|  
|**source_owner**|**sysname**|來源物件的擁有者。|  
|**source_object**|**Nvarchar (386) **|來源物件的名稱。|  
|**conflict_table**|**nvarchar(258)**|儲存插入或更新衝突的資料表名稱。|  
|**guidcolname**|**sysname**|來源物件的 RowGuidCol 名稱。|  
|**centralized_conflicts**|**int**|是否將衝突記錄儲存在給定的發行者。|  
  
 如果發行項只有刪除衝突，且沒有 **conflict_table** 資料列，則結果集中的 **CONFLICT_TABLE** 名稱為 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpmergearticleconflicts** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色和 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_helpmergearticleconflicts**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
