---
title: "SQL Server 2014 版本資訊 | Microsoft Docs"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: "100"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c507363ad05be7410ae69fc6d5f6748ad1738cb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
這份版本資訊文件說明安裝或疑難排解 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]之前應該閱讀的已知問題。  
  
## <a name="top"></a>目錄  
[1.0 安裝之前](#BeforeInstall)  
  
[2.0 產品文件](#ProdDoc)  
  
[3.0 資料庫引擎](#DBEngine)  
  
[4.0 Reporting Services](#SSRS)  
  
[5.0 Windows Azure 虛擬機器上的 SQL Server 2014](#AzureVM)  
  
[6.0 Analysis Services](#SSAS)  
  
[7.0 Data Quality Services](#DQS)  
  
[8.0 升級建議程式](#UA)  
  
## <a name="BeforeInstall"></a>1.0 安裝之前  
  
### <a name="11-limitations-and-restrictions-in-sql-server-2014-rtm"></a>1.1 SQL Server 2014 RTM 的侷限和限制  
  
#### <a name="111-general-limitations-and-restrictions"></a>1.1.1 一般侷限和限制  
  
1.  不支援從 SQL Server 2014 CTP 1 升級至 SQL Server 2014 RTM。  
  
2.  不支援並存安裝 SQL Server 2014 CTP 1 與 SQL Server 2014 RTM。  
  
3.  不支援將 SQL Server 2014 CTP 1 資料庫附加或還原到 SQL Server 2014 RTM。  
  
**因應措施** ：無。  
  
#### <a name="12-considerations-for-upgrading-sql-server-2014-ctp-2-to-sql-server-2014-rtm-and-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2 將 SQL Server 2014 CTP 2 升級至 SQL Server 2014 RTM 以及從 SQL Server 2014 RTM 降級至 SQL Server 2014 CTP 2 的考量  
  
#### <a name="121-upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm-is-fully-supported"></a>1.2.1 從 SQL Server 2014 CTP 2 升級至 SQL Server RTM 受到完整支援  
具體而言，您可以：  
  
1.  將 SQL Server 2014 CTP 2 資料庫附加到 SQL Server 2014 RTM 執行個體。  
  
2.  將 SQL Server 2014 CTP 2 上所建立的資料庫備份還原至 SQL Server 2014 RTM 執行個體。  
  
3.  就地升級至 SQL Server 2014 RTM。  
  
4.  輪流升級至 SQL Server 2014 RTM。 您必須先切換到手動容錯移轉模式，才能起始輪流升級。 如需詳細資訊，請參閱 [在停機時間和資料遺失最少的情況下升級及更新可用性群組伺服器](http://msdn.microsoft.com/library/dn178483.aspx) 。  
  
5.  SQL Server 2014 CTP 2 中安裝之交易效能收集組所收集的資料無法透過 SQL Server 2014 RTM 中的 SQL Server Management Studio 來檢視，反之亦然。 請使用 SQL Server 2014 CTP 2 中的 SQL Server Management Studio 來檢視 SQL Server 2014 CTP 2 中安裝之收集組所收集的資料，並使用 SQL Server 2014 RTM 中的 SQL Server Management Studio 來檢視 SQL Server 2014 RTM 中安裝之收集組所收集的資料。  
  
### <a name="122-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2.2 從 SQL Server 2014 RTM 降級至 SQL Server 2014 CTP 2  
不支援這個動作。  
  
**因應措施** ：沒有降級的因應措施。 我們建議您先備份資料庫，然後再升級至 SQL Server 2014 RTM。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="13-incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>1.3 SQL Server 2014 媒體/ISO/CAB 上出現錯誤版本的 StreamInsight 用戶端  
版本錯誤的 StreamInsight.msi 和 StreamInsightClient.msi 位於下列 SQL Server 媒體/ISO/CAB 的路徑中 (StreamInsight\\\<結構\>\\\<語言識別碼\>)。  
  
**因應措施：** 從 [SQL Server 2014 功能套件下載頁面](http://go.microsoft.com/fwlink/?LinkID=306709)下載並安裝正確版本。  
  
## <a name="ProdDoc"></a>2.0 產品文件  
  
### <a name="21-report-builder-content-is-not-available-in-some-languages"></a>2.1 報表產生器的內容不提供某些語言版本  
**問題** ：報表產生器的內容不提供以下這些語言版本。  
  
-   希臘文 (el-GR)  
  
-   挪威文 (巴克摩) (nb-NO)  
  
-   芬蘭文 (fi-FI)  
  
-   丹麥文 (da-DK)  
  
在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中，此內容可從隨附於產品的 CHM 檔案中取得，並且提供這些語言版本。 CHM 檔案不再隨附於產品，而報表產生器內容也只提供在 MSDN 上。 但 MSDN 不支援這些語言。 報表產生器也已從 TechNet 移除，無法再用於那些支援的語言。  
  
**因應措施** ：無。  
  
### <a name="22-powerpivot-content-is-not-available-in-some-languages"></a>2.2 某些語言版本不提供 PowerPivot 內容  
**問題：** 下列語言版本不提供 Power Pivot 的內容。  
  
-   希臘文 (el-GR)  
  
-   挪威文 (巴克摩) (nb-NO)  
  
-   芬蘭文 (fi-FI)  
  
-   丹麥文 (da-DK)  
  
-   捷克文 (cs-CZ)  
  
-   匈牙利文 (hu-HU)  
  
-   荷蘭文 (荷蘭) (nl-NL)  
  
-   波蘭文 (pl-PL)  
  
-   瑞典文 (sv-SE)  
  
-   土耳其文 (tr-TR)  
  
-   葡萄牙文 (葡萄牙) (pt-PT)  
  
在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]中，TechNet 與這些語言版本曾經提供此內容。 此內容已從 TechNet 移除，無法再用於這些支援的語言。  
  
**因應措施** ：無。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="DBEngine"></a>3.0 資料庫引擎  
  
### <a name="31-changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>3.1 針對 SQL Server 2014 RTM 中的 Standard 版所做的變更  
SQL Server 2014 Standard 版的變更如下：  
  
-   緩衝集區擴充功能最高允許使用已設定之記憶體大小的四倍。  
  
-   最大記憶體已經從 64GB 增加至 128GB。  
  
### <a name="32-in-memory-oltp-issues"></a>3.2 In-Memory OLTP 問題  
  
#### <a name="321-memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>3.2.1 Memory Optimization Advisor 旗標將預設條件約束設定為不相容  
**問題** ：SQL Server Management Studio 中的 Memory Optimized Advisor 旗標全都將預設條件約束設定為不相容。 並非所有預設條件約束在記憶體最佳化資料表中都有受到支援，此 Advisor 不會區分支援與未支援類型的預設條件約束。 支援的預設條件約束包括以原生方式編譯之預存程序內所支援的所有常數、運算式和內建函數。 若要查看以原生方式編譯之預存程序內所支援的函數清單，請參閱 [原生編譯的預存程序中支援的建構](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx)。  
  
**因應措施** ：如果您要使用此 Advisor 來識別封鎖器，請忽略相容的預設條件約束。 若要使用 Memory Optimization Advisor 來移轉具有相容預設條件約束的資料表，但沒有其他封鎖器，請遵循下列步驟進行：  
  
1.  從資料表定義中移除預設條件約束。  
  
2.  使用此 Advisor 針對資料表產生移轉指令碼。  
  
3.  在移轉指令碼中加回預設條件約束。  
  
4.  執行移轉指令碼。  
  
#### <a name="322-informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>3.2.2「檔案存取遭拒」參考訊息誤報為 SQL Server 2014 錯誤記錄檔中的錯誤  
**問題** ：當重新啟動的伺服器擁有包含記憶體最佳化資料表的資料庫時，您可能會在 SQL Server 2014 錯誤記錄檔中看到以下類型的錯誤訊息：  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
  
這事實上是參考訊息，使用者不必採取任何動作。  
  
**因應措施** ：無。 這是參考訊息。  
  
#### <a name="323-missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>3.2.3 遺漏索引詳細資料誤報記憶體最佳化資料表包含的資料行  
**問題** ：如果 SQL Server 2014 偵測到記憶體最佳化資料表上的查詢有遺漏索引，它將會在 SHOWPLAN_XML 中報告遺漏索引，以及在類似 sys.dm_db_missing_index_details 的遺漏索引 DMV 中報告遺漏索引。 在某些情況下，遺漏索引詳細資料將會包含內含的資料行。 當所有資料行都隱含地隨附記憶體最佳化資料表上的所有索引時，不允許明確指定包含記憶體最佳化索引的內含資料行。  
  
**因應措施** ：請勿使用記憶體最佳化資料表上的索引指定 INCLUDE 子句。  
  
#### <a name="324-missing-index-details-omit-missing-indexes-if-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>3.2.4 如果雜湊索引存在但不適用於查詢，遺漏索引詳細資料會省略遺漏索引  
**問題** ：如果您在查詢中參考之記憶體最佳化資料表的資料行上擁有 HASH 索引，但是此索引無法用於查詢，則 SQL Server 2014 不一定會在 SHOWPLAN_XML 和 DMV sys.dm_db_missing_index_details 中報告遺漏索引。  
  
特別是，如果查詢包含的等號比較述詞牽涉到索引鍵資料行的子集或是查詢包含的不等號比較述詞牽涉到索引鍵資料行，則 HASH 索引無法以其現狀使用，而且需要不同的索引才能有效率地執行查詢。  
  
**因應措施** ：如果您使用雜湊索引，請檢查查詢和查詢計劃，以判斷查詢在索引鍵的子集或不等號比較述詞上是否可以從索引搜尋作業獲益。 如果您需要進行索引鍵子集的搜尋，請使用 NONCLUSTERED 索引，或是在您正好需要搜尋的資料行上使用 HASH 索引。 如果您需要進行不等號比較述詞的搜尋，請使用 NONCLUSTERED 索引而不是 HASH 索引。  
  
#### <a name="325-failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>3.2.5 在相同查詢中使用記憶體最佳化資料表和記憶體最佳化資料表變數時，如果資料庫選項 READ_COMMITTED_SNAPSHOT 設為 ON 則會發生失敗  
**問題** ：如果資料庫選項 READ_COMMITTED_SNAPSHOT 設為 ON，而且您可在使用者交易內容外面的相同陳述式中存取記憶體最佳化資料表和記憶體最佳化資料表變數，您可能會收到下列錯誤訊息：  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**因應措施** ：請搭配資料表變數使用資料表提示 WITH (SNAPSHOT)，或是使用以下陳述式將資料庫選項 MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT 設定為 ON：  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="326-procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>3.2.6 以原生方式編譯之預存程序的程序和查詢執行統計資料以 1000 的倍數記錄工作者時間  
**問題** ：在使用 sp_xtp_control_proc_exec_stats 或 sp_xtp_control_query_exec_stats 針對原生方式編譯的預存程序啟用程序或查詢執行統計資料的收集之後，您將會看到 DMV sys.dm_exec_procedure_stats 和 sys.dm_exec_query_stats 中報告的 *_worker_time 為 1000 的倍數。 工作者時間少於 500 微秒的查詢執行會將 worker_time 報告為 0。  
  
**因應措施** ：無。 若要在以原生方式編譯的預存程序中執行短期的查詢，請勿依賴執行統計資料 DMV 中所報告的 worker_time。  
  
#### <a name="327-error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>3.2.7 如果以原生方式編譯的預存程序包含長的運算式，則 SHOWPLAN_XML 會發生錯誤  
**問題** ：如果以原生方式編譯的預存程序包含長的運算式，為此程序取得 SHOWPLAN_XML，則使用 T-SQL 選項 SET SHOWPLAN_XML ON 或是在 Management Studio 中使用 [顯示估計執行計畫] 選項可能會產生下列錯誤：  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**因應措施** ：有兩種建議的因應措施：  
  
1.  為運算式加上括號，如以下範例所示：  
  
    不要這樣撰寫：  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    而要這樣撰寫：  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  以稍微簡化的運算式建立第二個程序以供執行程序表使用 - 計劃的一般形狀應該相同。 例如，不要這樣撰寫：  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    而要這樣撰寫：  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="328-using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>3.2.8 在以原生方式編譯的預存程序中搭配 DATEPART 和相關函數使用字串參數或變數會產生錯誤  
**問題** ：在以原生方式編譯的預存程序中使用具有字串資料類型 (例如 (var)char 或 n(var)char) 的參數或變數搭配內建函數 DATEPART、DAY、MONTH 和 YEAR 時，您會看到錯誤訊息，此訊息表示以原生方式編譯的預存程序不支援 datetimeoffset 資料類型。  
  
**因應措施** ：將字串參數或變數指派給 datetime2 類型的新變數，然後在函數 DATEPART、DAY、MONTH 或 YEAR 中使用該變數。 例如：  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="329-native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>3.2.9 原生編譯 Advisor 標示 DELETE FROM 子句錯誤  
**問題：** 原生編譯 Advisor 將預存程序內的 DELETE FROM 子句誤標為不相容。  
  
**因應措施** ：無。  
  
### <a name="33-register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>3.3 透過 SSMS 註冊會加入具有不相符執行個體識別碼的 DAC 中繼資料  
**問題** ：當透過 SQL Server Management Studio 註冊或刪除資料層應用程式封裝 (.dacpac) 時，系統未正確更新 sysdac* 資料表來讓使用者查詢資料庫的 dacpac 記錄。  sysdac_history_internal 和 sysdac_instances_internal 的 instance_id 不符合，無法允許聯結。  
  
**因應措施** ：修正此問題的方法為重新發佈 [資料層應用程式架構](https://www.microsoft.com/download/details.aspx?id=42295)的功能套件。  套用更新之後，所有新的記錄項目將使用 sysdac_instances_internal 資料表中針對 instance_id 所列的值。  
  
如果您已遇到不相符的 instance_id 值這項問題，更正不相符之值的唯一方法是以權限使用者身分連接到伺服器，進而寫入 MSDB 資料庫並更新 instance_id 值來使其相符。  如果相同資料庫有多個註冊和取消註冊的事件，則您可能需查看日期/時間，以找出哪個記錄與目前的 instance_id 值相符。  
  
1.  使用具有 MSDB 更新權限的登入身分在 SQL Server Management Studio 中連接到伺服器。  
  
2.  使用 MSDB 資料庫開啟新的查詢。  
  
3.  執行此查詢來查看所有使用中的 DAC 執行個體。  尋找您想要更正的執行個體，並記下 instance_id：  
  
    `select * from` sysdac_instances_internal  
  
4.  執行此查詢，並查看所有記錄項目：  
  
    `select * from` sysdac_history_internal  
  
5.  識別應該對應至您要修正之執行個體的資料列  
  
6.  將 sysdac_history_internal.instance_id 值更新為您在步驟 3 記下的值 (來自 sysdac_instances_internal 資料表)：  
  
    `update` sysdac_history_internal `set` instance_id = '\<步驟 3 的值\>' `where` \<符合您想要更新之資料列的運算式\>  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="SSRS"></a>4.0 Reporting Services  
  
### <a name="41-the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>4.1 SQL Server 2012 Reporting Services 原生模式報表伺服器無法與 SQL Server 2014 Reporting Services SharePoint 元件並排執行  
**問題** ：如果在相同的伺服器上安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式 Windows 服務「SQL Server Reporting Services」(ReportingServicesService.exe) 便無法啟動。  
  
**因應措施** ：解除安裝 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 元件，並重新啟動 Microsoft SQL Server 2012 Reporting Services Windows 服務。  
  
**詳細資訊：**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式無法與下列任一項並存執行：  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 適用於 SharePoint 產品的增益集  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務  
  
並存安裝會阻止 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式 Windows 服務啟動。 在 Windows 事件記錄檔中將會看見類似下面的錯誤訊息：  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
如需詳細資訊，請參閱＜ [SQL Server 2014 Reporting Services 提示、秘訣和疑難排解](http://go.microsoft.com/fwlink/?LinkID=391254)＞。  
  
### <a name="42-required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>4.2 多節點 SharePoint 伺服器陣列至 SQL Server 2014 Reporting Services 的必要升級順序  
**問題** ：如果 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務的執行個體在所有適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集執行個體之前升級，則多節點伺服器陣列中的報表轉譯會失敗。  
  
**因應措施** ：在多節點 SharePoint 伺服器陣列中：  
  
1.  請先升級適用於 SharePoint 產品之 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集的所有執行個體。  
  
2.  然後升級 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 共用服務的所有執行個體。  
  
如需詳細資訊，請參閱 [SQL Server 2014 Reporting Services 提示、秘訣和疑難排解](http://go.microsoft.com/fwlink/?LinkID=391254)。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="AzureVM"></a>5.0 Windows Azure 虛擬機器上的 SQL Server 2014 RTM  
  
### <a name="51-the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>5.1 在 Windows Azure 中設定可用性群組接聽程式時，加入 Azure 複本精靈傳回錯誤  
**問題** ：如果可用性群組有接聽程式，加入 Azure 複本精靈嘗試在 Windows Azure 中設定接聽程式時將會傳回錯誤。  
  
這是因為可用性群組接聽程式需要在每一個主控可用性群組複本的子網路 (包括 Azure 子網路) 中指派一個 IP 位址。  
  
**因應措施：**  
  
1.  在 [接聽程式] 頁面中，將 Azure 子網路中將會主控可用性群組複本的免費靜態 IP 位址指派給可用性群組接聽程式。  
  
    這樣會讓精靈完成在 Windows Azure 中加入複本的工作。  
  
2.  當精靈完成之後，您必須在 Windows Azure 中完成接聽程式的組態，如 [教學課程：Windows Azure 中 AlwaysOn 可用性群組的接聽程式組態](http://msdn.microsoft.com/library/dn376546.aspx)中所述。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="SSAS"></a>6.0 Analysis Services  
  
### <a name="61-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>6.1 必須針對已使用 SQL Server 2014 設定的 SharePoint 2010 新伺服器陣列下載、安裝及註冊 MSOLAP.5。  
**問題：**  
  
-   如果是有設定 SQL Server 2014 RTM 部署的 SharePoint 2010 伺服器陣列，PowerPivot 活頁簿將無法連接到資料模型，因為連接字串中所參考的提供者並未安裝。  
  
**因應措施：**  
  
1.  從 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能套件下載 MSOLAP.5 提供者。 在執行 Excel Services 的應用程式伺服器上安裝提供者。 如需詳細資訊，請參閱＜ [Microsoft SQL Server 2012 SP1 功能套件](http://www.microsoft.com/download/details.aspx?id=35580)＞中的＜Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1＞一節。  
  
2.  向 SharePoint Excel Services 註冊 MSOLAP.5 當做信任的提供者。 如需詳細資訊，請參閱＜ [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx)＞。  
  
**詳細資訊：**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含 MSOLAP.6。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 活頁簿使用 MSOLAP.5。 如果 MSOLAP.5 並未安裝在執行 Excel Services 的電腦上，Excel Services 將無法載入資料模型。  
  
### <a name="62-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>6.2 必須針對已使用 SQL Server 2014 設定的 SharePoint 2013 新伺服器陣列下載、安裝及註冊 MSOLAP.5。  
**問題：**  
  
-   如果是已使用 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 部署設定的 SharePoint 2013 伺服器陣列，參照 MSOLAP.5 提供者的 Excel 活頁簿無法連接到表格式資料模型，因為並未安裝連接字串中所參照的提供者。  
  
**因應措施：**  
  
1.  從 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能套件下載 MSOLAP.5 提供者。 在執行 Excel Services 的應用程式伺服器上安裝提供者。 如需詳細資訊，請參閱＜ [Microsoft SQL Server 2012 SP1 功能套件](http://www.microsoft.com/download/details.aspx?id=35580)＞中的＜Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1＞一節。  
  
2.  向 SharePoint Excel Services 註冊 MSOLAP.5 當做信任的提供者。 如需詳細資訊，請參閱＜ [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx)＞。  
  
**詳細資訊：**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 包含 MSOLAP.6。 但是 SQL Server 2014 PowerPivot 活頁簿會使用 MSOLAP.5。 如果 MSOLAP.5 並未安裝在執行 Excel Services 的電腦上，Excel Services 將無法載入資料模型。  
  
### <a name="63-corrupt-data-refresh-schedules"></a>6.3 資料重新整理排程損毀  
**問題：**  
  
-   您要更新重新整理排程，而排程已損毀且無法使用。  
  
**因應措施：**  
  
1.  在 Microsoft Excel 中，清除自訂進階屬性。 請參閱下列知識庫文章＜ [KB 2927748](http://support.microsoft.com/kb/2927748)＞的＜因應措施＞一節。  
  
**詳細資訊：**  
  
-   當您更新活頁簿的資料重新整理排程時，如果重新整理排程的序列化長度小於原始排程，則無法正確更新緩衝區大小，新的排程資訊會與舊的排程資訊合併，而導致排程損毀。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="DQS"></a>7.0 Data Quality Services  
  
### <a name="71-no-cross-version-support-for-data-quality-services-in-master-data-services"></a>7.1 Master Data Services 中的 Data Quality Services 沒有跨版本支援  
**問題** ：以下案例不受支援：  
  
-   在已安裝 Data Quality Services 2012 的 SQL Server 2012 中，於 SQL Server Database Engine 資料庫中裝載 Master Data Services 2014。  
  
-   在已安裝 Data Quality Services 2014 的 SQL Server 2014 中，於 SQL Server Database Engine 資料庫中裝載 Master Data Services 2012。  
  
**因應措施** ：使用與 Database Engine 資料庫和 Data Quality Services 相同版本的 Master Data Services。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
## <a name="UA"></a>8.0 升級建議程式問題  
  
### <a name="81--sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>8.1 SQL Server 2014 Upgrade Advisor 報告與 SQL Server Reporting Services 無關的升級問題  
**問題** ：隨附於 SQL Server 2014 媒體的 SQL Server Upgrade Advisor (SSUA) 在分析 SQL Server Reporting Services 伺服器時誤報有多個錯誤。  
  
**因應措施** ： [適用於 SSUA 的 SQL Server 2014 功能套件](http://go.microsoft.com/fwlink/?LinkID=306709)中所提供的 SQL Server Upgrade Advisor 已修正此問題。  
  
### <a name="82--sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>8.2 SQL Server 2014 Upgrade Advisor 在分析 SQL Server Integration Services 伺服器時報告錯誤  
**問題** ：隨附於 SQL Server 2014 媒體的 SQL Server Upgrade Advisor (SSUA) 在分析 SQL Server Integration Services 伺服器時回報錯誤。  顯示給使用者看的錯誤如下：  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**因應措施** ： [適用於 SSUA 的 SQL Server 2014 功能套件](http://go.microsoft.com/fwlink/?LinkID=306709)中所提供的 SQL Server Upgrade Advisor 已修正此問題。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../sql-server/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[頂端](#top)  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
