---
title: 新功能
description: 查看 Microsoft 分析平台系統中新增功能,這是託管 MPP SQL Server 並行數據倉庫的橫向擴展本地設備。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: faf3bd1f487fb5c850759fdde3ddecd32bdd3b1f
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625545"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>分析平台系統(橫向延伸 MPP 資料倉儲)中的新增功能
查看 Microsoft 分析平台系統 (APS) 的最新設備更新中的新增功能。 APS 是託管 MPP SQL Server 並行數據倉庫的橫向擴展本地設備。 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.6"></a>
## <a name="aps-cu76"></a>APS CU7.6
發佈日期 - 2020 年 4 月

### <a name="rename-column"></a>重新命名資料行
升級到 CU7.6 後,客戶將能夠重新命名使用者創建的表的欄。 有關語法、範例、限制和詳細資訊,請參閱[RENAME(轉用 SQL)。](https://docs.microsoft.com/sql/t-sql/statements/rename-transact-sql)

### <a name="alter-view"></a>變更檢視
客戶現在將能夠更改檢視。 有關詳細資訊,請參閱[ALTER 檢視(轉用 SQL)。](https://docs.microsoft.com/sql/t-sql/statements/alter-view-transact-sql)

<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
發佈日期 - 2019 年 9 月

### <a name="alter-external-data-source"></a>變更外部資料來源
客戶將能夠使用 CU7.5 更新更改外部數據來源定義。 具有 Hadoop 名稱節點高可用性的客戶現在可以更改數據源,以在發生故障轉移時更改參數。 對於 APS,只能更改位置、RESOURCE_MANAGER_LOCATION和憑據。 有關詳細資訊,請參閱[變更外部資料來源](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017)。

### <a name="cdh-515-and-516-support-with-polybase"></a>CDH 5.15 和 5.16 支援 PolyBase
具有 CU7.5 更新的 APS 上的 PolyBase 現在支援來自 Cloudera 的 CDH 5.15 和 5.16 版本的 Hadoop 發行版。 對 CDH 5.x 版本使用選項 6。 

### <a name="try_convert-and-try_cast-support"></a>Try_Convert和Try_Cast支援
CU7.5 APS 現在支援[TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017)和[tsql函數TRY_CONVERT。](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) 如果轉換成功,這兩個函數都將返回轉換為指定數據類型的值;否則,返回 null。

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
發佈日期 - 2019 年 5 月

### <a name="loading-large-rows-with-dwloader"></a>使用 dwloader 載入大型行
從 APS CU7.4 開始,客戶將能夠使用新的 dwloader 將行載入到大於 32 KB(32,768 位元組)的表中。 新的 dwloader 支援 -l 開關,該開關採用 32768 和 33554432(以位元組為單位)之間的整數值來載入大於 32 KB 的行。 僅當載入大型行(大於 32 KB)時才使用此選項,因為此交換機將在用戶端和伺服器上分配更多記憶體,並可能降低負載。 你可以從[下載網站](https://www.microsoft.com/download/details.aspx?id=57472)下載新的dwloader。  

### <a name="hdp-30-and-31-support-with-polybase"></a>使用 PolyBase 支援 HDP 3.0 和 3.1
APS 上的 PolyBase 現在支援 HDP 3.0 和 3.1 此更新。 對 HDP 3.x 版本使用選項 7。 有關詳細資訊,請參閱[PolyBase 連接](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql)頁。

### <a name="utf16-file-support-with-polybase"></a>UTF16 檔案支援與 PolyBase
PolyBase 現在支援讀取 UTF16 (LE) 編碼中分隔的文本檔。 有關設定詳細資訊,請參考[外部檔案格式](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql)。 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
發佈日期 - 2018 年 12 月

### <a name="common-subexpression-elimination"></a>共通子運算式刪除
APS CU7.3 透過在 SQL 查詢最佳化器中消除常見子運算式來提高查詢性能。 改進以兩種方式改進查詢。 第一個好處是能夠識別和消除此類運算式,這有助於縮短 SQL 編譯時間。 第二個更重要的好處是消除了這些冗餘子表達式的數據移動操作,從而加快了查詢的執行時間。 有關此功能的詳細說明,請參閱[此處](common-sub-expression-elimination.md)。

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>APS 資訊學連接器 Informatica 10.2.0 發佈
我們發佈了適用於 Informatica 版本 10.2.0 和 10.2.0 修補程式 1 的 APS 的新版本 Informatica 連接器。 新的連接器可以從[下載網站](https://www.microsoft.com/download/details.aspx?id=57472)下載。

#### <a name="supported-versions"></a>支援的版本

| APS 版本 | Informatica PowerCenter | 驅動程式 |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL 伺服器本機客戶端 11.x |
| APS 2016 及更高版本 | 10.2.0, 10.2.0 修補程式 1 | SQL 伺服器本機客戶端 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
發佈日期 - 2018 年 10 月

### <a name="support-for-tls-12"></a>支援 TLS 1.2
APS CU7.2 支援 TLS 1.2。 用戶端計算機到 APS 和 APS 節點內通信現在只能設置為透過 TLS1.2 進行通訊。 安裝在用戶端電腦上(設置為僅透過 TLS 1.2 進行通訊)的 SSDT、SSIS 和 Dwloader 等工具現在可以使用 TLS 1.2 連接到 APS。 默認情況下,APS 將支援所有 TLS(1.0、1.1 和 1.2)版本,以便向後相容。 如果您希望將 APS 設備設置為嚴格使用 TLS 1.2,則可以通過更改註冊表設置來執行此操作。 

有關詳細資訊,請參閱在[APS 上配置 TLS1.2。](configure-tls12-aps.md)

### <a name="hadoop-encryption-zone-support-for-polybase"></a>對 PolyBase 的 Hadoop 加密區域支援
PolyBase 現在可以與 Hadoop 加密區域進行通信。 請參閱[配置 Hadoop 安全性](polybase-configure-hadoop-security.md#encryptionzone)中所需的 APS 配置更改。

### <a name="insert-select-maxdop-options"></a>插入-選擇最大多普選項
我們添加了一個[功能開關](appliance-feature-switch.md),允許您選擇大於 1 的 maxdop 設置,用於插入選擇操作。 現在,您可以將 maxdop 設置設置為 0、1、2 或 4。 預設值是 1。

> [!IMPORTANT]  
> 增加 maxdop 有時可能會導致操作速度較慢或死鎖錯誤。 如果發生這種情況,請將設置更改回 maxdop 1 並重試該操作。

### <a name="columnstore-index-health-dmv"></a>列儲存索引執行狀況 DMV
您可以使用**dm_pdw_nodes_db_column_store_row_group_physical_stats** dmv 查看列儲存索引運行狀況資訊。 使用以下檢視確定碎片並決定何時重新生成或重新組織列存儲索引。

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

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>ORC 與 Parquet 檔案的 PolyBase 日期範圍增加
使用 PolyBase 讀取、導入和匯出日期數據類型現在支援 ORC 和 Parquet 檔案類型的 1970-01-01 和 2038-01-20 之後的日期。

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>SQL Server 2017 的 SSIS 目標配接器作為目標
新的APS SSIS目標適配器,支援SQL Server 2017作為部署目標可以從[下載網站](https://www.microsoft.com/download/details.aspx?id=57472)下載。

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
發佈日期 - 2018 年 7 月

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>DBCC 指令不消耗併發槽(行為更改)
APS 支援 T-SQL [DBCC 指令](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql)的子集,如[DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql)。 之前，這些命令會耗用[並行位置](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots)，減少可執行的使用者載入/查詢數量。 這些`DBCC`命令現在在本地佇列中運行,這些佇列不使用使用者併發槽來提高整體查詢執行性能。

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>將某些中繼資料呼叫取代為目錄物件
將目錄物件用於中繼資料調用而不是使用 SMO 在 APS 中顯示了性能改進。 從 CU7.1 開始,這些元數據調用中的一些預設使用目錄物件。 如果使用元數據查詢的客戶遇到任何問題,則[功能切換](appliance-feature-switch.md)可以關閉此行為。

### <a name="bug-fixes"></a>錯誤修正
我們已升級到 SQL Server 2016 SP2 CU2 與 APS CU7.1。 升級修復了下面描述的一些問題。

| Title | 描述 |
|:---|:---|
| **潛在的元組前鎖死** |升級修復了分散式事務和元組器後台線程中長期存在的死鎖的可能性。 安裝 CU7.1 後,使用 TF634 停止元組器作為 SQL Server 啟動參數或全域追蹤標誌的客戶可以安全地將其刪除。 | 
| **某些延遲/潛在顧客查詢失敗** |對於具有嵌套滯後/潛在顧客函數的 CCI 表的某些查詢,這些查詢會出錯,現在通過此升級修復了這些查詢。 | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
發佈日期 - 2018 年 5 月

APS 2016 是升級到 AU7 的先決條件。 以下是 APS AU7 中的新功能:

### <a name="auto-create-and-auto-update-statistics"></a>自動建立與自動更新統計資訊
默認情況下,APS AU7 會自動創建和更新統計資訊。 要更新統計資訊設置,管理員可以使用[配置管理器](appliance-configuration.md#CMTasks)中的新功能切換功能表項。 [要素開關](appliance-feature-switch.md)控制統計資訊的自動創建、自動更新和非同步更新行為。 您還可以使用[ALTER 資料庫(並行數據倉庫)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)語句更新統計資訊設置。

### <a name="t-sql"></a>T-SQL
現在@var支援選擇。 有關詳細資訊,請參閱[選擇局部變數](/sql/t-sql/language-elements/select-local-variable-transact-sql) 

查詢提示 HASH 和 ORDER 組現在受支援。 有關詳細資訊,請參閱[提示(轉算 SQL) - 查詢](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>功能開關
APS AU7 在[配置管理器](launch-the-configuration-manager.md)中引入了功能切換。 啟用自動統計和 DmsProcessStopMessageTimeoutIn,現在它們是可配置的選項,管理員可以更改這些選項。

### <a name="known-issues"></a>已知問題
使用 APS AU7 軟體,提供了英特爾 BIOS 更新,修復了被描述為*投機性執行側通道攻擊*的問題。 攻擊的目的是利用所謂的*幽靈和熔毀漏洞*。 儘管與 APS 一起打包,但 BIOS 更新是手動安裝的,而不是作為 APS AU7 軟體安裝的一部分。

微軟建議所有客戶安裝更新的 BIOS。 Microsoft 已測量內核虛擬位址陰影 (KVAS)、內核頁錶間接 (KPTI) 和間接分支預測緩解 (IBP) 對各種環境中各種 SQL 工作負載的影響。 測量發現某些工作負載顯著退化。 根據結果,建議在生產環境中部署 BIOS 更新之前測試啟用 BIOS 更新的性能效果。 [在此處](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown)查看 SQL Server 指南。

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
本節介紹了 APS 2016-AU6 的新功能。

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 在最新的 SQL Server 2016 版本上運行,並使用默認資料庫相容性級別 130。 SQL Server 2016 支援新功能,例如:

- 群集列存儲索引的輔助索引。
- 多基的 Kerberos。

### <a name="t-sql"></a>T-SQL
APS AU6 支援這些 T-SQL 相容性改進。  這些附加語言元素使從 SQL Server 和其他數據源遷移變得更加容易。 

- 除了 Windows 排序規則之外,現在還支援[列級 SQL 排序規則][]。
- [群集列存儲索引上的非群集索引][]可提高搜索群集列存儲索引中特定值的查詢的性能。 
- [SELECT...INTO][] 
- [sp_spaceused()][]顯示表或資料庫中使用或保留的磁碟空間。
- [寬表][]支援與 SQL Server 2016 相同。 行大小的前一個限制為 32 K 不再存在。 

**資料類型**

- [瓦爾查爾(最大值][][)、NVARCHAR(MAX)][]和[瓦爾里卡(MAX)。][] 這些 LOB 資料類型的最大大小為 2 GB。 要載入這些物件,請使用[bcp 實用程式][]。 PolyBase 和 dwloader 目前不支援這些數據類型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [數位][]和 DECIMAL 資料類型。

**視窗函式**

- SELECT 語句 OVER 子句中的[行或範圍][]。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**安全功能**

- [CHECKSUM()][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**其他功能**

- [紐ID()][]
- [蘭德()][]

### <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 增強功能

- 與霍頓工程 HDP 2.4 和 HDP 2.5 相容
- 以資料庫範圍使用網域的支援 Kerberos
- 使用 Azure 儲存 Blob 提供認證

### <a name="install-and-upgrade-enhancements"></a>安裝並升級增強功能

**企業結構更新**將現有設備升級到 APS AU6 可安裝最新的韌體和驅動程式更新,其中包括安全修補程式。 

HPE 或 DELL 的新裝置包括所有最新更新以及:

- 最新一代處理器支援(布羅德韋爾)
- 更新到 DDR4 DIMM
- 改進的 DIMM 輸送量

**整合**

- 完全限定的功能變數名稱 (FQDN) 支援使得可以設置對設備的域信任。 
- 要使用 FQDN,您需要在升級期間執行完全升級並加入加入。 

**減少停機時間**安裝或升級到 APS AU6 的速度更快,並且需要的停機時間比以前的版本要少。 為了減少停機時間,安裝或升級: 

 - 使用包含所有更新的映像在 2016 年 6 月內簡化應用 WSUS 更新
 - 使用驅動程式和韌體更新應用安全更新
 - 將最新的修補程式和產品驗證實用程式 (PAV) 放在設備上,以便無需下載即可安裝。

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[欄位 SQL 排序規則]: ~/relational-databases/collations/collation-and-unicode-support.md

[叢集列儲存索引上的非叢集索引]:/sql/t-sql/statements/create-index-transact-sql
[瓦爾查爾(最大)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[恩瓦爾查爾(最大)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[瓦里卡(最大)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[SYSNAME]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[寬桌]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[bcp 公用程式]:/sql/tools/bcp-utility
[UNIQUEIDENTIFIER]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[公尺]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[行或範圍]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[驗證()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[紐ID()]:/sql/t-sql/functions/newid-transact-sql
[蘭德()]:/sql/t-sql/functions/rand-transact-sql


  

  


