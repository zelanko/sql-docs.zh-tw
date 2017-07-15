---
title: "已更新-關聯式資料庫文件 |Microsoft 文件"
description: "顯示更新的內容，如需關聯式資料庫的最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 06/30/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 19b664245f45ad45a4c7d1eba249858030fad718
ms.contentlocale: zh-tw
ms.lasthandoff: 07/03/2017

---
# 新的與最近的更新： 關聯式資料庫文件
<a id="new-and-recently-updated-relational-databases-docs" class="xliff"></a>



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017 年 05 月 17 日** &nbsp; 到 &nbsp; **2017 年 06 月 30 日**
- *主旨區域：* &nbsp; **關聯式資料庫**。




&nbsp;

## 最近建立的新文章
<a id="new-articles-created-recently" class="xliff"></a>

下列連結會跳至最近新增的新文章。


1. [SQL Server 2016 的 SQL Server 記憶體內部 OLTP 內部](in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016.md)
2. [SQL 資料庫中的彈性查詢處理](performance/adaptive-query-processing.md)
3. [增強的隱私權和定址 GDPR 需求與 Microsoft SQL 平台指南](security/microsoft-sql-and-the-gdpr-requirements.md)
4. [sys.dm_db_log_stats (Transact-SQL)](system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)
5. [sys.dm_exec_query_parallel_workers (Transact-SQL)](system-dynamic-management-views/sys-dm-exec-query-parallel-workers-transact-sql.md)



&nbsp;

## 更新的發行項、 只有摘要
<a id="updated-articles-with-excerpts" class="xliff"></a>

此區段會顯示更新從發行項的最近發生大規模的更新所收集的摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### 1.&nbsp;[改變記憶體最佳化資料表](in-memory-oltp/altering-memory-optimized-tables.md)
<a id="1-nbsp-altering-memory-optimized-tablesin-memory-oltpaltering-memory-optimized-tablesmd" class="xliff"></a>

