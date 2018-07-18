---
title: 檢視合併式發行集 （複寫 TRANSACT-SQL 程式設計） 的衝突資訊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- sp_helpmergeconflictrows
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
- sp_helpmergearticleconflicts
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48225870d89fc6bf39355957187fac84a704093d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316098"
---
# <a name="view-conflict-information-for-merge-publications-replication-transact-sql-programming"></a>檢視合併式發行集的衝突資訊 (複寫 Transact-SQL 程式設計)
  在合併式複寫中解決衝突時，遺失之資料列的資料會寫入衝突資料表。 可以使用複寫預存程序來以程式設計的方式檢視此衝突資料。 如需詳細資訊，請參閱 [進階合併式複寫衝突偵測與解決](merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>檢視所有衝突類型的衝突資訊和遺失的資料列資料  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)。 請注意結果集中下列資料行的值：  
  
    -   **centralized_conflicts** - 1 表示在發行者上儲存衝突資料列，0 則表示不會在發行者上儲存衝突資料列。  
  
    -   **decentralized_conflicts** - 1 表示在訂閱者上儲存衝突資料列，0 則表示不會在訂閱者上儲存衝突資料列。  
  
        > [!NOTE]  
        >  合併式發行集的衝突記錄行為是使用 **@conflict_logging** 的 [@conflict_logging](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 已取代使用 **@centralized_conflicts** 參數。  
  
     下表描述這些資料行的值 (根據針對 **@conflict_logging**。  
  
    |@conflict_logging 值|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |`publisher`|1|0|  
    |`subscriber`|0|1|  
    |`both`|1|1|  
  
2.  在發行集資料庫的發行者上或是在訂閱資料庫的訂閱者上，執行 [sp_helpmergearticleconflicts](/sql/relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql)。 針對 **@publication** 指定值，只傳回屬於特定發行集之發行項的衝突資訊。 這樣會傳回有衝突之發行項的衝突資料表資訊。 請記下感興趣之任何發行項的 **conflict_table** 值。 如果發行項的 **conflict_table** 值為 NULL，只要刪除此發行項中已發生的衝突。  
  
3.  (選擇性) 檢閱感興趣之發行項的衝突資料列。 根據步驟 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值而定，執行下列其中一項：  
  
    -   在發行集資料庫的發行者上，執行 [sp_helpmergeconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql)。 針對 **@conflict_table**。 (選擇性) 指定 **@publication** 的值，將傳回的衝突資訊限制為特定的發行集。 這樣會傳回遺失之資料列的資料列資料和其他資訊。  
  
    -   在訂閱資料庫的訂閱者上，執行 [sp_helpmergeconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql)。 針對 **@conflict_table**。 這樣會傳回遺失之資料列的資料列資料和其他資訊。  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>只檢視刪除失敗時的衝突資訊  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)。 請注意結果集中下列資料行的值：  
  
    -   **centralized_conflicts** - 1 表示在發行者上儲存衝突資料列，0 則表示不會在發行者上儲存衝突資料列。  
  
    -   **decentralized_conflicts** - 1 表示在訂閱者上儲存衝突資料列，0 則表示不會在訂閱者上儲存衝突資料列。  
  
        > [!NOTE]  
        >  合併式發行集的衝突記錄行為是使用 **@conflict_logging** 的 [@conflict_logging](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 已取代使用 **@centralized_conflicts** 參數。  
  
2.  在發行集資料庫的發行者上或是在訂閱資料庫的訂閱者上，執行 [sp_helpmergearticleconflicts](/sql/relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql)。 針對 **@publication** 指定值，只傳回屬於特定發行集之發行項的衝突資料表資訊。 這樣會傳回有衝突之發行項的衝突資料表資訊。 請記下感興趣之任何發行項的 **source_object** 值。 如果發行項的 **conflict_table** 值為 NULL，只要刪除此發行項中已發生的衝突。  
  
3.  (選擇性) 檢閱刪除衝突的衝突資訊。 根據步驟 1 中 **centralized_conflicts** 和 **decentralized_conflicts** 的值而定，執行下列其中一項：  
  
    -   在發行集資料庫的發行者上，執行 [sp_helpmergedeleteconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql)。 針對 **@source_object**。 (選擇性) 指定 **@publication** 的值，將傳回的衝突資訊限制為特定的發行集。 這樣會傳回儲存在發行者上的刪除衝突資訊。  
  
    -   在訂閱資料庫的訂閱者上，執行 [sp_helpmergedeleteconflictrows](/sql/relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql)。 針對 **@source_object**。 (選擇性) 指定 **@publication** 的值，將傳回的衝突資訊限制為特定的發行集。 這樣會傳回儲存在訂閱者上的刪除衝突資訊。  
  
## <a name="see-also"></a>另請參閱  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
