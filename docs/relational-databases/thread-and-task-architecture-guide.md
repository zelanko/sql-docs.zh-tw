---
title: "執行緒和工作架構指南 | Microsoft Docs"
ms.custom: 
ms.date: 10/26/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
caps.latest.revision: "3"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6f2ded3d40a1f17980507fdf92d05e3517f0bc54
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="thread-and-task-architecture-guide"></a>執行緒和工作架構指南
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

執行緒是一種作業系統功能，可讓應用程式邏輯分成數個並行的執行路徑。 當複雜的應用程式有許多可同時執行的工作時，此功能就很有用處。 

作業系統執行應用程式的執行個體時，會建立一個稱為處理序的單位來管理這個執行個體。 處理序有執行緒。 這是應用程式的程式碼所執行的程式化指令序列。 例如，如果簡易應用程式中有單一的一組可序列執行的指令，那麼應用程式將僅有一個執行路徑或一個執行緒。 較為複雜的應用程式可能會有多個工作，但這些工作可能需要一前一後執行，而不是以序列的方式執行。 應用程式可針對每一項工作啟動個別的處理序來達成此目的。 不過，啟動處理序是很耗費資源的作業。 反之，應用程式可啟動個別的執行緒， 這些就比較節省資源。 另外，每個執行緒跟那些與處理序相關聯的其他執行緒，可分開排程執行。

執行緒能讓複雜的應用程式，以更有效率的方式來使用 CPU，即使電腦只有一個 CPU。 只有一個 CPU 時，一次只能執行一個執行緒。 如果有一個執行緒執行不需使用 CPU 的長時間作業，像是磁碟讀寫，另一個執行緒便可以一直執行，直到第一個作業完成為止。 由於應用程式可在其他執行緒等待作業完成時執行一些執行緒，所以使 CPU 發揮最大功效。 特別是多使用者、需要大量磁碟 I/O 的應用程式 (例如資料庫伺服器) 更是如此。 有多個微處理器或 CPU 的電腦，可同時讓每個 CPU 執行一個執行緒。 例如，如果一部電腦有 8 個 CPU，就可以同時執行 8 個執行緒。

## <a name="sql-server-batch-or-task-scheduling"></a>SQL Server 批次或工作排程

### <a name="allocating-threads-to-a-cpu"></a>配置執行緒給 CPU

根據預設，SQL Server 的每個執行個體都會啟動每個執行緒。 如果已經啟用相似性，作業系統就會將每個執行緒指派給特定的 CPU。 作業系統會根據負載從 SQL Server 的執行個體，將執行緒分配給電腦上的微處理器或 CPU。 有時候，作業系統也會將執行緒從工作負擔繁重的 CPU 移到其他 CPU 上。 相反地，SQL Server Database Engine 會將工作者執行緒指派給排程器，以便將這些執行緒平均分配給 CPU。

Affinity Mask 選項是使用 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)設定的。 沒有設定 Affinity Mask 時，SQL Server 執行個體就會將工作者執行緒平均配置給尚未遮罩的排程器

### <a name="using-the-lightweight-pooling-option"></a>使用 lightweight pooling 選項

切換執行緒內容的額外負擔並不是太大。 SQL Server 大部分的執行個體，在將輕量型共用選項設為 0 或 1 時並不會察覺到任何效能上的差異。 只有擁有下列特性之電腦上的 SQL Server 執行個體，才有可能感受到 [輕量型共用](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) 的好處：    
* 有多個 CPU 的大型伺服器。
* 所有 CPU 皆以接近最大容量在執行。
* 內容切換的層次為高。

這些系統在將輕量型共用值設定為 1 時，可能會發現效能有稍微增加。

我們不建議您針對例行作業使用 Fiber 模式排程。 這是因為 Fiber 模式可能會抑制一般環境切換的好處而降低效能，而且 SQL Server 的某些元件無法在 Fiber 模式下正確運作。 如需詳細資訊，請參閱＜輕量型共用＞。

## <a name="thread-and-fiber-execution"></a>執行緒和 Fiber 執行

Microsoft Windows 使用數值優先權系統，從 1 到 31 的範圍來排程要執行的執行緒。 零是保留給作業系統使用的。 當有數個執行緒等待執行時，Windows 會先分派有最高優先順序的執行緒。

根據預設，每個 SQL Server 執行個體的優先權為 7，這稱為一般優先權。 這讓 SQL Server 執行緒有夠高的優先權，可以取得足夠的 CPU 資源，而不會影響其他的應用程式。 

使用 [優先權提升](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) 設定選項，可以將 SQL Server 執行個體中執行緒的優先權增加至 13。 這稱為高優先權。 這個設定讓 SQL Server 執行緒擁有比大部份其他應用程式更高的優先權。 因此，每當 SQL Server 執行緒可以執行時，通常系統會先分派執行緒，而且其他應用程式不會預先清空執行緒。 當伺服器僅執行 SQL Server 的執行個體，而沒有執行其他應用程式時，可以改善系統的效能。 不過，如果 SQL Server 中發生需要大量記憶體的作業，則其他應用程式可能無法擁有夠高的優先權以預先清空 SQL Server 執行緒。 

如果您在電腦上執行多個 SQL Server 執行個體，並且僅提高部份執行個體的優先權，則以一般優先權執行的所有執行個體之效能都將受到影響。 另外，如果有開啟優先權提升，就可能會降低伺服器上其他應用程式與元件的效能。 因此，它應該在嚴格控制的情況下使用。


## <a name="hot-add-cpu"></a>熱新增 CPU

