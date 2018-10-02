---
title: 指定發行項類型 (複寫 Transact-SQL 程式設計) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- stored procedures [SQL Server replication], publishing
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b72f1f7b6779819de87bc3aa37f8c9fc06e71fc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807686"
---
# <a name="specify-article-types-replication-transact-sql-programming"></a>指定發行項類型 (複寫 Transact-SQL 程式設計)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫的預設發行項類型為資料表發行項，但是您可以將其他資料庫物件發行為發行項，包括檢視、預存程序、使用者定義函數及預存程序執行。 您可以使用複寫預存程序，於定義發行項時以程式設計方式指定發行項類型。 使用哪些預存程序取決於複寫的類型和發行項類型而定。  
  
> [!NOTE]  
>  在定義資料表、檢視和預存程序發行項時的僅限結構描述指定會指示，只會複寫物件定義。  
  
### <a name="to-publish-a-table-article-in-a-transactional-or-snapshot-publication"></a>在交易式或快照式發行集中發行資料表發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 針對 **@type** 指定下列其中一個值，以定義發行項的類型：  
  
    -   **logbased** - 記錄式資料表發行項，這是交易式和快照式複寫的預設值。 複寫會自動產生用於水平篩選的預存程序以及定義垂直篩選之發行項的檢視。  
  
    -   **logbased manualfilter** - 記錄式、水平篩選的發行項，其中用於水平篩選的預存程序是由使用者手動建立及定義，而且是針對 **@filter**。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
    -   **logbased manualview** - 記錄式、垂直篩選的發行項，其中用於定義垂直篩選之發行項的檢視是由使用者建立及定義，而且是針對 **@sync_object**。 如需相關資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
    -   **logbased manualboth** - 記錄式、水平和垂直篩選的發行項，其中用於水平篩選的預存程序及定義垂直篩選之發行項的檢視是由使用者所建立及定義，而且是分別針對 **@filter** 及 **@sync_object**所指定。 如需相關資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  如果是 **logbased manualboth** 和 **logbased manualfilter** 發行項，請執行 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 來產生用於水平篩選之發行項的篩選預存程序。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  如果是 **logbased manualboth**、 **logbased manualview**和 **logbased manualfilter** 發行項，請執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 來產生用於定義垂直篩選之發行項的檢視。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
### <a name="to-publish-a-view-or-indexed-view-article-in-a-transactional-or-snapshot-publication"></a>在交易式或快照式發行集中發行檢視或索引檢視發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 針對 **@type** 指定下列其中一個值，以定義發行項的類型：  
  
    -   **indexed view logbased** - 記錄式索引檢視發行項。 複寫會自動產生用於水平篩選的預存程序以及定義垂直篩選之發行項的檢視。  
  
    -   **view schema only** - 僅限結構描述的檢視發行項。 也必須要複寫基底資料表。  
  
    -   **indexed view schema only** - 僅限結構描述的索引檢視發行項。 也必須要複寫基底資料表。  
  
    -   **indexed view logbased manualfilter** - 記錄式、水平篩選的索引檢視發行項，其中用於水平篩選的預存程序是由使用者手動建立及定義，而且是針對 **@filter**。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
    -   **indexed view logbased manualview** - 記錄式、篩選的索引檢視發行項，其中用於定義垂直篩選之發行項的檢視是由使用者建立及定義，而且是針對 **@sync_object**。 如需相關資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
    -   **indexed view logbased manualboth** - 記錄式、篩選的索引檢視發行項，其中用於水平篩選的預存程序及定義垂直篩選之發行項的檢視是由使用者所建立及定義，而且是分別針對 **@filter** 及 **@sync_object**所指定。 如需相關資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 及 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  如果是 **logbased manualboth** 和 **logbased manualfilter** 發行項，請執行 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 來產生用於水平篩選之發行項的篩選預存程序。 如需詳細資訊，請參閱 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  如果是 **logbased manualboth**、 **logbased manualview**和 **logbased manualfilter** 發行項，請執行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 來產生用於定義垂直篩選之發行項的檢視。 如需詳細資訊，請參閱 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
### <a name="to-publish-a-stored-procedure-stored-procedure-execution-or-user-defined-function-article-in-a-transactional-or-snapshot-publication"></a>在交易式或快照式發行集中發行預存程序、預存程序執行或使用者定義函數發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 針對 **@type** 指定下列其中一個值，以定義發行項的類型：  
  
    -   **proc schema only** - 僅限結構描述的預存程序發行項。  
  
    -   **proc exec** - 將預存程序的執行複寫到發行項的所有訂閱者。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **serializable proc exec** - 只有當預存程序執行於可序列化交易的環境內時，才複寫預存程序的執行。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
    -   **func schema only** - 僅限結構描述的使用者定義函數發行項。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
### <a name="to-publish-a-table-or-view-article-in-a-merge-publication"></a>在合併式發行集中發行資料表或檢視發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 針對 **@type** 指定下列其中一個值，以定義發行項的類型：  
  
    -   **table** - 資料表發行項。  
  
    -   **indexed view schema only** - 僅限結構描述的索引檢視發行項。  
  
    -   **view schema only** - 僅限結構描述的檢視發行項。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
### <a name="to-publish-a-stored-procedure-or-user-defined-function-article-in-a-merge-publication"></a>在合併式發行集中發行預存程序或使用者定義函數發行項  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 針對 **@type** 指定下列其中一個值，以定義發行項的類型：  
  
    -   **func schema only** - 僅限結構描述的使用者定義函數發行項。  
  
    -   **proc schema only** - 僅限結構描述的預存程序發行項。  
  
     這樣會為發行集定義新的發行項。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