*Updated: 2017-06-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 82.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 8359700b5db24838f1bb273526794c2865bbbe11 41d77cf0bbcf53a1b64d6524a24e5736c5a073da  (PR=2171  ,  Filename=altering-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**記憶體最佳化資料表上的 ALTER TABLE 記錄**

在記憶體最佳化資料表上，大部分的 ALTER TABLE 案例現在會以平行方式執行，並導致對交易記錄的寫入最佳化。 只有將中繼資料變更記錄到交易記錄檔才能達到最佳化。 不過，下列 ALTER TABLE 作業會以單一執行緒執行，而且不會進行記錄檔最佳化。

本例中的單一執行緒作業會將已改變的資料表完整內容記錄到交易記錄檔。 單一執行緒的作業清單如下︰

- 改變或新增資料行以使用大型物件 (LOB) 類型︰nvarchar(max)、varchar(max) 或 varbinary(max)。

- 加入或卸除資料行存放區索引。

- 幾乎所有會影響 [off-row column--../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md) 的項目。

    - 導致 on-row 資料行移到 off-row。

    - 導致 off-row 資料行移到 on-row。

    - 建立新的 off-row 資料行。

    - *例外狀況︰* 會以最佳化方式記錄使已經 off-row 的資料行變長的情況。 
  




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### 2.&nbsp;[記憶體最佳化資料表中的資料表和資料列大小](in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)
<a id="2-nbsp-table-and-row-size-in-memory-optimized-tablesin-memory-oltptable-and-row-size-in-memory-optimized-tablesmd" class="xliff"></a>

*Updated: 2017-06-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 114.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 27ce0fa2e7bb464f9c3d6e32dd195de3b79abfcd 0a3cacd86024e2b734704ffd37e55ca0b17a0c94  (PR=2163  ,  Filename=table-and-row-size-in-memory-optimized-tables.md  ,  Dirpath=docs\relational-databases\in-memory-oltp\  ,  MergeCommitSha40=fe6de2b16b9792a5399b1c014af72a2a5ee52377) -->



 
  
 下表中討論 [資料列主體大小] 的計算。  
  
 資料列主體大小有兩種不同的計算方式，也就是計算的大小和實際大小：  
  
-   計算的大小以 [計算的資料列主體大小] 表示，用於判斷是否超過 8,060 個位元組的資料列大小限制。  
  
-   實際大小以 [實際資料列主體大小] 表示，是資料列主體在記憶體中和檢查點檔案中的實際儲存體大小。  
  
 [計算的資料列主體大小] 和 [實際資料列主體大小] 兩者的計算方式十分類似。 唯一的差異在於 (n)varchar(i) 和 varbinary(i) 資料行大小的計算，如下列資料表底部所反映。 計算的資料列主體大小使用宣告的大小 *i* 作為資料行的大小，而實際的資料列主體大小使用實際的資料大小。  
  
 下表描述資料列主體大小的計算，指定為 [實際資料列主體大小] = SUM([淺層類型的大小]) + 2 + 2 * [深層類型資料行數目]。  
  
|章節|大小|註解|  
|-------------|----------|--------------|  
|淺層類型資料行|SUM([淺層類型的大小])。 個別類型的大小如下所示 (以位元組為單位)：<br /><br /> **Bit**：1<br /><br /> **Tinyint**：1<br /><br /> **Smallint**：2<br /><br /> **Int**：4<br /><br /> **Real**：4<br /><br /> **Smalldatetime**：4<br /><br /> **Smallmoney**：4<br /><br /> **Bigint**：8<br /><br /> **Datetime**：8<br /><br /> **Datetime2**：8<br /><br /> **Float**：8<br /><br /> **Money**：8<br /><br /> **Numeric** (precision <=18)：8<br /><br /> **Time**：8<br /><br /> **Numeric**(precision>18)：16<br /><br /> **Uniqueidentifier**：16||  
|淺層資料行填補|可能的值為：<br /><br /> 如果有深層類型資料行且淺層資料行的資料大小總計為奇數，則為 1。<br /><br /> 否則為 0|深層類型是指 (var)binary 和 (n)(var)char 類型。|  




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### 3.&nbsp;[移轉後驗證和最佳化指南](post-migration-validation-and-optimization-guide.md)
<a id="3-nbsp-post-migration-validation-and-optimization-guidepost-migration-validation-and-optimization-guidemd" class="xliff"></a>

*Updated: 2017-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2) | [Next](#TitleNum_4))

<!-- Source markdown line 27.  ms.author= "harinid".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 faa2e3dd8be3aeb475bf8c7f71617ebf17969892 f2760dfecda10baeb121929b72a4d8164e81185b  (PR=2126  ,  Filename=post-migration-validation-and-optimization-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=dcbeda6b8372b358b6497f78d6139cad91c8097c) -->



以下是移轉至 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 平台後常發生的效能案例以及解決方法。 這些案例包含 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 移轉至 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 的特有案例 (舊版移轉至新版)，以及外部平台 (如 Oracle、DB2、MySQL 和 Sybase) 移轉至 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]。

**<a name="CEUpgrade"></a>因為 CE 版本變更造成的查詢衰退**


**適用於：** [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 移轉至 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)]。

