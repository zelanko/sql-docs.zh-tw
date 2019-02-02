---
title: Analytics Platform System 的向外延展資料倉儲中最新消息
description: 請參閱什麼是 Microsoft Analytics Platform System 的新功能，擴充內部部署裝載 MPP SQL Server Parallel Data Warehouse 的設備。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3731f60047e22da7209b6c131ab93b28a20a99c2
ms.sourcegitcommit: c4870cb5bebf9556cdb4d8b35ffcca265fb07862
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652587"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Analytics Platform System，向外延展 MPP 資料倉儲中最新消息
請參閱什麼是最新的應用裝置更新 Microsoft Analytics Platform System (APS) 的新功能。 APS 是裝載 MPP SQL Server Parallel Data Warehouse 的向外延展內部部署設備。 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
發行日期為 2018 年 12 月

### <a name="common-subexpression-elimination"></a>共通子運算式刪除
APS CU7.3 可改善查詢效能，使用 SQL 查詢最佳化工具中的通用子運算式刪除。 改善可改善查詢有兩種。 第一個優點是能夠識別並排除這類運算式可以協助減少 SQL 編譯時間。 第二個和更重要的好處是這些多餘的子運算式的資料移動作業會刪除因此執行時間的查詢變得更快。 您可以找到這項功能的詳細的說明[此處](common-sub-expression-elimination.md)。

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>針對 Informatica 10.2.0 發行的 APS Informatica connector
我們已發行新版本的 Informatica 連接器搭配 Informatica 版 10.2.0 和 10.2.0 ap Hotfix 1。 您可以從下載新的連接器[下載網站](https://www.microsoft.com/download/details.aspx?id=57472)。

#### <a name="supported-versions"></a>支援的版本

| APS 版本 | Informatica powercenter 來 | 驅動程式 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 和更新版本 | 10.2.0、 10.2.0 Hotfix 1 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
發行日期為 2018 年 10 月

### <a name="support-for-tls-12"></a>Tls 1.2 支援
APS CU7.2 支援 TLS 1.2。 用戶端電腦 APS 和 APS 內部節點通訊現在可以設定只透過 tls 1.2 進行通訊。 SSDT、 SSIS 和安裝設定為只透過 TLS 1.2 通訊的用戶端電腦上的 Dwloader 之類的工具現在可以連線至 AP 使用 TLS 1.2。 根據預設，APS 會回溯相容性支援 TLS （1.0、 1.1 及 1.2） 的所有版本。 如果您想要設定為完全使用 TLS 1.2 AP 設備，則可以藉由變更登錄設定。 

如需詳細資訊，請參閱 < [AP 上設定 tls 1.2](configure-tls12-aps.md)。

### <a name="hadoop-encryption-zone-support-for-polybase"></a>PolyBase 支援 Hadoop 加密區域
現在 PolyBase 可以通訊 Hadoop 加密區域。 請參閱 APS 組態變更所需[設定 Hadoop 安全性](polybase-configure-hadoop-security.md#encryptionzone)。

### <a name="insert-select-maxdop-options"></a>Insert-select maxdop 選項
我們已新增[功能切換](appliance-feature-switch.md)，可讓您挑選大於 1 的 insert select 作業的 maxdop 設定。 您現在可以設定 maxdop 設定為 0、 1、 2 或 4。 預設值是 1。

> [!IMPORTANT]  
> 增加 maxdop 可能有時會導致較慢的作業或死結錯誤。 如果發生此情況，將設定變更回 maxdop 1，然後重試此作業。

### <a name="columnstore-index-health-dmv"></a>資料行存放區索引健全狀況 DMV
您可以檢視資料行存放區索引健全狀況資訊使用**dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv。 使用下列檢視，判斷片段，並決定何時要重建或重新組織資料行存放區索引。

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>PolyBase ORC 和 Parquet 檔案的日期範圍增加
讀取、 匯入和匯出現在使用 PolyBase 的日期資料類型支援的日期 1970年-01-01 之前和之後 2038年-01-20 ORC 和 Parquet 檔案類型。

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>SQL Server 2017 為目標的 SSIS 目的地配接器
新 AP SSIS 目的地配接器支援 SQL Server 2017，可以從下載部署目標[下載網站](https://www.microsoft.com/download/details.aspx?id=57472)。

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
發行日期為 2018 年 7 月

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC 命令不會取用的並行存取插槽 （行為變更）
APS 支援 T-SQL 子集[DBCC 命令](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql)這類[DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)。 這些命令之前，會耗用[並行存取插槽](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)減少使用者載入/查詢無法執行的數目。 `DBCC`現在會執行命令並不會耗用改善整體的查詢執行效能的使用者並行存取插槽的本機佇列中。

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>有些中繼資料的呼叫取代目錄物件
使用目錄物件，而不是使用 SMO 的中繼資料呼叫已顯示效能改善的 APS。 CU7.1 從開始，這些中繼資料呼叫的一些現在目錄物件，依預設使用。 可以關閉此行為由[功能切換](appliance-feature-switch.md)如果客戶使用中繼資料查詢時遇到任何問題。

### <a name="bug-fixes"></a>錯誤修正
我們已經升級至 SQL Server 2016 SP2 CU2 AP CU7.1 使用。 升級會修正一些問題，如下所述。

| 標題 | 描述 |
|:---|:---|
| **潛在的 tuple mover 死結** |升級分散式交易和 tuple mover 背景執行緒中的修正長久可能的死結。 安裝之後 CU7.1，用以 TF634 停止 tuple mover 為 SQL Server 啟動參數或全域追蹤旗標的客戶可以安全地移除它。 | 
| **某些 lag/lead 查詢失敗** |使用錯誤的巢狀的 lag/lead 函式的 CCI 資料表上的特定查詢現在已修正此升級。 | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
發行日期為 2018 年

APS 2016 是升級至 AU7 的必要條件。 以下是 AP AU7 的新功能：

### <a name="auto-create-and-auto-update-statistics"></a>自動建立 」 與 「 自動更新統計資料
APS AU7 建立，並根據預設，自動更新統計資料。 若要更新統計資料設定，系統管理員可以使用中的新功能切換功能表項目[Configuration Manager](appliance-configuration.md#CMTasks)。 [功能切換](appliance-feature-switch.md)控制 auto-create、 自動更新和非同步更新統計資料的行為。 您也可以更新使用統計資料設定[ALTER DATABASE （平行資料倉儲）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)陳述式。

### <a name="t-sql"></a>T-SQL
選取@var現在支援。 如需詳細資訊，請參閱[選取本機變數](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

現在支援雜湊和訂單群組的查詢提示。 如需詳細資訊，請參閱[Hints(Transact-SQL)-查詢 ](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>功能參數
APS AU7 導入了在功能切換[Configuration Manager](launch-the-configuration-manager.md)。 現在已可設定的選項，系統管理員可以變更的 AutoStatsEnabled 和 DmsProcessStopMessageTimeoutInSeconds。

### <a name="known-issues"></a>已知問題
APS AU7 軟體 Intel BIOS 更新會提供其描述為問題的修正*推測性執行旁路攻擊*。 攻擊的目標是要利用所謂*Spectre 與 Meltdown 弱點*。 雖然封裝以及 AP，手動安裝的 BIOS 更新，而不是 AP AU7 軟體安裝的一部分。

Microsoft 建議所有客戶安裝 BIOS 更新。 Microsoft 已在各種環境中的各種 SQL 工作負載來測量核心虛擬位址的遮蔽功能 (KVAS)、 核心分頁表間接取值 (KPTI) 和間接的分支預測風險降低 (IBP) 的效果。 測量結果找到某些工作負載顯著降低。 根據結果，建議您測試的效能影響，再將它們部署在生產環境中啟用 BIOS 更新。 請參閱 SQL Server 指導方針[此處](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)。

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
針對 APS 2016 AU6 這一節所述的新功能。

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 上最新的 SQL Server 2016 版本中，執行，並使用預設資料庫的相容性層級 130。 SQL Server 2016 可支援新的功能，例如：

- 叢集資料行存放區索引的次要索引。
- 針對 PolyBase Kerberos。

### <a name="t-sql"></a>T-SQL
APS AU6 支援這些 T-SQL 的相容性改進。  這些額外的語言項目，請從 SQL Server 和其他資料來源移轉的工作變得更容易。 

- [資料行層級 SQL 定序][]現已支援，除了 Windows 定序。
- [在叢集資料行存放區索引上的非叢集索引][]改善叢集資料行存放區索引中的特定值搜尋的查詢效能。 
- [SELECT...INTO][] 
- [sp_spaceused()][]顯示使用的磁碟空間，或保留在資料表或資料庫中。
- [寬型資料表][]支援是 SQL Server 2016 相同。 32k 的資料列大小先前的限制不存在。 

**資料類型**

- [VARCHAR(MAX)][]， [NVARCHAR(MAX)][]並[VARBINARY(MAX)][]。 這些 LOB 資料型別有大小上限為 2 GB。 若要將這些物件使用[bcp 公用程式][]。 PolyBase 和 dwloader 目前不支援這些資料類型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMERIC][]和十進位資料類型。

**視窗函式**

- [ROWS 或 RANGE][] OVER 子句的 SELECT 陳述式中。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**安全性函式**

- [CHECKSUM()][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**其他函式**

- [NEWID()][]
- [RAND()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 的增強功能

- Hortonworks HDP 2.4 版和 HDP 2.5 相容性
- Kerberos 支援透過資料庫範圍認證
- 使用 Azure 儲存體 Blob 的認證支援

### <a name="install-and-upgrade-enhancements"></a>安裝和升級的增強功能

**企業架構更新**AP AU6 來升級您現有的應用裝置安裝最新的韌體和驅動程式更新，其中包括安全性修正程式。 

新的裝置，從 HPE 或 DELL 包含所有最新的更新再加上：

- 最新的產生處理器支援 (Broadwell)
- 更新為搭載 DDR4 Dimm
- 改善的 DIMM 輸送量

**整合**

- 完整網域名稱 (FQDN) 支援讓您能夠設定到設備的網域信任。 
- 若要使用 FQDN，您需要執行完整的升級且在升級期間。 

**減少停機時間**安裝或升級至 AP AU6 的速度，而且需要較少的停機時間，比之前的版本。 若要減少停機時間、 安裝或升級： 

 - 簡化使用包含截至 2016 年 6 月的所有更新的映像套用 WSUS 更新
 - 套用安全性更新的驅動程式和韌體更新
 - 會最新的 hotfix 和設備驗證公用程式 (PAV) 放在您的應用裝置，讓它們準備好要安裝不需要下載它們。

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[資料行層級 SQL 定序]: ~/relational-databases/collations/collation-and-unicode-support.md

[在叢集資料行存放區索引上的非叢集索引]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR(MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARY(MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[寬型資料表]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 公用程式]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[NUMERIC]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[ROWS 或 RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NEWID()]:/sql/t-sql/functions/newid-transact-sql
[RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


