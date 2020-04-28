---
title: sp_deletemergeconflictrow （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: stevestein
ms.author: sstein
ms.openlocfilehash: a315bc147cf86df40cf6fa216b8c45eeb1fcccca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68111963"
---
# <a name="sp_deletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從衝突資料表或[MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)資料表中刪除資料列。 這個預存程序在任何資料庫中儲存衝突資料表的電腦上執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_deletemergeconflictrow [ [ @conflict_table = ] 'conflict_table' ]  
    [ , [ @source_object = ] 'source_object' ]  
    { , [ @rowguid = ] 'rowguid'  
        , [ @origin_datasource = ] 'origin_datasource' ] }  
    [ , [ @drop_table_if_empty = ] 'drop_table_if_empty' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @conflict_table = ] 'conflict_table'`這是衝突資料表的名稱。 *conflict_table*是**sysname**，預設值是**%**。 如果*conflict_table*指定為 Null 或**%**，則會假設衝突是刪除衝突，而且會從[MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)資料表中刪除符合*rowguid*和*origin_datasource*和*source_object*的資料列。  
  
`[ @source_object = ] 'source_object'`這是來源資料表的名稱。 *source_object*是**Nvarchar （386）**，預設值是 Null。  
  
`[ @rowguid = ] 'rowguid'`這是刪除衝突的資料列識別碼。 *rowguid*是**uniqueidentifier**，沒有預設值。  
  
`[ @origin_datasource = ] 'origin_datasource'`這是衝突的來源。 *origin_datasource*為**Varchar （255）**，沒有預設值。  
  
`[ @drop_table_if_empty = ] 'drop_table_if_empty'`這是一個旗標，表示如果是空的，就會卸載*conflict_table* 。 *drop_table_if_empty*是**Varchar （10）**，預設值是 FALSE。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_deletemergeconflictrow**用於合併式複寫中。  
  
 [MSmerge_conflicts_info &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)資料表是系統資料表，而且即使是空的，也不會從資料庫中刪除。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_deletemergeconflictrow**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
