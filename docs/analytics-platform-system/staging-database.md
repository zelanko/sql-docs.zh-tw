---
title: 使用暫存資料庫-Parallel Data Warehouse |Microsoft 文件
description: SQL Server Parallel Data Warehouse (PDW) 會使用暫存資料庫，在載入程序期間暫時儲存資料。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 73822c1495fa5f83d9a8ba37325a025999f94530
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544652"
---
# <a name="using-a-staging-database-in-parallel-data-warehouse-pdw"></a>使用暫存資料庫中 Parallel Data Warehouse (PDW)
SQL Server Parallel Data Warehouse (PDW) 會使用暫存資料庫，在載入程序期間暫時儲存資料。 根據預設，SQL Server PDW 會使用目的地資料庫的臨時資料庫，可能會造成資料表片段。 若要減少資料表分散程度，您可以建立使用者定義的暫存資料庫。 或者，當從載入失敗的復原不是問題，您可以使用 fastappend 載入模式以略過暫存資料表和目的地資料表直接載入改進效能。  
  
## <a name="StagingDatabase"></a>暫存資料庫的基本概念  
A*臨時資料庫*是使用者建立的 PDW 資料庫載入至應用裝置時，暫時儲存資料。 指定臨時資料庫時的負載，應用裝置第一次資料複製到暫存資料庫，然後從暫存資料表中的暫存資料庫將資料複製到目的地資料庫中的永久資料表。  
  
暫存資料庫未指定的負載，SQL ServerPDW 目的地資料庫中建立的暫存資料表，並使用它們來儲存所載入的資料之前載入的資料插入永久的目的地資料表。  
  
當負載時，使用*fastappend 模式*，SQL ServerPDW 略過完全使用暫存資料表，並將資料附加至目標資料表的直接。 Fastappend 模式可改善負載效能，ELT 案例，其中資料會載入到應用程式的觀點來看從暫存資料表的資料表。 比方說，ELT 程序無法載入至暫存資料表的資料、 清理和取消 duping，以處理資料和再將資料插入目標資料表。 在此情況下，它不需要 PDW 先載入到內部暫存資料表中的資料在應用程式的暫存資料表中插入資料之前。 Fastappend 模式可避免額外的負載步驟中，會大幅改善負載效能。 若要使用 fastappend 模式，您必須使用多重交易模式中，這表示您自己的載入處理序必須處理從失敗或已中止負載復原。  
  
**暫存資料庫的優點**  
  
暫存資料庫的主要優點是減少資料表分散程度。 如果未使用暫存資料庫，會將資料載入目的地資料庫中的暫存資料表。 當暫存資料表取得建立和卸除目的地資料庫中時，暫存資料表和永久資料表的頁面會變成交錯。 經過一段時間，資料表分散程度，就會發生，並會降低效能。 相反地，會建立暫存資料表，並在個別的檔案空間比永久資料表中卸除可確保暫存資料庫。  
  
**暫存資料庫的資料表結構**  
  
每個資料庫資料表的儲存體結構取決於目的地資料表。  
  
-   若是插入堆積或叢集資料行存放區索引的載入，暫存資料表是堆積。  
  
-   若是載入到資料列存放區叢集索引，暫存資料表會是資料列存放區叢集的索引。  
  
## <a name="Permissions"></a>Permissions  
需要的暫存資料庫空間 （適用於建立的暫存資料表） 的建立權限。 

<!-- MISSING LINKS

For more information, see [Grant Permissions to load data](grant-permissions-to-load-data.md).  

-->
  
## <a name="CreatingStagingDatabase"></a>建立暫存資料庫的最佳作法  
  
1.  只能有一個暫存資料庫，每個應用裝置。 暫存資料庫可以共用所有的目的地資料庫的所有載入作業。  
  
2.  暫存資料庫的大小是特定的客戶。 一開始，當第一次填入設備，臨時資料庫應該大到足以容納初始載入作業。 這些載入工作通常會比較大，因為可以同時進行多項載入。 初始載入作業完成之後，並在系統處於生產環境之後，每個載入作業的大小很小。 當負載很小時，您可以減少暫存資料庫，以容納較小的載入大小的大小。 若要減少大小，您可以卸除暫存資料庫並重新建立具有較小的大小配置，或者您可以使用[ALTER DATABASE](../t-sql/statements/alter-database-parallel-data-warehouse.md)陳述式。  
  
    建立暫存資料庫時，請使用下列指導方針。  
  
    -   複寫的資料表大小應該是每個計算節點，將會同時載入所有複寫資料表的估計的大小。 大小通常是 25-30 GB。  
  
    -   分散式的資料表大小應該估計的大小，每個應用裝置，將會同時載入的所有分散式資料表。  
  
    -   複寫的資料表大小通常相似的記錄檔大小。  
  
## <a name="Examples"></a>範例  
  
### <a name="a-create-a-staging-database"></a>A. 建立暫存資料庫 
下列範例會建立暫存資料庫，Stagedb，用於所有的應用裝置上的負載。 假設您估計五個複寫將會同時載入 5 GB 大小的資料表。 這個並行存取造成配置至少 25 GB 做為複寫的大小。 假設您估計六個分散式資料表的大小為 100，200、 400、 500、 500 和 550 GB 會同時載入。 配置至少 2250 GB 分散式的資料表大小會導致此並行存取。  
  
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
  
