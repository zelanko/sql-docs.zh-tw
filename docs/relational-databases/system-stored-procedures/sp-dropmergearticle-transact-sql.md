---
description: sp_dropmergearticle (Transact-SQL)
title: sp_dropmergearticle (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7c91fe7b1cc57630565fae398fc8cbc798df314a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536509"
---
# <a name="sp_dropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @publication = ] 'publication'` 這是要卸載發行項的發行集名稱。 *發行*集是 **sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 這是要從指定的發行集卸載的發行項名稱。 *文章*是 **sysname**，沒有預設值。 如果是 **all**，指定之合併式發行集內的所有現有發行項都會被移除。 *即使是***全部**發行項，還是必須從發行項分開卸載發行集。  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否在未連接到散發者的情況下執行此預存程式。 *ignore_distributor* 是 **bit**，預設值是 **0**。  
  
`[ @reserved = ] reserved` 保留供日後使用。 *reserved* 是 **Nvarchar (20) **，預設值是 Null。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot* 是 **bit**，預設值是 **0**。  
  
 **0** 指定合併發行項的變更不會使快照集失效。  
  
 **1** 表示合併發行項的變更可能會導致快照集無效，如果是這種情況，則值為 **1** 會提供要發生之新快照集的許可權。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 認可卸載發行項需要重新初始化現有的訂閱。 *force_reinit_subscription* 是 **bit**，預設值是 **0**。  
  
 **0** 指定卸載發行項並不會使訂閱重新初始化。  
  
 **1** 表示卸載發行項會使現有的訂閱重新初始化，並提供要進行的訂閱重新初始化的許可權。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 僅供內部使用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_dropmergearticle** 用於合併式複寫中。 如需卸載發行項的詳細資訊，請參閱 [在現有發行集中加入和](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)卸載發行項。  
  
 執行 **sp_dropmergearticle** 從發行集中卸載發行項，並不會從發行集資料庫中移除物件，也不會從訂閱資料庫中移除對應的物件。 必要的話，請利用 `DROP <object>` 來手動移除這些物件。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_dropmergearticle**。  
  
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
 [刪除文章](../../relational-databases/replication/publish/delete-an-article.md)   
 [在現有發行集中加入和卸除發行項](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
