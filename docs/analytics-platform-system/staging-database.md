---
title: 使用暫存資料庫
description: SQL Server 平行處理資料倉儲 (PDW) 會使用臨時資料庫在載入程式期間暫時儲存資料。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400287"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>在平行處理資料倉儲中使用暫存資料庫 (PDW) 
SQL Server 平行處理資料倉儲 (PDW) 會使用臨時資料庫在載入程式期間暫時儲存資料。 根據預設，SQL Server PDW 會使用目的地資料庫做為暫存資料庫，這可能會導致資料表片段。 若要減少資料表片段，您可以建立使用者定義的暫存資料庫。 或者，當從載入失敗復原時，您可以使用 fastappend 載入模式來改善效能，方法是略過臨時表並直接載入目的地資料表。  
  
## <a name="staging-database-basics"></a><a name="StagingDatabase"></a>暫存資料庫基本概念  
*暫存資料庫*是使用者建立的 PDW 資料庫，可在載入至設備時暫時儲存資料。 針對負載指定暫存資料庫時，設備會先將資料複製到暫存資料庫，然後將暫存資料庫中臨時表的資料複製到目的地資料庫中的永久資料表。  
  
未指定載入的暫存資料庫時，SQL ServerPDW 會在目的地資料庫中建立臨時表，並使用這些資料表來儲存載入的資料，然後再將載入的資料插入到永久目的地資料表中。  
  
當負載使用 *fastappend 模式*時，SQL ServerPDW 會完全略過使用臨時表，並將資料直接附加到目標資料表。 Fastappend 模式可改善 ELT 案例的載入效能，其中資料會從應用程式的觀點載入至資料表。 例如，ELT 進程可能會將資料載入臨時表、透過清理和取消誘騙來處理資料，然後將資料插入目標事實資料表中。 在此情況下，PDW 在將資料插入應用程式的臨時表之前，不需要先將資料載入內部臨時表。 Fastappend 模式可避免額外的載入步驟，這可大幅提升載入效能。 若要使用 fastappend 模式，您必須使用多重交易模式，這表示從失敗或中止的負載復原必須由您自己的負載處理常式來處理。  
  
**暫存資料庫的優點**  
  
臨時資料庫的主要優點是減少資料表片段。 如果未使用暫存資料庫，則會將資料載入至目的地資料庫中的臨時表。 在目的地資料庫中建立和卸載臨時表時，臨時表和永久資料表的頁面會變成交錯。 經過一段時間，就會發生資料表片段，並降低效能。 相反地，暫存資料庫可確保臨時表會在與永久資料表不同的檔案空間中建立和卸載。  
  
**臨時資料庫資料表結構**  
  
每個資料庫資料表的儲存結構相依于目的地資料表。  
  
-   若要將載入堆積或叢集資料行存放區索引，臨時表為堆積。  
  
-   若要將載入 rowstore 叢集索引，暫存資料表是 rowstore 叢集索引。  
  
## <a name="permissions"></a><a name="Permissions"></a>Permissions  
需要 CREATE 許可權 (，才能在暫存資料庫上) 建立臨時表。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="best-practices-for-creating-a-staging-database"></a><a name="CreatingStagingDatabase"></a>建立臨時資料庫的最佳作法  
  
1.  每個設備只能有一個暫存資料庫。 所有目的地資料庫的所有載入作業都可以共用預備資料庫。  
  
2.  臨時資料庫的大小是客戶專用的。 一開始，在第一次填入設備時，暫存資料庫應該夠大，足以容納初始的載入作業。 這些載入作業通常很大，因為多個負載可能會同時發生。 初始載入作業完成且系統在生產環境中之後，每個載入作業的大小可能會較小。 當負載很小時，您可以減少暫存資料庫的大小，以容納較小的載入大小。 若要減少大小，您可以卸載暫存資料庫，然後再以較小的配置重新建立，或者可以使用 [ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 語句。  
  
    建立臨時資料庫時，請使用下列指導方針。  
  
    -   複寫的資料表大小應該是將同時載入之所有複寫資料表的估計大小（每個計算節點）。 大小通常是 25-30 GB。  
  
    -   分散式資料表大小應該是將同時載入之所有分散式資料表的估計大小（每個設備）。  
  
    -   記錄檔大小通常類似于複寫的資料表大小。  
  
## <a name="examples"></a><a name="Examples"></a>範例  
  
### <a name="a-create-a-staging-database"></a>A. 建立臨時資料庫 
下列範例會建立預備資料庫 Stagedb，以搭配設備上的所有負載使用。 假設您估計 5 GB 的五個複寫資料表將會同時載入。 此並行會導致複寫的大小至少配置 25 GB。 假設您預估有六個大小為100、200、400、500、500和 550 GB 的分散式資料表將會同時載入。 這種並行結果會為分散式資料表大小配置至少 2250 GB。  
  
```sql  
CREATE DATABASE Stagedb  
WITH (  
  
    AUTOGROW = ON,  
  
    REPLICATED_SIZE = 25 GB,  
  
    DISTRIBUTED_SIZE = 2250 GB,  
  
    LOG_SIZE = 25 GB  
  
);  
```  

<!-- MISSING LINKS
 
## See Also  
[Common metadata query examples](metadata-query-examples.md)  

-->
  
