---
title: 使用非叢集資料行存放區索引 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e97aed3a5a4f5b49e482479b58928d2092a314f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773783"
---
# <a name="using-nonclustered-columnstore-indexes"></a>使用非叢集資料行存放區索引
  描述在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表上使用非叢集資料行存放區索引的主要工作。  
  
 如需資料行存放區索引的概觀，請參閱＜ [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md)＞。  
  
 如需有關叢集資料行存放區索引的詳細資訊，請參閱＜ [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md)＞。  
  
## <a name="contents"></a>目錄  
  
-   [建立非叢集資料行存放區索引](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)  
  
-   [變更非叢集資料行存放區索引中的資料](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)  
  
##  <a name="load"></a> 建立非叢集資料行存放區索引  
 要將資料載入非叢集資料行存放區索引，先將資料載入至傳統的資料列存放區資料表儲存為堆積或叢集索引，然後再使用[建立資料行存放區索引&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql)來建立資料行存放區索引。  
  
 ![將資料載入至資料行存放區索引](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "資料載入資料行存放區索引")  
  
##  <a name="change"></a> 變更非叢集資料行存放區索引中的資料  
 一旦您在資料表上建立非叢集資料行存放區索引，就無法直接修改該資料表中的資料。 使用 INSERT、UPDATE、DELETE 或 MERGE 的查詢將會失敗，並傳回錯誤訊息。 若要加入或修改資料表中的資料，您可以執行下列其中一項操作：  
  
-   停用資料行存放區索引。 然後您就可以更新資料表中的資料。 如果您停用資料行存放區索引，您可以在完成更新資料時重建資料行存放區索引。 例如：  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   卸除資料行存放區索引、 更新資料表，並再重新建立與建立資料行存放區索引的資料行存放區索引。 例如：  
  
    ```  
    DROP INDEX mycolumnstoreindex ON mytable  
    -- update mytable --  
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;  
  
    ```  
  
-   將資料載入未包含資料行存放區索引的暫存資料表。 在暫存資料表上建立資料行存放區索引。 將暫存資料表切換至主資料表的空白分割區。  
  
-   從具有資料行存放區索引的資料表分割區切換至空白的暫存資料表。 如果暫存資料表上有資料行存放區索引，請停用資料行存放區索引。 執行所有更新。 建立 (或重建) 資料行存放區索引。 將暫存資料表切換回 (現在為空白的) 主資料表分割區。  
  

  
  
