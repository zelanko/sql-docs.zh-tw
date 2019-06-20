---
title: tempdb 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b1265d3ef58f6ef0946937b15411b0cb79a3c20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916880"
---
# <a name="tempdb-database"></a>tempdb 資料庫
  **tempdb** 系統資料庫是全域資源，適用於所有連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的使用者，且可用來保留下列項目：  
  
-   明確建立的暫存使用者物件 (例如：全域或本機暫存資料表、暫存預存程序、資料表變數或資料指標)。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]所建立的內部物件 (例如，儲存多工緩衝處理或排序之中繼結果集的工作資料表)。  
  
-   由資料庫中的資料修改交易所產生的資料列版本，該資料庫採用使用資料列版本設定隔離的讀取認可或快照集隔離交易。  
  
-   由以下這類功能的資料修改交易所產生的資料列版本：線上索引作業、Multiple Active Result Set (MARS) 和 AFTER 觸發程序。  
  
 **tempdb** 中的作業會以最低限度記錄。 這可讓您回復交易。 每次啟動**時都會重新建立** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這樣系統永遠會以乾淨的資料庫複本啟動。 連接中斷時會自動卸除暫存資料表與預存程序，且系統關閉時所有連接都會停止。 因此， **tempdb** 中的任何資料都不會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個工作階段儲存到其他的工作階段。 **tempdb**不允許進行備份和還原作業。  
  
## <a name="physical-properties-of-tempdb"></a>tempdb 的實體屬性  
 下表列示 **tempdb** 資料和記錄檔的初始組態值。 對於不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這些檔案的大小稍有不同。  
  
|檔案|邏輯名稱|實體名稱|檔案成長|  
|----------|------------------|-------------------|-----------------|  
|主要資料|tempdev|tempdb.mdf|以百分之 10 的比例自動成長，直到磁碟全滿|  
|Log|templog|templog.ldf|以 10% 的比例自動成長，最大至 2 TB|  
  
 大小**tempdb**可能會影響系統效能。 例如，如果**tempdb**大小太小，可能是系統處理太成長佔用資料庫，以支援您每次您啟動的工作負載需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以增加的大小，以避免額外的負荷**tempdb**。  
  
## <a name="performance-improvements-in-tempdb"></a>tempdb 中的效能改進  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，會以下列方式改進 **tempdb** 效能：  
  
-   可能會快取暫存資料表和資料表變數。 快取允許卸除和建立暫存物件以極快速度執行的作業，並減少頁面配置競爭。  
  
-   已改進配置頁面閂鎖通訊協定。 這會減少所使用的 UP (更新) 閂鎖數目。  
  
-   會減少 **tempdb** 的記錄負擔。 這會減少 **tempdb** 記錄檔的磁碟 I/O 頻寬耗用量。  
  
-   配置混合的頁面中的演算法**tempdb**已獲得改善。  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>移動 tempdb 資料和記錄檔  
 若要移動 **tempdb** 資料和記錄檔，請參閱 [移動系統資料庫](system-databases.md)。  
  
### <a name="database-options"></a>資料庫選項  
 下表列出 **tempdb** 資料庫中每個資料庫選項的預設值，以及這些選項是否可以修改。 若要檢視這些選項目前的設定，請參閱 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 目錄檢視。  
  
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
|CURSOR_DEFAULT|GLOBAL|是|  
|資料庫可用性選項|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|否<br /><br /> 否<br /><br /> 否|  
|DATE_CORRELATION_OPTIMIZATION|OFF|是|  
|DB_CHAINING|ON|否|  
|ENCRYPTION|OFF|否|  
|NUMERIC_ROUNDABORT|OFF|是|  
|PAGE_VERIFY|CHECKSUM (新安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。<br /><br /> NONE (升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。|是|  
|PARAMETERIZATION|SIMPLE|是|  
|QUOTED_IDENTIFIER|OFF|是|  
|READ_COMMITTED_SNAPSHOT|OFF|否|  
|RECOVERY|SIMPLE|否|  
|RECURSIVE_TRIGGERS|OFF|是|  
|Service Broker 選項|ENABLE_BROKER|是|  
|TRUSTWORTHY|OFF|否|  
  
 如需這些資料庫選項的描述，請參閱 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
## <a name="restrictions"></a>限制  
 下列作業不能在 **tempdb** 資料庫上執行：  
  
-   加入檔案群組。  
  
-   備份或還原資料庫。  
  
-   變更定序。 預設定序是伺服器定序。  
  
-   變更資料庫擁有者。 **tempdb** 是由 **sa**擁有。  
  
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
  
## <a name="permissions"></a>Permissions  
 任何使用者都可以在 tempdb 中建立暫時物件。 除非收到其他權限，否則使用者只能存取自己的物件。 您可以撤銷 tempdb 的連接權限來阻止使用者使用 tempdb，不過不建議您這樣做，因為有些常式作業需要使用 tempdb。  
  
## <a name="related-content"></a>相關內容  
 [索引的 SORT_IN_TEMPDB 選項](../indexes/indexes.md)  
  
 [系統資料庫](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [移動資料庫檔案](move-database-files.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server 2005 中的 tempdb](https://chresandro.wordpress.com/2014/09/29/working-with-tempdb-in-sql-server-2005/)  
  
  
