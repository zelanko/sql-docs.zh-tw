---
title: sp_dropmergearticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords:
- sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13f48722b940c26cda8b29258f16f641f74d15e9
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531890"
---
# <a name="spdropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從合併式發行集中移除發行項。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是要卸除發行項的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 是要從給定的發行集卸除的發行項的名稱。 *發行項*已**sysname**，沒有預設值。 如果**所有**，移除指定的合併式發行集的所有現有發行項。 即使*一文*是**所有**，發行集仍必須先卸除個別發行項。  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否要將此預存程序執行而不需要連線到散發者。 *ignore_distributor*已**位元**，預設值是**0**。  
  
`[ @reserved = ] reserved` 是保留供日後使用。 *保留*已**nvarchar(20)**，預設值是 NULL。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*已**位元**，預設值**0**。  
  
 **0**指定合併發行項的變更不會使快照集失效。  
  
 **1**表示合併發行項的變更可能使快照集失效，如果這種情況下，值為**1**提供將出現新的快照集的權限。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 認可卸除發行項需要重新初始化現有的訂用帳戶。 *force_reinit_subscription*已**位元**，預設值是**0**。  
  
 **0**指定卸除發行項不會不會使訂閱重新初始化。  
  
 **1**表示卸除發行項會使現有的訂閱重新初始化，並提供發生之訂閱重新初始化的權限。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergearticle**用於合併式複寫中。 如需有關卸除發行項的詳細資訊，請參閱 <<c0> [ 新增和卸除現有發行集中的發行項](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
 執行**sp_dropmergearticle**從發行集中卸除的發行項不會移除該物件從發行集資料庫或從訂閱資料庫對應的物件。 必要的話，請利用 `DROP <object>` 來手動移除這些物件。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropmergearticle**。  
  
## <a name="example"></a>範例  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [刪除發行項](../../relational-databases/replication/publish/delete-an-article.md)   
 [在現有發行集中加入和卸除發行項](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
