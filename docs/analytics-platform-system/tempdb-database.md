---
title: "tempdb 資料庫 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5840033d-2dc6-4576-8a5f-067e2a58b170
caps.latest.revision: "22"
ms.workload: not set
ms.openlocfilehash: 94cd8614f5098a1f065dbfe19f0ec024c42f9179
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="tempdb-database"></a>tempdb 資料庫
**tempdb**會儲存使用者資料庫的本機暫存資料表的 SQL Server PDW 系統資料庫。 暫存資料表，通常可用來改善查詢效能。 比方說，您可以使用的暫存資料表，使模組化指令碼，並重複使用計算的資料。  
  
如需系統資料庫的詳細資訊，請參閱[系統資料庫](system-databases.md)。  
  
## <a name="Basics"></a>主要詞彙和概念  
*本機暫存資料表*  
A*本機暫存資料表*使用 # 前置詞的資料表名稱前面，而且本機使用者工作階段所建立的暫存資料表。 每個工作階段只能存取自己的工作階段的本機暫存資料表中的資料。  
  
每個工作階段可以檢視所有工作階段中的本機暫存資料表的中繼資料。 例如，所有工作階段可以檢視使用的所有本機暫存資料表的中繼資料`SELECT * FROM tempdb.sys.tables`查詢。  
  
全域暫存資料表  
*全域暫存資料表*、 支援的 SQL Server # # 語法，在這一版的 SQL Server PDW 中不支援。  
  
pdwtempdb  
**pdwtempdb**是儲存本機暫存資料表的資料庫。  
  
使用 SQL Server PDW 未實作暫存資料表**tempdb**資料庫。 相反地，PDW 將它們儲存在名為 pdwtempdb 的資料庫。 此資料庫存在每個計算節點上，而且看不到使用者已透過 PDW 介面。 在管理主控台中，在儲存體頁面上，您會看到這些些許的呼叫在 PDW 系統資料庫**tempdb sql**。  
  
tempdb  
**tempdb**是 SQL Server tempdb 資料庫。 它會使用最低限度記錄。 儲存過程中執行 SQL Server 作業需要的暫存資料表，SQL Server 會使用 tempdb 在計算節點上。  
  
SQL Server PDW 會從資料表卸除**tempdb**時：  
  
-   DROP TABLE 陳述式。  
  
-   工作階段已中斷連接。 只有工作階段暫存資料表會卸除。  
  
-   應用裝置是關機。  
  
-   控制節點擁有叢集容錯移轉。  
  
## <a name="general-remarks"></a>一般備註  
除非明確指定，否則，SQL Server PDW 執行暫存資料表和永久資料表相同的作業。 例如，本機暫存資料表，就像永久資料表中的資料是散發或在計算節點之間複寫。  
  
## <a name="LimitationsRestrictions"></a>限制事項  
限制 SQL Server PDW 上事項**tempdb**資料庫。 您*無法：*  
  
-   建立全域暫存資料表開頭為 # #。  
  
-   執行備份或還原**tempdb**。  
  
-   修改權限給**tempdb**與**GRANT**，**拒絕**，或**撤銷**陳述式。  
  
-   執行**DBCC SHRINKLOG**如**tempdb**tempdb。  
  
-   執行 DDL 作業**tempdb**。 有一些例外狀況。 如需詳細資訊，請參閱下列限制事項的清單上本機暫存資料表。  
  
限制事項本機暫存資料表上。 您*無法：*  
  
-   重新命名的暫存資料表  
  
-   在暫存資料表上建立資料分割、 檢視或非叢集索引。 **ALTER INDEX**可用來重建資料表，其中一個所建立的叢集的索引。  
  
-   修改權限到暫存資料表與 GRANT、 DENY 或 REVOKE 陳述式。  
  
-   暫存資料表上執行資料庫主控台命令。  
  
-   使用相同的批次內的兩個或多個暫存資料表相同的名稱。 如果批次內使用多個本機暫存資料表，則每一個都必須是唯一的名稱。 如果多個工作階段會執行相同的批次，並且建立了相同的本機暫存資料表，SQL Server PDW 在內部將數值後置詞附加到本機暫存資料表名稱，以維護每個本機暫存資料表的唯一名稱。  
  
> [!NOTE]  
> 您*可以*建立和更新暫存資料表上的統計資料。**ALTER INDEX**可用來重建叢集的索引。  
  
## <a name="permissions"></a>Permissions  
任何使用者都可以在 tempdb 中建立暫時物件。 除非收到其他權限，否則使用者只能存取自己的物件。 您可以撤銷 tempdb 的連接權限來阻止使用者使用 tempdb，不過不建議您這樣做，因為有些常式作業需要使用 tempdb。  
  
## <a name="RelatedTasks"></a>相關的工作  
  
|工作|Description|  
|---------|---------------|  
|中建立資料表**tempdb**。|您可以建立使用者的暫存資料表以 CREATE TABLE 和 CREATE TABLE AS SELECT 陳述式。 如需詳細資訊，請參閱[CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)和[CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)。|  
|檢視中的現有資料表的清單**tempdb**。|`SELECT * FROM tempdb.sys.tables;`|  
|檢視中的現有資料行的清單**tempdb**。|`SELECT * FROM tempdb.sys.columns;`|  
|檢視中的現有物件的清單**tempdb**。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
