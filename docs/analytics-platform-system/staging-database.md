---
title: 使用臨時資料庫
description: SQL Server 平行處理資料倉儲（PDW）會使用臨時資料庫，在載入過程中暫時儲存資料。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: dcd7f95833695cc5f9f791d83a6221c35e88f58e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400287"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>在平行處理資料倉儲（PDW）中使用臨時資料庫
SQL Server 平行處理資料倉儲（PDW）會使用臨時資料庫，在載入過程中暫時儲存資料。 根據預設，SQL Server PDW 會使用目的地資料庫做為暫存資料庫，這可能會造成資料表片段。 若要減少資料表片段，您可以建立使用者定義的臨時資料庫。 或者，當從載入失敗復原不是問題時，您可以使用 fastappend 載入模式來改善效能，方法是略過臨時表並直接載入目的地資料表。  
  
## <a name="staging-database-basics"></a><a name="StagingDatabase"></a>臨時資料庫基本概念  
*暫存資料庫*是使用者建立的 PDW 資料庫，會在將資料載入應用裝置時暫時儲存。 指定負載的臨時資料庫時，設備會先將資料複製到臨時資料庫，然後將資料從臨時資料庫中的臨時表複製到目的地資料庫中的永久資料表。  
  
若未指定負載的臨時資料庫，SQL ServerPDW 會在目的地資料庫中建立臨時表，並使用它們來儲存載入的資料，然後再將載入的資料插入至永久的目的地資料表。  
  
當負載使用*fastappend 模式*時，SQL ServerPDW 會完全略過使用臨時表，並將資料直接附加至目標資料表。 Fastappend 模式可改善 ELT 案例的載入效能，其中資料會從應用程式的觀點載入至資料表，這是臨時表。 例如，ELT 進程可以將資料載入臨時表、清理和取消 duping 來處理資料，然後將資料插入目標事實資料表。 在此情況下，PDW 在將資料插入應用程式的臨時表之前，不需要先將資料載入內部臨時表。 Fastappend 模式可避免額外的負載步驟，大幅提升負載效能。 若要使用 fastappend 模式，您必須使用多重交易模式，這表示從失敗或中止的負載復原必須由您自己的載入進程處理。  
  
**臨時資料庫的優點**  
  
臨時資料庫的主要優點是減少資料表的片段。 如果未使用臨時資料庫，則會將資料載入目的地資料庫中的臨時表。 在目的地資料庫中建立和卸載臨時表時，臨時表和永久資料表的頁面會變得交錯。 經過一段時間，會發生資料表片段並降低效能。 相反地，臨時資料庫可確保臨時表在與永久資料表不同的檔案空間中建立和卸載。  
  
**臨時資料庫資料表結構**  
  
每個資料庫資料表的儲存結構取決於目的地資料表。  
  
-   若要將載入堆積或叢集資料行存放區索引，臨時表為堆積。  
  
-   若要載入 rowstore 叢集索引，臨時表是 rowstore 叢集索引。  
  
## <a name="permissions"></a><a name="Permissions"></a>權限  
需要在臨時資料庫上建立許可權（用於建立臨時表）。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="best-practices-for-creating-a-staging-database"></a><a name="CreatingStagingDatabase"></a>建立臨時資料庫的最佳作法  
  
1.  每個設備應該只有一個暫存資料庫。 所有目的地資料庫的所有載入作業都可以共用臨時資料庫。  
  
2.  暫存資料庫的大小是客戶特有的。 一開始，在第一次填入設備時，暫存資料庫應該夠大，以容納初始載入作業。 這些載入作業通常會很大，因為可以同時執行多個負載。 在初始載入作業完成且系統進入生產環境後，每個載入作業的大小可能會較小。 當負載很小時，您可以減少臨時資料庫的大小，以容納較小的負載大小。 若要縮減大小，您可以卸載臨時資料庫，然後使用較小的配置重新建立它，或者您可以使用[ALTER database](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)語句。  
  
    建立臨時資料庫時，請使用下列指導方針。  
  
    -   複寫的資料表大小應該是所有將同時載入之複寫資料表的估計大小（依據計算節點）。 大小通常是 25-30 GB。  
  
    -   分散式資料表大小應該是所有將同時載入之分散式資料表的預估大小（每一設備）。  
  
    -   記錄檔大小通常類似于複寫的資料表大小。  
  
## <a name="examples"></a><a name="Examples"></a>範例  
  
### <a name="a-create-a-staging-database"></a>A. 建立臨時資料庫 
下列範例會建立臨時資料庫 Stagedb，以便與設備上的所有負載搭配使用。 假設您估計五個大小為 5 GB 的複寫資料表會同時載入。 此並行會導致複寫的大小至少配置 25 GB。 假設您估計6個大小為100、200、400、500、500和 550 GB 的分散式資料表會同時載入。 此並行處理會導致分配至少 2250 GB 的分散式資料表大小。  
  
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
  
