---
title: "刪除發行項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "發行項 [SQL Server 複寫], 卸除"
  - "sp_droparticle"
  - "sp_dropmergearticle"
  - "刪除發行項"
  - "移除發行項"
  - "卸除發行項"
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 刪除發行項
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中刪除發行項。 卸除發行項，以及是否要卸除發行項需要新的快照集或重新初始化訂閱條件的相關資訊，請參閱 [新增和卸除現有的發行集的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
 **本主題內容**  
  
-   **若要刪除發行項，請使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來以程式設計的方式刪除發行項。 使用哪些預存程序要依發行項所屬的發行集類型而定。  
  
#### 從快照式或交易式發行集中刪除發行項  
  
1.  執行 [sp_droparticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) 若要刪除發行項，由指定 **@article**, ，從發行集中，由指定 **@publication**。 指定的值為 **1** 的 **@force_invalidate_snapshot**。  
  
2.  (選擇性) 若要從資料庫完全移除發行的物件，請在發行集資料庫的發行者上執行 `DROP <objectname>` 命令。  
  
#### 從合併式發行集中刪除發行項  
  
1.  執行 [sp_dropmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 若要刪除發行項，由指定 **@article**, ，從發行集中，由指定 **@publication**。 如有必要，指定其值為 **1** 的 **@force_invalidate_snapshot** 且值為 **1** 的 **@force_reinit_subscription**。  
  
2.  (選擇性) 若要從資料庫完全移除發行的物件，請在發行集資料庫的發行者上執行 `DROP <objectname>` 命令。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會刪除交易式發行集中的發行項。 因為這項變更會使現有的快照集的值 **1** 指定 **@force_invalidate_snapshot** 參數。  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 下列範例會刪除合併式發行集中的兩個發行項。 因為這些變更會使現有的快照集的值 **1** 指定 **@force_invalidate_snapshot** 參數。  
  
```  
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
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 您可以使用 Replication Management Objects (RMO) 以程式設計的方式刪除發行項。 用於刪除發行項的 RMO 類別，將取決於發行項所屬的發行集類型而定。  
  
#### 刪除屬於快照式或交易式發行集的發行項  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransArticle> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  設定步驟 1 中的連接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認文件存在。 如果這個屬性的值為 **false**，則表示步驟 3 中的發行項屬性定義錯誤或是此發行項不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 方法。  
  
7.  關閉所有連接。  
  
#### 刪除屬於合併式發行集的發行項  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeArticle> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 屬性。  
  
4.  設定步驟 1 中的連接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
5.  檢查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 屬性，確認文件存在。 如果這個屬性的值為 **false**，則表示步驟 3 中的發行項屬性定義錯誤或是此發行項不存在。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 方法。  
  
7.  關閉所有連接。  
  
## 另請參閱  
 [在現有發行集中加入和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  