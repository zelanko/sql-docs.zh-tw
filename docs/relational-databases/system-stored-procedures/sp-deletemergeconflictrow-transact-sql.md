---
title: sp_deletemergeconflictrow (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_deletemergeconflictrow
- sp_deletemergeconflictrow_TSQL
helpviewer_keywords:
- sp_deletemergeconflictrow
ms.assetid: 64cf1186-28b8-4cd9-88f1-a7808a9c8d60
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fc1152ee4893991a207936c1a08dccc988fbde5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670563"
---
# <a name="spdeletemergeconflictrow-transact-sql"></a>sp_deletemergeconflictrow (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從衝突資料表刪除資料列或[MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)資料表。 這個預存程序在任何資料庫中儲存衝突資料表的電腦上執行。  
  
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
 [  **@conflict_table=**] **'***conflict_table***'**  
 這是衝突資料表的名稱。 *conflict_table*已**sysname**，預設值是**%**。 如果*conflict_table*指定為 NULL 或**%**，就會假設衝突是刪除衝突，而且資料列比對*rowguid*並*origin_datasource*並*source_object*從刪除[MSmerge_conflicts_info &#40;-&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)資料表。  
  
 [  **@source_object=**] **'***source_object***'**  
 這是來源資料表的名稱。 *source_object*已**nvarchar(386)**，預設值是 NULL。  
  
 [  **@rowguid =**] **'***rowguid***'**  
 這是刪除衝突的資料列識別碼。 *rowguid*已**uniqueidentifier**，沒有預設值。  
  
 [  **@origin_datasource=**] **'***origin_datasource***'**  
 這是衝突的來源。 *origin_datasource*已**varchar(255)**，沒有預設值。  
  
 [  **@drop_table_if_empty=**] **'***drop_table_if_empty***'**  
 是旗標，表示*conflict_table*是要卸除，如果是空的。 *drop_table_if_empty*已**varchar(10)**，預設值是 FALSE。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_deletemergeconflictrow**用於合併式複寫中。  
  
 [MSmerge_conflicts_info &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msmerge-conflicts-info-transact-sql.md)資料表是系統資料表而且不會刪除從資料庫中，即使是空的。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_deletemergeconflictrow**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
