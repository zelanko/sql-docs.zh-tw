---
title: Tempdb 資料庫
description: 平行處理資料倉儲中的 Tempdb 資料庫。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3772e2b4cabac84c00854eba85f7a0c2a33d48bc
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400145"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>平行處理資料倉儲中的 tempdb 資料庫
**tempdb** 是 SQL Server PDW 系統資料庫，可儲存使用者資料庫的本機臨時表。 臨時表通常用來改善查詢效能。 例如，您可以使用臨時表來模組化腳本，並重複使用計算的資料。  
  
如需系統資料庫的詳細資訊，請參閱 [系統資料庫](system-databases.md)。  
  
## <a name="key-terms-and-concepts"></a><a name="Basics"></a>主要詞彙和概念  
*本機臨時表*  
*本機臨時表*使用資料表名稱前面的 # 前置詞，而且是本機使用者會話所建立的臨時表。 每個會話只能存取自己會話的本機臨時表中的資料。  
  
每個會話都可以在所有會話中查看本機臨時表的中繼資料。 例如，所有會話都可以使用查詢來查看所有本機臨時表的中繼資料 `SELECT * FROM tempdb.sys.tables` 。  
  
全域臨時表  
這一版的 SQL Server PDW 不支援使用 # # 語法 SQL Server 中支援的*全域臨時表*。  
  
pdwtempdb  
**pdwtempdb** 是儲存本機臨時表的資料庫。  
  
PDW 不會使用 SQL Server**tempdb** 資料庫來執行臨時表。 而是將其儲存在名為 pdwtempdb 的資料庫中。 此資料庫存在於每個計算節點上，且使用者透過 PDW 介面看不到此資料庫。 在管理主控台的 [儲存體] 頁面上，您會在名為 **[tempdb-sql**] 的 PDW 系統資料庫中看到這些資訊。  
  
tempdb  
**tempdb** 是 SQL Server 的 tempdb 資料庫。 它會使用基本記錄。 SQL Server 在計算節點上使用 tempdb，在執行 SQL Server 作業的過程中儲存所需的臨時表。  
  
在下列情況中，SQL Server PDW 會卸載 **tempdb** 的資料表：  
  
-   執行 DROP TABLE 語句。  
  
-   會話已中斷連線。 只會卸載會話的臨時表。  
  
-   設備已關閉。  
  
-   控制項節點有叢集容錯移轉。  
  
## <a name="general-remarks"></a>一般備註  
除非明確指定，否則 SQL Server PDW 會對臨時表和永久資料表執行相同的作業。 例如，本機臨時表中的資料就像永久資料表一樣，都是在計算節點之間散發或複寫。  
  
## <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a>限制事項  
SQL Server PDW**tempdb** 資料庫的限制。 您 *無法：*  
  
-   建立以 # # 開頭的全域臨時表。  
  
-   執行 **tempdb**的備份或還原。  
  
-   使用**GRANT**、 **DENY**或**REVOKE**語句來修改**tempdb**的許可權。  
  
-   針對**tempdb**Tempdb 執行**DBCC SHRINKLOG** 。  
  
-   在 **tempdb**上執行 DDL 作業。 有幾個例外狀況。 如需詳細資訊，請參閱下列有關本機臨時表的限制和限制清單。  
  
本機臨時表的限制和限制。 您 *無法：*  
  
-   重新命名臨時表  
  
-   在臨時表上建立資料分割、視圖或非叢集索引。 **ALTER INDEX** 可以用來重建使用一個建立之資料表的叢集索引。  
  
-   使用 GRANT、DENY 或 REVOKE 語句來修改臨時表的許可權。  
  
-   在臨時表上執行資料庫主控台命令。  
  
-   同一個批次中的兩個或多個臨時表，請使用相同的名稱。 如果在批次內使用超過一個本機暫存資料表，每個資料表都必須有唯一的名稱。 如果有多個會話執行相同的批次並建立相同的本機臨時表，SQL Server PDW 會在內部將數值尾碼附加至本機臨時表名稱，以維護每個本機臨時表的唯一名稱。  
  
> [!NOTE]  
> 您 *可以* 在臨時表上建立和更新統計資料。**ALTER INDEX** 可以用來重建叢集索引。  
  
## <a name="permissions"></a>權限  
任何使用者都可以在 tempdb 中建立暫時物件。 除非收到其他權限，否則使用者只能存取自己的物件。 您可以撤銷 tempdb 的連接權限來阻止使用者使用 tempdb，不過不建議您這樣做，因為有些常式作業需要使用 tempdb。  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a>相關工作  
  
|工作|描述|  
|---------|---------------|  
|在 **tempdb**中建立資料表。|您可以使用 CREATE TABLE 和 CREATE TABLE 做為 SELECT 語句來建立使用者臨時表。 如需詳細資訊，請參閱 [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) ，並 [CREATE TABLE 為 SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)。|  
|查看 **tempdb**中的現有資料表清單。|`SELECT * FROM tempdb.sys.tables;`|  
|查看 **tempdb**中現有資料行的清單。|`SELECT * FROM tempdb.sys.columns;`|  
|查看 **tempdb**中的現有物件清單。|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
