---
title: Tempdb 資料庫-Parallel Data Warehouse |Microsoft Docs
description: 在平行處理資料倉儲中的 Tempdb 資料庫。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63156968"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>平行處理資料倉儲中的 tempdb 資料庫
**tempdb**已儲存的使用者資料庫的本機暫存資料表的 SQL Server PDW 系統資料庫。 暫存資料表通常會用來改善查詢效能。 比方說，您可以使用暫存資料表，以模塊化指令碼，並重複使用計算的資料。  
  
如需有關系統資料庫的詳細資訊，請參閱[系統資料庫](system-databases.md)。  
  
## <a name="Basics"></a>主要詞彙和概念  
*本機暫存資料表*  
A*本機暫存資料表*使用 # 前置詞的資料表名稱前面，而且本機使用者工作階段所建立的暫存資料表。 每個工作階段只能存取自己的工作階段中本機暫存資料表的資料。  
  
每個工作階段可以檢視所有工作階段中的本機暫存資料表的中繼資料。 例如，所有工作階段可以在其中檢視使用的所有本機暫存資料表的中繼資料`SELECT * FROM tempdb.sys.tables`查詢。  
  
全域暫存資料表  
*全域暫存資料表*、 支援與 SQL Server # # 的語法，這一版的 SQL Server PDW 中不支援。  
  
pdwtempdb  
**pdwtempdb**是儲存本機暫存資料表的資料庫。  
  
使用 SQL Server PDW 不會實作暫存資料表**tempdb**資料庫。 相反地，PDW 將它們儲存在名為 pdwtempdb 的資料庫。 此資料庫在每個計算節點上存在，而且不會察覺到使用者已透過 PDW 介面。 在系統管理員主控台中，在儲存體 頁面上，您會看到這些報銷在 PDW 系統資料庫，叫做**tempdb sql**。  
  
tempdb  
**tempdb**是 SQL Server tempdb 資料庫。 它會使用最低限度記錄。 SQL Server 會使用 tempdb 在計算節點上儲存過程中執行 SQL Server 作業需要的暫存資料表。  
  
SQL Server PDW 會從資料表卸除**tempdb**時：  
  
-   DROP TABLE 陳述式。  
  
-   工作階段已中斷連接。 只有工作階段的暫存資料表會卸除。  
  
-   設備會關閉。  
  
-   控制節點擁有叢集容錯移轉。  
  
## <a name="general-remarks"></a>一般備註  
除非明確指定，否則，SQL Server PDW 執行暫存資料表和永久資料表相同的作業。 比方說，本機暫存資料表的詳細資訊，就像的永久資料表中的資料為分散式或複寫到各個計算節點。  
  
## <a name="LimitationsRestrictions"></a>限制事項  
限制和限制的 SQL Server PDW**tempdb**資料庫。 您*無法：*  
  
-   建立全域暫存資料表開頭為 # #。  
  
-   執行備份或還原**tempdb**。  
  
-   修改權限**tempdb**具有**GRANT**，**拒絕**，或**撤銷**陳述式。  
  
-   執行**DBCC SHRINKLOG** for **tempdb**tempdb。  
  
-   執行 DDL 作業**tempdb**。 有幾個例外狀況。 如需詳細資訊，請參閱本機暫存資料表上的下列限制事項的清單。  
  
限制與本機暫存資料表的限制。 您*無法：*  
  
-   重新命名的暫存資料表  
  
-   在暫存資料表上建立資料分割、 檢視或非叢集索引。 **ALTER INDEX**可用來重建資料表，建立一個叢集的索引。  
  
-   修改到暫存資料表的權限，使用 GRANT、 DENY 或 REVOKE 陳述式。  
  
-   暫存資料表上執行資料庫主控台命令。  
  
-   使用相同的批次內的兩個或多個暫存資料表相同的名稱。 如果在批次內使用超過一個本機暫存資料表，每個資料表都必須有唯一的名稱。 如果多個工作階段會執行相同的批次，並建立相同的本機暫存資料表，SQL Server PDW 在內部將數值後置詞附加至本機暫存資料表名稱，以維持每個本機暫存資料表的唯一名稱。  
  
> [!NOTE]  
> 您*可以*建立和更新在暫存資料表上的統計資料。**ALTER INDEX**可用來重建叢集的索引。  
  
## <a name="permissions"></a>Permissions  
任何使用者都可以在 tempdb 中建立暫時物件。 除非收到其他權限，否則使用者只能存取自己的物件。 您可以撤銷 tempdb 的連接權限來阻止使用者使用 tempdb，不過不建議您這樣做，因為有些常式作業需要使用 tempdb。  
  
## <a name="RelatedTasks"></a>相關的工作  
  
|工作|描述|  
|---------|---------------|  
|在當中建立資料表**tempdb**。|您可以建立使用者的暫存資料表的 CREATE TABLE 和 CREATE TABLE AS SELECT 陳述式使用。 如需詳細資訊，請參閱 < [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)並[CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)。|  
|檢視中的現有資料表的清單**tempdb**。|`SELECT * FROM tempdb.sys.tables;`|  
|檢視中的現有資料行的清單**tempdb**。|`SELECT * FROM tempdb.sys.columns;`|  
|檢視中的現有物件的清單**tempdb**。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
