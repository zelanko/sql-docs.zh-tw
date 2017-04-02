---
title: "SQL Server 組態 (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server 組態 (R Services)
本章節中的資訊提供一般指引的硬體和網路設定的電腦，可用來裝載 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 除了一般應視為 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 效能微調中提供的資訊 [SQL Server Database Engine 和 Azure SQL Database 的效能中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## 處理器

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 以平行方式可以執行的工作上，使用可用的核心可供使用，更多核心的較佳的效能。 由於 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通常是由多位使用者同時使用，資料庫管理員應該判斷理想的支援尖峰工作負載計算所需的核心數目。 CPU IO 繫結作業，也沒有幫助的核心數目，而繫結演算法將受益於含多核心更快的 Cpu。

## 記憶體

在電腦上的可用記憶體數量會對效能的進階分析的演算法很大的影響。 記憶體不足，無法使用 SQL 計算內容時，可能會影響平行處理原則程度。 它也會影響可處理的區塊大小 （每次讀取作業的資料列），同時可支援的工作階段數目。

強烈建議至少 32 GB。 如果您有超過 32 GB 的可用，您可以設定 SQL 資料來源中每個讀取作業使用多個資料列，來改善效能。

## 電源選項

Windows 作業系統上 __高效能__ 應使用電源選項。 使用不同的電源設定將會導致效能降低或不一致時使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

## 磁碟 IO

使用定型和預測工作 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 本質上是 IO 繫結，並將磁碟上儲存資料庫的速度而定。 可能有助於更快的磁碟機，例如固態硬碟 (SSD)。 

磁碟 IO 也會受到其他應用程式存取磁碟︰ 例如，讀取作業，對其他用戶端資料庫。 磁碟 IO 效能也會受到使用中，例如檔案系統所使用的區塊大小的檔案系統上的設定。 如果有多個磁碟機，將資料庫儲存在不同的磁碟上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 這樣的要求的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 無法到達的同一個磁碟做為資料儲存在資料庫中的要求。

磁碟 IO 執行 RevoScaleR 分析函數在定型期間使用多個反覆項目時，可以也會大幅影響效能。 例如， `rxLogit`, ，`rxDTree`, ，`rxDForest` 和 `rxBTrees` 所有使用多個反覆項目。 當資料來源是 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，這些演算法會使用已最佳化，以擷取資料的暫存檔案。 這些檔案會自動清除工作階段完成之後。 具有讀取/寫入作業的高效能磁碟，可以大幅改善這些演算法經過的總時間。

> [!NOTE]
> [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 需要在 Windows 作業系統上的 8.3 檔名支援。 若要判斷磁碟機是否支援 8.3 檔案名稱，或啟用支援，如果沒有，您可以使用 fsutil.exe。 如需有關使用 fsutil.exe 具有 8.3 檔案名稱的詳細資訊，請參閱 [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

### 資料表壓縮

使用壓縮或 columstore 索引通常可改善 IO 效能。 一般而言，資料通常中有重複數個資料行在資料表中，因此當壓縮資料時使用的資料行存放區索引會充分利用這些重複。

資料行存放區索引可能不是如果有很多插入至資料表的效率，但如果資料是靜態或只在不常變更，是不錯的選擇。 如果不適當的單欄式存放區，資料列的主要資料表上啟用壓縮可用來改善 IO。

如需詳細資訊，請參閱下列文件：

* [資料壓縮](../../relational-databases/data-compression/data-compression.md)

* [啟用資料表或索引的壓縮](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [資料行存放區索引指南](Columnstore%20Indexes%20Guide.md)

## 分頁檔

Windows 作業系統使用來管理損毀傾印的分頁檔和儲存的虛擬記憶體分頁。 如果您發現過度分頁，請考慮增加電腦上的實體記憶體。 雖然有更多實體記憶體不排除分頁，但它並減少分頁。

分頁檔儲存在磁碟的速度也會影響效能。 儲存頁面上的檔案 SSD，或跨多個 Ssd，使用多個頁面的檔案可以改善效能。

請參閱 [如何判斷適當的分頁檔大小為 64 位元版本的 Windows](https://support.microsoft.com/en-us/kb/2860880) 的調整大小的分頁檔的詳細資訊。

## 資源管理

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 支援支援資源監管以控制所使用的各種資源 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 例如，R 的記憶體耗用量的預設值是限制為 20%的可用的記憶體總計的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 這為了要確保 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 工作流程不會嚴重影響長時間執行的 R 工作。 不過，資料庫管理員可以變更這些限制。 

有限的資源是 __MAX_CPU_PERCENT__, ，__MAX_MEMORY_PERCENT__, ，和 __MAX_PROCESSES__。 若要檢視目前的設定，請使用這個 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 陳述式︰

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

如果 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 主要是用於 R 的服務，它可能有助於 MAX_CPU_PERCENT 增加至 40%或 60%。 如果有許多 R 工作階段使用的相同 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 這三個就會增加一次。 若要變更已配置的資源，請使用 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 陳述式。 

本範例會設定為 40%的記憶體使用量︰

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
下列範例會設定所有三個可設定的值︰
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> 若要變更這些設定會立即生效，執行陳述式 `ALTER RESOURCE GOVERNOR RECONFIGURE` 之後變更記憶體、 CPU 或最大的處理序設定。 

## 另請參閱
[資源管理員](../../relational-databases/resource-governor/resource-governor.md)

[建立外部的資源集區](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R 服務效能微調的指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [效能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 和資料最佳化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)