從舊版 [!INCLUDE[ssNoVersion--../includes/ssnoversion-md.md)] 移轉至 [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] 或更新版本，以及從 [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 升級到最新版本時，工作負載可能有效能衰退的風險。

這是因為從 [!INCLUDE[ssSQL14--../includes/sssql14-md.md)] 開始，所有的查詢最佳化工具變更都會繫結至最新的 [database compatibility level--../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)；因此，計劃不會在升級時立即變更，而是在使用者將 `COMPATIBILITY_LEVEL` 資料庫選項變更為最新版本時變更。 此功能會結合查詢存放區，可讓您在升級過程中對查詢效能擁有絕佳層級的控制。 

如需 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 所導入的查詢最佳化工具變更的詳細資訊，請參閱[使用 SQL Server 2014 基數估算程式最佳化您的查詢計劃](http://msdn.microsoft.com/library/dn673537.aspx)。




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### 4. &nbsp; [sys.query_store_plan (Transact-SQL)](system-catalog-views/sys-query-store-plan-transact-sql.md)
<a id="4-nbsp-sysquerystoreplan-transact-sqlsystem-catalog-viewssys-query-store-plan-transact-sqlmd" class="xliff"></a>

*Updated: 2017-06-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_3) | [Next](#TitleNum_5))

<!-- Source markdown line 58.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1b77e34309ba7033578b3c82ed83c8c2fbc93e24 ce4ade9ab906c35cb87068a1fb91c4e1d7549aac  (PR=1940  ,  Filename=sys-query-store-plan-transact-sql.md  ,  Dirpath=docs\relational-databases\system-catalog-views\  ,  MergeCommitSha40=1d363db8e8bd0e1460cdea3c3a7add68e48714c9) -->



**強制執行計劃的限制**

查詢存放區有強制查詢最佳化工具使用特定執行計劃的機制。 不過，也有避免強制執行計劃的一些限制。 

首先，如果計劃包含下列建構：
* INSERT BULK 陳述式。
* INSERT BULK 陳述式。
* 參考外部資料表
* 分散式查詢或全文檢索作業
* 使用全域查詢 
* 資料指標
* 無效的星型聯結規格 

其次，無法再使用計劃依賴的物件時：
* 資料庫 (如果計劃的來源資料庫不再存在)
* 索引 (不再存在或停用)

最後，計劃本身的問題：
* 查詢不合法
* 查詢最佳化工具超過允許的作業數目
* 計劃 XML 格式不正確




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### 5.&nbsp;[管理的系統版本設定時態表中的歷程記錄資料保留](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
<a id="5-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd" class="xliff"></a>

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_4))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b  (PR=1777  ,  Filename=manage-retention-of-historical-data-in-system-versioned-temporal-tables.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



**使用時態歷程記錄保留原則方法**

> **注意：**時態歷程記錄保留原則的方法適用於 [！包含 [sqldbesa../../includes/sqldbesa-md.md)] 和 SQL Server 2017 從 CTP 1.3 開始。  

可以是時態歷程記錄保留在個別的資料表層級的設定，可讓使用者建立彈性的過時原則。 套用暫時保留很簡單： 它只需要一個參數是在資料表建立或結構描述變更時設定。

定義保留原則之後，Azure SQL Database 會啟動定期檢查是否有資格可自動清除資料的歷程記錄資料列。 相符的資料列的識別和歷程記錄資料表中的移除它們發生背景工作，排程及執行系統中的透明的方式。 歷程記錄資料表資料列的存留期條件檢查會根據表示一端的 SYSTEM_TIME 期間資料行。 保留期限，例如，設定為六個月內，如果資料表有資格清除的資料列滿足下列條件：
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
在上述範例中，我們假設 ValidTo 資料行對應至 SYSTEM_TIME 週期的結尾。
**如何設定保留原則？**

設定的時態表的保留原則之前，請先檢查是否啟用時態歷程記錄保留在資料庫層級：
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
資料庫旗標**is_temporal_history_retention_enabled**設為 ON，根據預設，但使用者可以變更利用 ALTER DATABASE 陳述式。 它也會自動設為 OFF 之後的時間還原作業中的點。 若要啟用時態歷程記錄保留為清除，為您的資料庫，請執行下列陳述式：





&nbsp;

<a name="compactupdatedlist"/>

## Compact 文件最近才更新清單
<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

此壓縮清單所提供的所有更新發行項上一節中所列的連結。

1. [改變記憶體最佳化資料表](#TitleNum_1)
2. [記憶體最佳化資料表中的資料表和資料列大小](#TitleNum_2)
3. [移轉後驗證和最佳化指南](#TitleNum_3)
4. [sys.query_store_plan (Transact-SQL)](#TitleNum_4)
5. [管理系統設定版本時態表中的歷程記錄資料保留](#TitleNum_5)




<a name="sisters2"/>

&nbsp;

## 姊文件
<a id="sister-articles" class="xliff"></a>

本節會在 GitHub 儲存機制中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/)。

<!--  20170630-1150  -->

#### 具有新文章或最近更新文章的主題區
<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

- [新文章 + 更新文章 (12+2)：**SQL 進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+2)：**連接到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (3+0)：**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (1+2)：**Integration Services for SQL** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (2+8)：**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (1+0):  **Master Data Services (MDS) for SQL** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (5+5)：**SQL 關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (2+0)：**Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+4)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (1+0)：**SQL 工具**文件](../tools/new-updated-tools.md)


#### 沒有新文章或最近更新文章的主題區
<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


&nbsp;


