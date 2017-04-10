---
title: "指定發行項類型 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
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
  - "發行 [SQL Server 複寫], 預存程序執行"
  - "發行項 [SQL Server 複寫]、交易式複寫選項"
  - "發行項 [SQL Server 複寫]、合併複寫選項"
  - "預存程序 [SQL Server 複寫], 發行"
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 指定發行項類型 (複寫 Transact-SQL 程式設計)
  複寫的預設發行項類型為資料表發行項，但是您可以將其他資料庫物件發行為發行項，包括檢視、預存程序、使用者定義函數及預存程序執行。 您可以使用複寫預存程序，於定義發行項時以程式設計方式指定發行項類型。 使用哪些預存程序取決於複寫的類型和發行項類型而定。  
  
> [!NOTE]  
>  在定義資料表、檢視和預存程序發行項時的僅限結構描述指定會指示，只會複寫物件定義。  
  
### 在交易式或快照式發行集中發行資料表發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定下列值的其中一個 **@type** 來定義發行項的類型︰  
  
    -   **logbased** -記錄檔為基礎的資料表發行項，也就是交易式和快照式複寫的預設值。 複寫會自動產生用於水平篩選的預存程序以及定義垂直篩選之發行項的檢視。  
  
    -   **logbased manualfilter** -記錄式、 水平篩選發行項，其中用於水平篩選的預存程序是手動建立使用者定義並指定 **@filter**。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
    -   **logbased manualview** -記錄式、 垂直篩選發行項定義垂直篩選發行項之檢視的位置建立和由使用者定義並指定 **@sync_object**。 如需詳細資訊，請參閱 [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [定義及修改資料行篩選](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
    -   **logbased manualboth** -記錄式、 水平及垂直篩選的發行項的預存程序用來水平篩選及定義垂直篩選發行項之檢視的位置建立及定義使用者和指定 **@filter** 和 **@sync_object**, 分別。 如需詳細資訊，請參閱 [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [定義及修改資料行篩選](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  如 **logbased manualboth** 和 **logbased manualfilter** 發行項，執行 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 產生水平篩選發行項篩選的預存程序。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  如 **logbased manualboth**, ，**logbased manualview**, ，和 **logbased manualfilter** 發行項，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 來產生定義垂直篩選發行項的檢視。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
### 在交易式或快照式發行集中發行檢視或索引檢視發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定下列值的其中一個 **@type** 來定義發行項的類型︰  
  
    -   **索引檢視 logbased** -記錄式索引檢視表發行項。 複寫會自動產生用於水平篩選的預存程序以及定義垂直篩選之發行項的檢視。  
  
    -   **僅限檢視結構描述** -僅限結構描述的檢視表發行項。 也必須要複寫基底資料表。  
  
    -   **僅限索引檢視表結構描述** -僅限結構描述的索引的檢視發行項。 也必須要複寫基底資料表。  
  
    -   **索引檢視 logbased manualfilter** -記錄式、 水平篩選的索引檢視表發行項，其中用於水平篩選的預存程序是以手動方式建立使用者定義並指定 **@filter**。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
    -   **索引檢視 logbased manualview** -記錄式、 已篩選的索引的檢視發行項定義垂直篩選發行項之檢視的位置建立及定義使用者，指定 **@sync_object**。 如需詳細資訊，請參閱 [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [定義及修改資料行篩選](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
    -   **索引檢視 logbased manualboth** -記錄式、 已篩選的索引的檢視發行項，建立和由使用者定義並指定這兩個預存程序用來水平篩選及定義垂直篩選發行項之檢視的 **@filter** 和 **@sync_object**, 分別。 如需詳細資訊，請參閱 [定義及修改靜態資料列篩選](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 和 [定義及修改資料行篩選](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  如 **logbased manualboth** 和 **logbased manualfilter** 發行項，執行 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 產生水平篩選發行項篩選的預存程序。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  如 **logbased manualboth**, ，**logbased manualview**, ，和 **logbased manualfilter** 發行項，執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 來產生定義垂直篩選發行項的檢視。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
### 在交易式或快照式發行集中發行預存程序、預存程序執行或使用者定義函數發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定下列值的其中一個 **@type** 來定義發行項的類型︰  
  
    -   **僅限程序結構描述** -僅限結構描述的預存程序發行項。  
  
    -   **proc exec** -將預存程序執行複寫的發行項所有訂閱者。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **serializable proc exec** -它可序列化交易的內容中執行時，才複寫預存程序執行。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **僅限函數結構描述** -僅限結構描述的使用者定義函數發行項。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
### 在合併式發行集中發行資料表或檢視發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定下列值的其中一個 **@type** 來定義發行項的類型︰  
  
    -   **資料表** -資料表發行項。  
  
    -   **僅限索引檢視表結構描述** -僅限結構描述的索引的檢視發行項。  
  
    -   **僅限檢視結構描述** -僅限結構描述的檢視表發行項。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
### 在合併式發行集中發行預存程序或使用者定義函數發行項  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定下列值的其中一個 **@type** 來定義發行項的類型︰  
  
    -   **僅限函數結構描述** -僅限結構描述的使用者定義函數發行項。  
  
    -   **僅限程序結構描述** -僅限結構描述的預存程序發行項。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## 另請參閱  
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  