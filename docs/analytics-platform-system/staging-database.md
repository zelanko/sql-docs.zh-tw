---
title: 使用暫存資料庫-Parallel Data Warehouse |Microsoft Docs
description: SQL Server Parallel Data Warehouse (PDW) 會使用暫存資料庫，在載入過程中暫時儲存資料。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 52ede16185515c3df00ff21ece784d62eec984ef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157694"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>使用暫存資料庫中 Parallel Data Warehouse (PDW)
SQL Server Parallel Data Warehouse (PDW) 會使用暫存資料庫，在載入過程中暫時儲存資料。 根據預設，SQL Server PDW 做為目的地資料庫的臨時資料庫，這可能會導致資料表片段化。 若要減少資料表的片段化，您可以建立使用者定義的暫存資料庫。 或者，當從載入失敗的復原不需要考量，您可以使用 fastappend 載入模式以略過暫存資料表，並直接載入目的地資料表，以改善效能。  
  
## <a name="StagingDatabase"></a>暫存資料庫的基本概念  
A*臨時資料庫*是使用者建立的 PDW 資料庫載入至應用裝置時，暫時儲存資料。 載入指定的暫存資料庫時，應用裝置會先將資料複製到暫存資料庫，並再從暫存資料庫中的暫存資料表將資料複製到目的地資料庫中的永久資料表。  
  
當負載未指定暫存資料庫時，SQL ServerPDW 目的地資料庫中建立的暫存資料表，並使用它們來儲存所載入的資料，它將載入的資料插入至永久的目的地資料表之前。  
  
當負載時，使用*fastappend 模式*，SQL ServerPDW 會略過 一併使用暫存資料表，並將資料附加至目標資料表的直接。 Fastappend 模式可改善資料載入其中的資料表，是從應用程式的觀點來看一個暫存資料表的 ELT 情節的負載效能。 比方說，ELT 程序無法將資料載入暫存資料表、 處理資料清理和取消 duping，並再將資料插入目標事實資料表。 在此情況下，不需要適用於 PDW 先載入到內部暫存資料表中的資料之前將資料插入應用程式的暫存資料表。 Fastappend 模式可避免額外的負載步驟中，這可大幅改善載入效能。 若要使用 fastappend 模式，您必須使用多重交易模式中，這表示從失敗或已中止負載復原必須由您自己的載入程序。  
  
**暫存資料庫的優點**  
  
暫存資料庫的主要優點是減少資料表的片段化。 如果未使用暫存資料庫，則會將資料載入目的地資料庫中的暫存資料表。 取得建立暫存資料表，並卸除目的地資料庫中，暫存資料表和永久資料表的頁面會變成交錯。 經過一段時間，資料表的片段化，就會發生，並會降低效能。 相反地，會建立暫存資料表，並在個別的檔案空間比永久資料表中卸除可確保暫存資料庫。  
  
**暫存資料庫的資料表結構**  
  
每個資料庫資料表的儲存體結構取決於目的地資料表。  
  
-   針對至堆積或叢集資料行存放區索引的負載，暫存資料表是堆積。  
  
-   暫存資料表載入至資料列存放區叢集索引，是資料列存放區叢集的索引。  
  
## <a name="Permissions"></a>Permissions  
需要暫存資料庫的 CREATE 權限 （用於建立暫存資料表）。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>建立暫存資料庫的最佳作法  
  
1.  只應該有一個暫存資料庫，每一設備。 暫存資料庫可由所有目的地資料庫的所有載入作業共用。  
  
2.  暫存資料庫的大小是客戶專屬。 一開始，當第一次填入的設備，臨時資料庫應該大到足以容納初始載入作業。 這些載入工作通常都很大，因為可以同時進行多項載入。 初始載入作業已完成且系統在生產環境中之後，每個載入作業的大小很小。 當負載很小時，您可以減少暫存資料庫，以容納較小的載入大小的大小。 若要減少大小，您可以卸除暫存資料庫，然後再次建立它與較小的大小配置，或者您可以使用[ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)陳述式。  
  
    建立暫存資料庫時，請使用下列指導方針。  
  
    -   複寫的資料表大小應該是估計的大小，每個計算節點，會同時載入的所有複寫資料表。 大小通常是 25-30 GB。  
  
    -   配置資源分散式的資料表大小應該是估計的大小，每一設備，會同時載入的所有分散式資料表。  
  
    -   記錄檔大小是通常類似於複寫的資料表大小。  
  
## <a name="Examples"></a>範例  
  
### <a name="a-create-a-staging-database"></a>A. 建立暫存資料庫 
下列範例會建立暫存資料庫，Stagedb，用於在應用裝置上的所有載入。 假設您估計五個複寫資料表大小的 5 GB 會同時載入。 這個並行存取會導致配置複寫的大小至少 25 GB。 假設您估計六個分散式資料表的大小為 100、 200、 400、 500、 500 和 550GB 會同時載入。 這個並行存取會導致配置資源分散式的資料表大小至少 2250 GB。  
  
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
  
