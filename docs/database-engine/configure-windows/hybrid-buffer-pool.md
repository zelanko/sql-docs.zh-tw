---
title: 混合式緩衝集區 | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: 1d1e595918b33ae4fcc11cd59bf0964b2e6d919c
ms.sourcegitcommit: 59c09dbe29882cbed539229a9bc1de381a5a4471
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/11/2020
ms.locfileid: "79112286"
---
# <a name="hybrid-buffer-pool"></a>混合式緩衝集區
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

混合式緩衝集區可讓緩衝集區物件參考位於持續性記憶體 (PMEM) 裝置上資料庫檔案中的資料頁，而不是在揮發性 DRAM 中快取的資料頁複本。 這項功能是在 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 中引進。

![混合式緩衝集區](./media/hybrid-buffer-pool.png)

持續性記憶體 (PMEM) 裝置為位元組可定址，且如果使用直接存取 (DAX) 持續性記憶體感知檔案系統 (例如 XFS、EXT4 或 NTFS)，則可以使用 OS 中一般檔案系統 API 來存取檔案系統上的檔案。 或者，也可以對裝置上檔案的記憶體配置圖，執行所謂的載入和儲存作業。 這可讓 PMEM 感知應用程式 (例如 SQL Server) 存取裝置上的檔案，而不需要周遊傳統的儲存體堆疊。

混合式緩衝集區使用此功能對記憶體配置圖檔案執行載入和儲存作業，以將 PMEM 裝置用為緩衝集區的快取，並儲存資料庫檔案。 這會造成獨特的情況，就是邏輯讀取和實體讀取基本上是相同的作業。 持續性記憶體裝置可透過記憶體匯流排來存取，如同一般的揮發性 DRAM。

只有完整資料頁會在混合式緩衝集區的裝置上快取。 當頁面標示為中途時，頁面會先複製到 DRAM 緩衝集區，最後寫回 PMEM 裝置，並再次標示為完整。 這會發生在一般檢查點作業期間，類似於對標準區塊裝置執行此作業。

Windows 和 Linux 都提供混合式緩衝集區功能。 PMEM 裝置必須以支援 DAX (DirectAccess) 的檔案系統格式化。 XFS、EXT4 和 NTFS 檔案系統都支援 DAX。 連結、還原或建立新的資料庫時，SQL Server 會自動偵測資料檔案是否位於正確格式化的 PMEM 裝置，並在啟動時執行資料庫檔案的記憶體對應。

如需詳細資訊，請參閱

* [了解及部署持續性記憶體 (Windows)](/windows-server/storage/storage-spaces/deploy-pmem/)
* [設定 Linux 上的 SQL Server 持續性記憶體 (PMEM)](../../linux/sql-server-linux-configure-pmem.md)


## <a name="enable-hybrid-buffer-pool"></a>啟用混合式緩衝集區

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 引進動態資料語言 (DDL) 以控制混合式緩衝集區。

下例針對 SQL Server 執行個體啟用混合式緩衝集區：

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

根據預設，混合式緩衝集區在執行個體範圍上停用。 請注意，為了讓設定變更生效，必須重新啟動 SQL Server 執行個體。 需要重新啟動以方便配置足夠的雜湊頁，納入伺服器的總 PMEM 容量。

下例針對特定資料庫啟用混合式緩衝集區。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

根據預設，混合式緩衝集區在資料庫範圍上啟用。

## <a name="disable-hybrid-buffer-pool"></a>停用混合式緩衝集區

下列範例會停用執行個體層級的混合式緩衝集區：

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

根據預設，混合式緩衝集區在執行個體層級上停用。 為了讓這項變更生效，必須重新啟動執行個體。 這樣可以確保為緩衝集區配置足夠的雜湊頁，因為現在需要將伺服器上的 PMEM 容量納入考量。

下例針對特定資料庫停用混合式緩衝集區。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

根據預設，混合式緩衝集區在資料庫範圍上啟用。

## <a name="view-hybrid-buffer-pool-configuration"></a>檢視混合式緩衝集區設定

下列範例會傳回執行個體的目前混合式緩衝集區設定狀態。

```sql
SELECT * FROM
sys.server_memory_optimized_hybrid_buffer_pool_configuration;
```

下列範例列出混合式緩衝集區 (`is_memory_optimized_enabled`) 的資料庫及資料庫層級設定。

```sql
SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>混合式緩衝集區的最佳做法

在 Windows 上格式化 PMEM 裝置時，請使用 NTFS 可提供的最大配置單位大小 (Windows Server 2019 為 2 MB)，並確定裝置已針對 DAX (直接存取) 格式化。

使用大型分頁記憶體配置模型，此模型可以透過[追蹤旗標 834](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 來啟用。 追蹤旗標 834 是啟動追蹤旗標。

使用大型分頁記憶體配置模型時，需要使用 Windows 上[記憶體中的鎖定分頁](./enable-the-lock-pages-in-memory-option-windows.md)。

檔案大小應該是 2 MB 的倍數 (模數 2 MB 應該等於零)。

如果混合式緩衝集區的伺服器範圍設定為停用，則任何使用者資料庫都不會使用此功能。

如果混合式緩衝集區的伺服器範圍設定為啟用，則您可以使用資料庫範圍設定來停用個別使用者資料庫的功能。
