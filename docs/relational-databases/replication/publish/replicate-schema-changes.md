---
title: "複寫結構描述變更 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replication [SQL Server], schema changes"
  - "結構描述 [SQL Server 複寫], 複寫變更"
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# 複寫結構描述變更
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中複寫結構描述變更。  
  
 如果您想要針對發行的發行項進行以下的結構描述變更，這些變更預設會傳播到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要複寫結構描述變更，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   ALTER TABLE… DROP COLUMN 陳述式一定會複寫至訂閱包含要卸除之資料行的所有「訂閱者」，即使您停用結構描述變更的複寫也是如此。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 如果不想複寫發行集的結構描述變更，停用的結構描述變更複寫 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
#### 若要停用結構描述變更的複寫  
  
1.  在 **訂閱選項** 頁面 **發行集屬性-\< 發行集>** 對話方塊方塊中，設定的值 **複寫結構描述變更** 屬性 **False**。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     若只要傳播特定的結構描述變更，請在結構描述變更之前將屬性設定為 **[True]** ，然後在進行變更後將屬性設定為 **[False]** 。 相反的，若要傳播大多數結構描述變更，而不是給定變更，請在結構描述變更之前將屬性設定為 **[False]** ，然後在進行變更後將屬性設定為 **[True]** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序來指定是否要複寫這些結構描述變更。 您使用的預存程序取決於發行集的類型而定。  
  
#### 建立不會複寫結構描述變更的快照式或交易式發行集  
  
1.  在發行集資料庫的發行者，執行 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ，指定的值為 **0** 的 **@replicate_ddl**。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 建立不會複寫結構描述變更的合併式發行集  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ，指定的值為 **0** 的 **@replicate_ddl**。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 暫時停用快照式或交易式發行集的複寫結構描述變更  
  
1.  使用結構描述變更複寫的發行集，對於執行 [sp_changepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，指定的值為 **replicate_ddl** 的 **@property** 且值為 **0** 的 **@value**。  
  
2.  在發行的物件上執行 DDL 命令。  
  
3.  （選擇性）重新啟用複寫結構描述變更，藉由執行 [sp_changepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，指定的值為 **replicate_ddl** 的 **@property** 且值為 **1** 的 **@value**。  
  
#### 暫時停用合併式發行集的複寫結構描述變更  
  
1.  使用結構描述變更複寫的發行集，對於執行 [sp_changemergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，指定的值為 **replicate_ddl** 的 **@property** 且值為 **0** 的 **@value**。  
  
2.  在發行的物件上執行 DDL 命令。  
  
3.  （選擇性）重新啟用複寫結構描述變更，藉由執行 [sp_changemergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，指定的值為 **replicate_ddl** 的 **@property** 且值為 **1** 的 **@value**。  
  
## 另請參閱  
 [對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  