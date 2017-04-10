---
title: "檢視合併式發行集的衝突資訊 (複寫 Transact-SQL 程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
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
  - "合併式複寫衝突解決 [SQL Server 複寫], 檢視衝突"
  - "sp_helpmergeconflictrows"
  - "檢視衝突資訊"
  - "衝突解決 [SQL Server 複寫], 合併式複寫"
  - "sp_helpmergearticleconflicts"
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 檢視合併式發行集的衝突資訊 (複寫 Transact-SQL 程式設計)
  在合併式複寫中解決衝突時，遺失之資料列的資料會寫入衝突資料表。 可以使用複寫預存程序來以程式設計的方式檢視此衝突資料。 如需詳細資訊，請參閱 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
### 檢視所有衝突類型的衝突資訊和遺失的資料列資料  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 請注意結果集中下列資料行的值：  
  
    -   **centralized_conflicts** -1 表示衝突資料列會儲存在 「 發行者 」，而 0 則表示衝突資料列，不會儲存在 「 發行者 」。  
  
    -   **decentralized_conflicts** -1 表示衝突資料列會儲存在訂閱者，0 表示 「 訂閱者 」 不儲存衝突資料列。  
  
        > [!NOTE]  
        >  合併式發行集的衝突記錄行為使用設定的 **@conflict_logging** 參數 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 使用 **@centralized_conflicts** 參數已被取代。  
  
     下表描述這些指定的值為基礎的資料行的值 **@conflict_logging**。  
  
    |@conflict_logging value|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  在發行集資料庫的發行者或訂閱資料庫的訂閱者端，執行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 針對 **@publication** 指定值，只傳回屬於特定發行集之發行項的衝突資訊。 這樣會傳回有衝突之發行項的衝突資料表資訊。 記下的值 **conflict_table** 感興趣的任何發行項。 如果值 **conflict_table** 發行項為 NULL，只是刪除衝突發生在這篇文章。  
  
3.  (選擇性) 檢閱感興趣之發行項的衝突資料列。 依據的值 **centralized_conflicts** 和 **decentralized_conflicts** 從步驟 1 中，執行下列其中之一︰  
  
    -   在發行集資料庫的發行者，執行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 指定衝突資料表發行項 （從步驟 1） **@conflict_table**。 （選擇性）指定的值為 **@publication** 來限制傳回的衝突資訊至特定的發行集。 這樣會傳回遺失之資料列的資料列資料和其他資訊。  
  
    -   在訂閱資料庫上的 「 訂閱者 」 執行 [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md)。 指定衝突資料表發行項 （從步驟 1） **@conflict_table**。 這樣會傳回遺失之資料列的資料列資料和其他資訊。  
  
### 只檢視刪除失敗時的衝突資訊  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)。 請注意結果集中下列資料行的值：  
  
    -   **centralized_conflicts** -1 表示衝突資料列會儲存在 「 發行者 」，而 0 則表示衝突資料列，不會儲存在 「 發行者 」。  
  
    -   **decentralized_conflicts** -1 表示衝突資料列會儲存在訂閱者，0 表示 「 訂閱者 」 不儲存衝突資料列。  
  
        > [!NOTE]  
        >  使用設定合併式發行集的衝突記錄行為 **@conflict_logging** 參數 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 使用 **@centralized_conflicts** 參數已被取代。  
  
2.  在發行集資料庫的發行者或訂閱資料庫的訂閱者端，執行 [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md)。 針對 **@publication** 指定值，只傳回屬於特定發行集之發行項的衝突資料表資訊。 這樣會傳回有衝突之發行項的衝突資料表資訊。 記下的值 **source_object** 感興趣的任何發行項。 如果值 **conflict_table** 發行項為 NULL，只是刪除衝突發生在這篇文章。  
  
3.  (選擇性) 檢閱刪除衝突的衝突資訊。 依據的值 **centralized_conflicts** 和 **decentralized_conflicts** 從步驟 1 中，執行下列其中之一︰  
  
    -   在發行集資料庫的發行者，執行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 指定的名稱衝突發生所在的來源資料表 （來自步驟 1） **@source_object**。 （選擇性）指定的值為 **@publication** 來限制傳回的衝突資訊至特定的發行集。 這樣會傳回儲存在發行者上的刪除衝突資訊。  
  
    -   在訂閱資料庫上的 「 訂閱者 」 執行 [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md)。 指定的名稱衝突發生所在的來源資料表 （來自步驟 1） **@source_object**。 （選擇性）指定的值為 **@publication** 來限制傳回的衝突資訊至特定的發行集。 這樣會傳回儲存在訂閱者上的刪除衝突資訊。  
  
## 另請參閱  
 [進階合併式複寫衝突偵測與解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  