熱新增 CPU 是指將 CPU 動態新增到執行中系統的功能。 新增 CPU 可發生於實體上新增硬體、邏輯上進行線上硬體分割或是虛擬上透過虛擬化層時。 從 SQL Server 2008 開始，SQL Server 支援熱新增 CPU。

熱新增 CPU 的需求：  
* 需要有支援熱新增 CPU 的硬體。
* 需要 64 位元版本的 Windows Server 2008 Datacenter 或適用於 Itanium 系統之作業系統的 Windows Server 2008 Enterprise Edition。
* 需要 SQL Server Enterprise。
* SQL Server 無法設定為使用軟體 NUMA。 如需有關軟體 NUMA 的詳細資訊，請參閱 [軟體 NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md)。

SQL Server 不會在新增 CPU 之後自動開始使用這些 CPU。 這樣可避免 SQL Server 使用可能要供其他用途使用而新增的 CPU。 在新增 CPU 之後，請執行 [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) 陳述式，好讓 SQL Server 會將新的 CPU 辨識為可用的資源。

> [!NOTE]
> 如果設定了 [affinity64 mask](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) ，則必須修改 affinity64 mask 才能使用新的 CPU。
 

## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>在超過 64 個 CPU 之電腦上執行 SQL Server 的最佳做法

### <a name="assigning-hardware-threads-with-cpus"></a>使用 CPU 指派硬體執行緒

請勿使用 affinity mask 和 affinity64 mask 伺服器組態選項，將處理器繫結至特定執行緒。 這些選項僅限於 64 個 CPU。 請改用 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) 的 SET PROCESS AFFINITY 選項。

### <a name="managing-the-transaction-log-file-size"></a>管理交易記錄檔大小

請勿仰賴自動成長來增加交易記錄檔的大小。 增加交易記錄必須是序列處理序。 擴充記錄可避免在記錄擴充完成之前繼續進行交易寫入作業。 不過，您可以將檔案大小設定為夠大的值來支援環境中的典型工作負載，藉此為所有記錄檔預先配置空間。

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>針對索引作業設定平行處理原則的最大程度

在具有許多 CPU 的電腦上，您可以暫時將資料庫的復原模式設定為大量記錄或簡單復原模式，藉此改善建立或重建索引等索引作業的效能。 這些索引作業可能會產生重要的記錄活動，而且記錄競爭可能會影響 SQL Server 所選擇之平行處理原則的最佳程度 (DOP)。

此外，請考慮針對這些作業調整**平行處理原則的最大程度 (MAXDOP)** 伺服器組態選項。 下列指導方針是以內部測試為基礎，而且屬於一般建議。 您應該嘗試多種不同的 MAXDOP 設定，以便決定適合您環境的最佳設定。

* 若為完整復原模式，請將「平行處理原則的最大程度」選項的值限制為 8 或更小的值。   
* 若為大量記錄模式或簡單復原模式，您就應該考慮將「平行處理原則的最大程度」選項的值設定為高於 8 的值。   
* 若為已設定 NUMA 的伺服器，平行處理原則的最大程度就不應該超過指派給每個 NUMA 節點的 CPU 數目。 這是因為查詢很可能會使用來自 1 個 NUMA 節點的本機記憶體，以便改善記憶體存取時間。  
* 若為已啟用超執行緒且為 2009 年或之前 (在改善超執行緒功能之前) 製造的伺服器，MAXDOP 值就不應該超過實體處理器的數目，而不是邏輯處理器的數目。

如需平行處理原則最大程度選項的詳細資訊，請參閱[設定 [平行處理原則的最大程度] 伺服器組態選項](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。

### <a name="setting-the-maximum-number-of-worker-threads"></a>設定工作者執行緒的數目上限

請一律將工作者執行緒的數目上限設定為大於平行處理原則的最大程度的設定。 工作者執行緒的數目一律至少必須設定為目前存在伺服器上之 CPU 數目的七倍。 如需詳細資訊，請參閱 [設定最大工作者執行緒選項](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)。

### <a name="using-sql-trace-and-sql-server-profiler"></a>使用 SQL 追蹤和 SQL Server Profiler

 我們建議您不要在實際執行環境中使用 SQL 追蹤和 SQL Server Profiler。 執行這些工具的負擔也會隨著 CPU 數目增加而提高。 如果您必須在實際執行環境中使用 SQL 追蹤，請將追蹤事件的數目限制為最小值。 請仔細地分析和測試低於負載的每個追蹤事件，並且避免使用大幅影響效能的事件組合。

### <a name="setting-the-number-of-tempdb-data-files"></a>設定 tempdb 資料檔案的數目

通常，tempdb 資料檔案的數目應該與 CPU 數目相符。 不過，只要仔細地考量 tempdb 的並行需求，您就可以減少資料庫管理作業。 例如，如果系統具有 64 個 CPU 而且通常只有 32 個查詢使用 tempdb，則將 tempdb 檔案的數目增加至 64 並不會改善效能。

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>可以使用超過 64 個 CPU 的 SQL Server 元件

下表將列出 SQL Server 元件並指出它們是否能使用超過 64 個 CPU。

|程序名稱   |可執行的程式 |使用超過 64 個 CPU |  
|----------|----------|----------|  
|SQL Server Database Engine |Sqlserver.exe  |是 |  
|Reporting Services |Rs.exe |否 |  
|Analysis Services  |As.exe |否 |  
|Integration Services   |Is.exe |否 |  
|Service Broker |Sb.exe |否 |  
|全文檢索搜尋   |Fts.exe    |否 |  
|SQL Server Agent   |Sqlagent.exe   |否 |  
|Transact-SQL   |Ssms.exe   |否 |  
|SQL Server 安裝程式   |Setup.exe  |否 |  


