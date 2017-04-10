---
title: "tempdb 資料庫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "暫存資料表 [SQL Server], tempdb 資料庫"
  - "tempdb 資料庫 [SQL Server], 關於 tempdb"
  - "暫存預存程序 [SQL Server]"
  - "tempdb 資料庫 [SQL Server]"
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
caps.latest.revision: 66
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 66
---
# tempdb 資料庫
  **tempdb** 系統資料庫是全域資源，適用於所有連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的使用者，且可用來保留下列項目：  
  
-   明確建立的暫存使用者物件 (例如：全域或本機暫存資料表、暫存預存程序、資料表變數或資料指標)。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 所建立的內部物件 (例如，儲存多工緩衝處理或排序之中繼結果集的工作資料表)。  
  
-   由資料庫中的資料修改交易所產生的資料列版本，該資料庫採用使用資料列版本設定隔離的讀取認可或快照集隔離交易。  
  
-   由以下這類功能的資料修改交易所產生的資料列版本：線上索引作業、Multiple Active Result Set (MARS) 和 AFTER 觸發程序。  
  
 **tempdb** 中的作業會以最低限度記錄。 這可讓您回復交易。 每次啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時都會重新建立 **tempdb**，這樣系統永遠會以乾淨的資料庫複本啟動。 連接中斷時會自動卸除暫存資料表與預存程序，且系統關閉時所有連接都會停止。 因此，**tempdb** 中的任何資料都不會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個工作階段儲存到其他的工作階段。 **tempdb** 不允許進行備份和還原作業。  
  
## tempdb 的實體屬性  
 下表列示 **tempdb** 資料和記錄檔的初始組態值。 對於不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這些檔案的大小稍有不同。  
  
|檔案|邏輯名稱|實體名稱|初始大小|檔案成長|  
|----------|------------------|-------------------|------------------|-----------------|  
|主要資料|tempdev|tempdb.mdf|8 MB|自動成長 64 KB，直到磁碟滿了為止|  
|次要資料檔*|temp#|tempdb_mssql_#.ndf|8 MB|自動成長 64 KB，直到磁碟滿了為止|  
|Log|templog|templog.ldf|8 MB|自動成長 64 MB，最大至 2 TB。|  
  
 \* 檔案數目取決於電腦上 (邏輯) 核心的數量。 值會是核心的數目或 8 個，以較低者為準。   
資料檔案數目預設值取決於 [KB 2154845](https://support.microsoft.com/en-us/kb/2154845/) 內的一般指導方針。  
  
## tempdb 中的效能改進  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，會以下列方式改進 **tempdb** 效能：  
  
-   可能會快取暫存資料表和資料表變數。 快取允許卸除和建立暫存物件以極快速度執行的作業，並減少頁面配置競爭。  
  
-   已改進配置頁面閂鎖通訊協定。 這會減少所使用的 UP (更新) 閂鎖數目。  
  
-   會減少 **tempdb** 的記錄負擔。 這會減少 **tempdb** 記錄檔的磁碟 I/O 頻寬耗用量。  
  
-   安裝程式會在新的執行個體安裝期間加入多個 tempdb 資料檔案。 可使用 [資料庫引擎組態] 區段上的新 UI 輸入控制項和命令列參數 /SQLTEMPDBFILECOUNT 完成此工作。 根據預設，安裝程式會加入與 CPU 計數一樣多的 (或是 8 個) tempdb 檔案，以較低者為準。  
  
-   如果有多個 **tempdb** 資料檔案，則視成長設定而定，所有的檔案會都同時以相同數量自動成長。  不再需要追蹤旗標 1117。  
  
-   **tempdb** 中的所有配置都使用統一範圍。 不再需要追蹤旗標 1118。  
  
-   主要檔案群組中，已開啟 AUTOGROW_ALL_FILES 屬性而且此屬性無法修改。  
  
### 移動 tempdb 資料和記錄檔  
 若要移動 **tempdb** 資料和記錄檔，請參閱[移動系統資料庫](../../relational-databases/databases/move-system-databases.md)。  
  
### 資料庫選項  
 下表列出 **tempdb** 資料庫中每個資料庫選項的預設值，以及這些選項是否可以修改。 若要檢視這些選項目前的設定，請參閱 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視。  
  
|資料庫選項|預設值|可以修改|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|是|  
|ANSI_NULL_DEFAULT|OFF|是|  
|ANSI_NULLS|OFF|是|  
|ANSI_PADDING|OFF|是|  
|ANSI_WARNINGS|OFF|是|  
|ARITHABORT|OFF|是|  
|AUTO_CLOSE|OFF|否|  
|AUTO_CREATE_STATISTICS|ON|是|  
|AUTO_SHRINK|OFF|否|  
|AUTO_UPDATE_STATISTICS|ON|是|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|是|  
|CHANGE_TRACKING|OFF|否|  
|CONCAT_NULL_YIELDS_NULL|OFF|是|  
|CURSOR_CLOSE_ON_COMMIT|OFF|是|  
|CURSOR_DEFAULT |GLOBAL|是|  
|資料庫可用性選項|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|MIXED_PAGE_ALLOCATION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY |CHECKSUM (新安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。<br /><br /> NONE (升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|否|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 選項|ENABLE_BROKER |是|  
|TRUSTWORTHY|OFF|否|  
  
 如需這些資料庫選項的描述，請參閱 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)。  
  
## 限制  
 下列作業不能在 **tempdb** 資料庫上執行：  
  
-   加入檔案群組。  
  
-   備份或還原資料庫。  
  
-   變更定序。 預設定序是伺服器定序。  
  
-   變更資料庫擁有者。 **tempdb** 是由 **sa** 擁有。  
  
-   建立資料庫快照集。  
  
-   卸除資料庫。  
  
-   從資料庫卸除 **guest** 使用者。  
  
-   啟用異動資料擷取。  
  
-   參與資料庫鏡像。  
  
-   移除主要檔案群組、主要資料檔或記錄檔。  
  
-   重新命名資料庫或主要檔案群組。  
  
-   執行 DBCC CHECKALLOC。  
  
-   執行 DBCC CHECKCATALOG。  
  
-   將資料庫設定為 OFFLINE。  
  
-   將資料庫或主要檔案群組設定為 READ_ONLY。  
  
## Permissions  
 任何使用者都可以在 tempdb 中建立暫時物件。 除非收到其他權限，否則使用者只能存取自己的物件。 您可以撤銷 tempdb 的連接權限來阻止使用者使用 tempdb，不過不建議您這樣做，因為有些常式作業需要使用 tempdb。  
  
## 相關內容  
 [索引的 SORT_IN_TEMPDB 選項](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
  
 [系統資料庫](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)  
  
## 另請參閱  
 [使用 SQL Server 2005 中的 tempdb](http://go.microsoft.com/fwlink/?LinkId=81216)  
  
  