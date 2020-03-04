---
title: 資料表 | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server]
- table components [SQL Server]
ms.assetid: 82d7819c-b801-4309-a849-baa63083e83f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b59f204fafd7e1b912eea2673783290f67fa786
ms.sourcegitcommit: 92b2e3cf058e6b1e9484e155d2cc28ed2a0b7a8c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/25/2020
ms.locfileid: "77608518"
---
# <a name="tables"></a>資料表
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

資料表是資料庫物件，其中包含資料庫內所有的資料。 在資料表中，會以邏輯的方式將資料整理成資料列與資料行格式，這與試算表相似。 每個資料列都代表唯一的記錄，而每個資料行則代表記錄中的一個欄位。 例如，包含公司員工資料的資料表可能會包含每個員工的資料列，並以資料行來顯示員工資訊 (例如，員工編號、姓名、地址、工作職稱和住家電話號碼)。 

- 資料庫中的資料表數目只受限於資料庫中允許的物件數 (2,147,483,647)。 標準使用者定義的資料表最多可以有 1,024 個資料行。 資料表中的資料列數只受限於伺服器的儲存體容量。 

- 您可以將屬性指派給資料表或資料表中的每個資料行，以控制允許的資料和其他屬性。 例如，您可以在資料行上建立禁止 Null 值的條件約束，或在未指定值時提供預設值，也可以在資料表上指派強制唯一性的索引鍵條件約束，或是定義資料表之間的關聯性。 

- 資料表中的資料可以依資料列或頁面進行壓縮。 資料壓縮可以允許將更多的資料列儲存在頁面上。 如需詳細資訊，請參閱 [Data Compression](../../relational-databases/data-compression/data-compression.md)。 

## <a name="types-of-tables"></a>資料表的類型
 除了基本使用者定義資料表的標準角色之外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還提供在資料庫中具有特殊用途的下列資料表類型。 

### <a name="partitioned-tables"></a>分割區資料表

資料分割資料表的資料會水平劃分成數個單元，分散於資料庫中的多個檔案群組。 資料分割使大型資料表或索引的管理更為容易，這是因為您可以快速有效地存取或管理資料的子集，同時維持整體集合的完整性。 依預設， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 最多支援 15,000 個資料分割。 如需詳細資訊，請參閱＜ [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)＞。

### <a name="temporary-tables"></a>暫存資料表

暫存資料表儲存在 **tempdb**中。 暫存資料表有兩種：區域與全域。 它們在名稱、可見性和可用性方面有些差異。 本機暫存資料表是以單一數字符號 (#) 作為名稱的第一個字元；只有目前連接的使用者才能看見它們，當使用者中斷與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的連接時，就會刪除它們。 全域暫存資料表是以兩個數字符號 (##) 做為名稱的前兩個字元；只要一建立好，任何使用者都能看見它們，只有當所有參考這些資料表的使用者都中斷與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的連接時，才會刪除它們。 


#### <a name="ctp23"></a> 使用多個範圍的暫存資料表減少重新編譯工作負載

[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)] 在所有資料庫相容性層級下，使用多個範圍的暫存資料表來減少重新編譯工作負載。 也會針對所有部署模型，在 Azure SQL Database 的資料庫相容性層級 150 下啟用這項功能。  在此功能推出之前，使用資料操作語言 (DML) 陳述式 (`SELECT`、`INSERT`、`UPDATE`、`DELETE`) 參考暫存資料表時，若暫存資料表是由外部範圍批次建立的，便會導致在每一次執行陳述式時重新編譯 DML 陳述式。 透過這項改善，SQL Server 可執行額外的輕量檢查，避免不必要的重新編譯：

- 檢查在編譯時期用於建立暫存資料表之外部範圍模組是否與用於連續執行的模組相同。 
- 追蹤任何在初始編譯時進行的資料定義語言 (DDL) 變更，並將其與連續執行的 DDL 作業比較。

最終結果便是減少無關的重新編譯及 CPU 額外負荷。

### <a name="system-tables"></a>系統資料表

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將伺服器組態及其所有資料表的定義資料儲存在一組特殊資料表中，稱為系統資料表。 使用者不能直接查詢或更新系統資料表。 系統資料表中的資訊可透過系統檢視表取得。 如需詳細資訊，請參閱[系統檢視 &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)。 
 
### <a name="wide-tables"></a>寬型資料表

