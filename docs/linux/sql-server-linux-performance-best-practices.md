---
title: "SQL Server on Linux 的效能最佳做法 |Microsoft 文件"
description: "本主題提供在 Linux 上執行 SQL Server 2017 的效能最佳做法和方針。"
author: rgward
ms.author: bobward
manager: jhubbard
ms.date: 09/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 8aa36adac3f7be50105a387dc3d39fca208eaba8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-2017-on-linux"></a>效能最佳作法和 Linux 上的 SQL Server 2017 的設定指導方針

本主題會提供最佳做法和建議將用於連接到 SQL Server on Linux 的資料庫應用程式的效能最大化。 這些建議專屬於 Linux 平台上執行。 所有標準 SQL Server，例如索引設計仍適用於建議。

下列指導方針包含設定 SQL Server 和 Linux 作業系統的建議。

## <a name="sql-server-configuration"></a>SQL Server 組態

建議您安裝 SQL Server on Linux，若要達到最佳效能，您的應用程式之後，執行下列組態工作。

### <a name="best-practices"></a>最佳做法

- **使用節點和/或 Cpu 的處理序親和的性**

   建議使用`ALTER SERVER CONFIGURATION`設定`PROCESS AFFINITY`所有**NUMANODEs**及/或 Cpu 您使用 SQL Server （這通常是針對所有節點和 Cpu） 的 Linux 作業系統上。 處理器親和性可協助維護有效率的 Linux 和 SQL 排程行為。 使用**NUMANODE**選項是最簡單的方法。 請注意，您應該使用**處理序相似性**即使您電腦上有單一 NUMA 節點。  請參閱[ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)文件，如需有關如何設定**處理序相似性**。

- **設定多個 tempdb 資料檔案**

   因為安裝 Linux 上的 SQL Server 不提供一個選項來設定多個 tempdb 檔案，我們建議您考慮建立多個 tempdb 資料檔案安裝之後。 如需詳細資訊，請參閱本文件的指導方針[建議，可降低 SQL Server tempdb 資料庫中的配置競爭](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)。

### <a name="advanced-configuration"></a>進階的組態

下列建議是選擇性的組態設定，您可以選擇執行的 SQL Server on Linux 的安裝之後。 這些選項會根據您的工作負載和 Linux 作業系統的組態需求。

- **設定與 mssql conf 的記憶體限制**

   為了確保沒有足夠的可用實體記憶體適用於 Linux 作業系統，SQL Server 處理序預設會使用只有 80%的實體 RAM。 某些系統上的大量實體 RAM 的 20%可能會有大量。 例如，在系統上使用 1 TB 的 RAM，預設值會使約 200 GB 的 RAM 未使用。 在此情況下，您可能想要設定記憶體限制更高的值。 請參閱說明文件**mssql conf**工具和[memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit)設定控制顯示 （以 MB 為單位） 的 SQL Server 的記憶體。

   在變更此設定，請小心不要設定太高的值。 如果您未保留足夠的記憶體，您可能會導致 Linux 作業系統和其他 Linux 應用程式的問題。

## <a name="linux-os-configuration"></a>Linux 作業系統設定

請考慮使用下列 Linux 作業系統組態設定經驗的 SQL Server 安裝的最佳效能。

### <a name="kernel-settings-for-high-performance"></a>高效能的核心設定

這些是建議的 Linux 作業系統設定為高相關的效能和輸送量的 SQL Server 安裝。 請參閱您的 Linux 作業系統文件的程序來設定這些設定。



> [!Note]
> Red Hat Enterprise Linux (RHEL) 使用者的輸送量效能設定檔會設定這些設定自動 （除了 C 狀態）。

下表提供 CPU 設定的建議：

| 設定 | 值 | 詳細資訊 |
|---|---|---|
| CPU 頻率管理員 | 效能 | 請參閱**cpupower**命令 |
| ENERGY_PERF_BIAS | 效能 | 請參閱**x86_energy_perf_policy**命令 |
| min_perf_pct | 100 | 在 intel p 狀態上看到您的文件 |
| C 狀態 | 只有 C1 | 如何確保只有 C 狀態設為 C1 上看到您的 Linux 或系統文件 |

下表提供磁碟設定的建議：

| 設定 | 值 | 詳細資訊 |
|---|---|---|
| 磁碟 readahead | 4096 | 請參閱**blockdev**命令 |
| sysctl 設定 | kernel.sched_min_granularity_ns 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness=10 | 請參閱**sysctl**命令 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>平衡的多節點 NUMA 系統的核心設定自動 numa

如果您在多個節點上安裝 SQL Server **NUMA**系統中，下列**kernel.numa_balancing**預設會啟用核心的設定。 若要讓 SQL Server 上運作以最有效率**NUMA**系統，平衡多節點 NUMA 系統上停用自動 numa:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>虛擬位址空間的核心設定

預設值為**vm.max_map_count** （此為 65536） 可能無法夠高，SQL Server 安裝的。 （此為上限） 此值變更為 256 K。

```bash
sysctl -w vm.max_map_count 262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>停用上次存取日期/時間在檔案系統上的 SQL Server 資料和記錄檔

使用**noatime**具有任何用來儲存 SQL Server 資料和記錄檔的檔案系統屬性。 請參閱 Linux 的文件，有關如何設定這個屬性。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>保留透明龐大頁面 (THP) 啟用

大部分的 Linux 安裝應該對具有這個選項依預設。 我們建議您針對最一致效能體驗，請不要啟用此組態選項。

### <a name="swapfile"></a>交換檔

請確定您有已正確設定的交換檔，以避免任何記憶體不足問題。 請參閱您的 Linux 文件說明如何建立及正確調整大小的交換檔。

### <a name="virtual-machines-and-dynamic-memory"></a>虛擬機器和動態記憶體

如果您執行 SQL Server on Linux 的虛擬機器中，請確定您選取選項來修正虛擬機器保留的記憶體數量。 請勿使用等 HYPER-V 動態記憶體功能。

## <a name="next-steps"></a>後續的步驟

若要深入了解 SQL Server 功能可改善效能，請參閱[開始使用的效能功能](sql-server-linux-performance-get-started.md)。

如需有關 SQL Server on Linux，請參閱[概觀的 SQL Server on Linux](sql-server-linux-overview.md)。
