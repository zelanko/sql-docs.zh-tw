---
title: "已更新 - 關聯式資料庫文件 | Microsoft Docs"
description: "針對關聯式資料庫，顯示文件最新變更之已更新內容的程式碼片段。"
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
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: 1fbc7affa833eb34b6e13e28b229d47ac0b05a5c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的與最近更新的文章： 關聯式資料庫文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp; **2017-09-28** &nbsp; 到 &nbsp; **2017-12-02**
- *主旨區域：* &nbsp; **關聯式資料庫**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [使用 SSMS XEvent 分析工具](extended-events/use-the-ssms-xe-profiler.md)
2. [將一般檔案匯入 SQL 精靈](import-export/import-flat-file-wizard.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [tempdb 資料庫](#TitleNum_1)
2. [記憶體管理架構指南](#TitleNum_2)
3. [統計資料](#TitleNum_3)
4. [sp_server_diagnostics (Transact-SQL)](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>1. &nbsp; [tempdb 資料庫](databases/tempdb-database.md)

*更新日期：2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 121.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c8bb5f9c40625aaf955295e5b5d03e4257e6c6b 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d  (PR=4039  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=ef1fa818beea435f58986af3379853dc28f5efd8) -->



**最佳化 tempdb 效能**

 tempdb 資料庫的大小和實體位置會影響系統效能。 例如，如果為 tempdb 定義的大小太小，每次您重新啟動 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 的執行個體時，部分的系統處理負載可能會開始將 tempdb 自動成長到支援工作負載所需的大小。

 可能的話，請使用[資料庫立即檔案初始化--../../relational-databases/databases/database-instant-file-initialization.md)來改善資料檔成長作業的效能。

 您可將檔案大小設定為夠大的值來容納環境中的典型工作負載，藉此為所有 tempdb 檔案預先配置空間。 這防止 tempdb 擴充過於頻繁而影響效能。 tempdb 資料庫應該設為自動成長，但這應該用來增加非計畫中例外狀況的磁碟空間。

 資料檔案應該在每個[檔案群組--../../relational-databases/databases/database-files-and-filegroups.md#filegroups) 內具有相同大小，因為 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 使用依比例填滿演算法，此法喜好在具有更多可用空間的檔案中進行配置。 將 tempdb 分割成相同大小的多個資料檔案時，可讓使用 tempdb 的作業具有較高的平行效率。

 將檔案成長增量設成合理的大小，可避免 tempdb 資料庫檔案每次成長量的值太小。 如果檔案的成長比寫入 tempdb 的資料量少太多，那麼 tempdb 可能必須經常擴大。 這樣會影響效能。

 若要檢查目前的 tempdb 大小和成長參數，請使用下列查詢：
```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeinMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-memory-management-architecture-guidememory-management-architecture-guidemd"></a>2.&nbsp;[記憶體管理架構指南](memory-management-architecture-guide.md)

*更新日期：2017-11-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1) | [下一個](#TitleNum_3))

<!-- Source markdown line 75.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 dd47431ca47eab16af40e41adaeeaf3fc5fb7461 445f013af3bdad65dd3eaf837db7f744b43e8f97  (PR=4113  ,  Filename=memory-management-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



在舊版的 SQL Server (..!NCLUDE-NotShown--ssVersion2005--../includes/ssversion2005-md.md)]、..!NCLUDE-NotShown--ssKatmai--../includes/ssKatmai-md.md)] 和 ..!NCLUDE-NotShown--ssKilimanjaro--../includes/ssKilimanjaro-md.md)]) 裡，記憶體配置使用五種不同的機制來完成：
-  **單一頁面配置器 (SPA)**，在 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 處理序中只包含少於或等於 8 KB 的記憶體配置。 [最大伺服器記憶體 (MB)] 與 [最小伺服器記憶體 (MB)] 設定選項決定了 SPA 可取用的實體記憶體上限。 緩衝集區同時是 SPA 的機制，以及單一分頁配置的最大取用者。
-  **多頁配置器 (MPA)**，適用於要求超過 8KB 的記憶體配置。
-  **CLR 配置器**，包括 SQL CLR 堆積，及其在 CLR 初始化期間所建立的全域配置。
-  ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 處理序中的**[執行緒堆疊--../relational-databases/memory-management-architecture-guide.md#stacksizes)** 記憶體配置。
-  **直接 Windows 配置 (DWA)**，適用於直接向 Windows 提出的記憶體配置要求。 這些包括使用 Windows 堆積，以及載入至 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 處理序之模組所做的直接虛擬配置。 這類的記憶體配置要求範例，包括擴充預存程序 DLL 的配置、使用「自動」處理序 (sp_OA 呼叫) 所建立的物件，以及連結伺服器提供者的配置。

從 ..!NCLUDE-NotShown--ssSQL11--../includes/sssql11-md.md)] 開始，單頁配置、多頁配置及 CLR 配置皆一併整合為「任何大小」分頁配置器，且包含在 [最大伺服器記憶體 (MB)] 及 [最小伺服器記憶體 (MB)] 設定選項所控制的記憶體限制之中。 這些變更為經由 ..!NCLUDE-NotShown--ssNoVersion--../includes/ssnoversion-md.md)] 記憶體管理員的所有記憶體需求，提供了更準確的調整大小功能。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-statisticsstatisticsstatisticsmd"></a>3.&nbsp; [統計資料](statistics/statistics.md)

*更新日期：2017-11-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_2) | [下一個](#TitleNum_4))

<!-- Source markdown line 48.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1dbe3bd6fdfcd27cf4a597cac5a4a09821b51ba7 971cfccf75fbc8842a0ef020a2bc93992c5f4ad9  (PR=4087  ,  Filename=statistics.md  ,  Dirpath=docs\relational-databases\statistics\  ,  MergeCommitSha40=9fbe5403e902eb996bab0b1285cdade281c1cb16) -->



> [!NOTE]
> ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 中的長條圖只針對單一資料行而建置ΓÇö統計資料物件索引鍵資料行集合中的第一個資料行。

若要建立長條圖，查詢最佳化工具會排序資料行值、計算符合每一個相異資料行值的值數目，然後將資料行值彙總成最多 200 個連續長條圖步驟。 每一個長條圖步驟都包含某個範圍的資料行值，後面緊接著上限資料行值。 此範圍包括界限值之間的所有可能資料行值，但是不包括界限值本身。 最低的已排序資料行值就是第一個長條圖步驟的上限值。

更詳細地說，..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 會以三個步驟從資料行值的已排序集合建立**長條圖**：

- **長條圖初始化**：第一個步驟會從已排序的集合開頭處理一連串的值，並收集最多 200 個 *range_high_key*、*equal_rows*、*range_rows* 和 *distinct_range_rows* 的值 (在此步驟中，*range_rows* 和 *distinct_range_rows* 一定是零)。 當所有的輸入都已用完，或已找到 200 個值時，就會結束第一個步驟。
- **使用貯體合併掃描**：第二個步驟會依順序處理統計資料索引鍵之前置資料行的每一個額外值；每個後續的值可以新增到最後一個範圍，或在結束時建立新的範圍 (由於輸入的值會排序，因此這是可行的)。 建立新的範圍時，會將現有的一組相鄰範圍摺疊成單一範圍。 系統會選取這一組範圍，以將資訊遺失的機率降至最低。 此方法會使用「最大差異」演算法，讓長條圖中的步驟數減至最少，同時讓界限值之間的差異最大化。 在這整個步驟期間，範圍摺疊之後的步驟數目仍然為 200。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-spserverdiagnostics-transact-sqlsystem-stored-proceduressp-server-diagnostics-transact-sqlmd"></a>4. &nbsp; [sp_server_diagnostics (Transact-SQL)](system-stored-procedures/sp-server-diagnostics-transact-sql.md)

*更新日期：2017-11-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_3))

<!-- Source markdown line 157.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d0d97efbb0b16638d0120af9ac5e66ec3bcfa391 b98735ec26a091f8c8c58ca1790243be7942e038  (PR=4052  ,  Filename=sp-server-diagnostics-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=45e4efb7aa828578fe9eb7743a1a3526da719555) -->



以下的範例查詢會從資料表讀取摘要輸出：
```sql
SELECT create_time,
       component_name,
       state_desc
FROM SpServerDiagnosticsResult;
```

以下的範例查詢會從資料表中的每個元件讀取某些詳細輸出：
```sql
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult
where component_name like 'resource'
go

-- Nonpreemptive waits
```







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (3+14)：**SQL 的進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (87 + 0)：**SQL 的分析平台系統**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (5+4)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：**SQL 的資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (2+2)：**SQL 的 Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (10+9)：**SQL 適用的 Linux** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (2+4)：**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (4+2)：**SQL 的 Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+1)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (21 + 0)：**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (5+1)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0 + 0)：**SQL 資料移轉小幫手 (DMA)**文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