寬型資料表會使用 [疏鬆資料行](../../relational-databases/tables/use-sparse-columns.md) ，將資料表可以包含的資料行總數增加至 30,000。 疏鬆資料行為已最佳化儲存位置來保存 Null 值的一般資料行。 疏鬆資料行會減少 Null 值的空間需求，但要付出擷取非 Null 值的更多成本負擔。 寬型資料表已定義 [資料行集](../../relational-databases/tables/use-column-sets.md)，而資料行集是不具類型的 XML 表示，可將資料表的所有疏鬆資料行合併至結構化輸出中。 索引和統計資料的數目也會分別增加至 1,000 和 30,000。 寬型資料表資料列的大小上限為 8,019 個位元組。 因此，任何特定資料列中的大部分資料應該是 NULL。 在寬型資料表中，非疏鬆資料行加上計算資料行的數目上限仍然是 1,024。 

寬型資料表具有下列效能影響。

- 寬型資料表會增加維護資料表索引的成本。 我們建議寬型資料表的索引數目應該要限制為商務邏輯所需的索引。 當索引數目增加時，DML 編譯階段和記憶體需求也會增加。 非叢集索引應該是套用至資料子集的篩選索引。 如需詳細資訊，請參閱 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。 

- 應用程式可以用動態方式在寬型資料表中加入和移除資料行。 加入或移除資料行時，已編譯的查詢計畫也會失效。 我們建議您設計與預計工作負載相符的應用程式，以便盡可能減少結構描述變更。 

- 在寬型資料表中加入和移除資料時，效能可能會受到影響。 您必須針對預計的工作負載設計應用程式，以便盡可能減少對資料表資料所做的變更。 

- 針對寬型資料表，限制更新叢集索引鍵之多個資料列的 DML 陳述式執行。 這些陳述式可能會需要大量記憶體資源才能編譯和執行。 

- 寬型資料表的切換資料分割作業速度可能會降低，而且可能需要大量記憶體才能處理。 效能和記憶體需求會與來源和目標資料分割中的資料行總數成正比。 

- 在寬型資料表中更新特定資料行的更新資料指標應該在 FOR UPDATE 子句中明確列出這些資料行。 在您使用資料指標時，這有助於最佳化效能。 

## <a name="common-table-tasks"></a>一般資料表工作
 下表提供與建立或修改資料表相關聯之一般工作的連結。 

|資料表工作|主題|
|-----------------|-----------|
|描述如何建立資料表。|[建立資料表 &#40;Database Engine&#41;](../../relational-databases/tables/create-tables-database-engine.md)|
|描述如何刪除資料表。|[刪除資料表 &#40;Database Engine&#41;](../../relational-databases/tables/delete-tables-database-engine.md)|
|描述如何建立含有現有資料表之部分或所有資料行的新資料表。|[複製資料表](../../relational-databases/tables/duplicate-tables.md)|
|描述如何重新命名資料表。|[重新命名資料表 &#40;Database Engine&#41;](../../relational-databases/tables/rename-tables-database-engine.md)|
|描述如何檢視資料表的屬性。|[檢視資料表定義](../../relational-databases/tables/view-the-table-definition.md)|
|描述如何判斷其他物件 (例如檢視表或預存程序) 是否與資料表相依。|[檢視資料表的相依性](../../relational-databases/tables/view-the-dependencies-of-a-table.md)|

 下表提供與建立或修改資料表中資料行相關聯之一般工作的連結。 

|資料行工作|主題|
|------------------|-----------|
|描述如何將資料行加入現有資料表。|[將資料行新增至資料表 &#40;Database Engine&#41;](../../relational-databases/tables/add-columns-to-a-table-database-engine.md)|
|描述如何刪除資料表中的資料行。|[從資料表中刪除資料行](../../relational-databases/tables/delete-columns-from-a-table.md)|
|描述如何變更資料行的名稱。|[重新命名資料行 &#40;Database Engine&#41;](../../relational-databases/tables/rename-columns-database-engine.md)|
|描述如何將資料行從某個資料表複製到另一個資料表，但只複製資料行定義，或複製定義和資料。|[將資料行從一個資料表複製至另一個資料表 &#40;Database Engine&#41;](../../relational-databases/tables/copy-columns-from-one-table-to-another-database-engine.md)|
|描述如何透過變更資料類型或其他屬性來修改資料行定義。|[修改資料行 &#40;Database Engine&#41;](../../relational-databases/tables/modify-columns-database-engine.md)|
|描述如何變更資料行的顯示順序。|[變更資料表中的資料行順序](../../relational-databases/tables/change-column-order-in-a-table.md)|
|描述如何在資料表中建立計算資料行。|[指定資料表中的計算資料行](../../relational-databases/tables/specify-computed-columns-in-a-table.md)|
|描述如何指定資料行的預設值。 如果未提供其他值，則會使用此值。|[指定資料行的預設值](../../relational-databases/tables/specify-default-values-for-columns.md)|

## <a name="see-also"></a>另請參閱
 [主要與外部索引鍵條件約束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) [唯一條件約束與檢查條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md)


