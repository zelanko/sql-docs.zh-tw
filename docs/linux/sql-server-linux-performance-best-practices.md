---
title: 在 Linux 上的 SQL Server 的效能最佳做法 |Microsoft Docs
description: 這篇文章提供在 Linux 上執行 SQL Server 2017 的效能最佳做法和方針。
author: rgward
ms.author: bobward
manager: craigg
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: f27cda67baa5d4101f94a8351bacd1ef3ecbff05
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101136"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>效能最佳做法和 Linux 上的 SQL Server 組態指導方針

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文章提供最佳作法和建議，以連接到 Linux 上的 SQL Server 的資料庫應用程式的效能最大化。 這些建議專屬於 Linux 平台上執行。 所有標準 SQL Server 的建議，例如索引設計仍適用。

下列指導方針包含 SQL Server 和 Linux 作業系統設定的建議。

## <a name="sql-server-configuration"></a>SQL Server 組態

建議您若要達到最佳效能，您的應用程式的 Linux 上安裝 SQL Server 之後，請執行下列設定工作。

### <a name="best-practices"></a>最佳做法

- **使用節點及/或 Cpu 的處理序相似性**

   建議使用`ALTER SERVER CONFIGURATION`來設定`PROCESS AFFINITY`所有**NUMANODEs**和/或 Cpu 您使用 SQL Server （這通常是針對所有節點和 Cpu） 的 Linux 作業系統上。 處理器親和性可協助維護有效率的 Linux 和 SQL 排程行為。 使用**NUMANODE**選項是最簡單的方法。 請注意，您應該使用**處理序相似性**即使您電腦上有單一 NUMA 節點。  請參閱[ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)如需有關如何設定的文件**處理序相似性**。

- **設定多個 tempdb 資料檔案**

   因為 Linux 安裝上的 SQL Server 不提供一個選項來設定多個 tempdb 檔案，我們建議您考慮在安裝後建立多個 tempdb 資料檔案。 如需詳細資訊，請參閱本文件的指導方針[減少配置爭用情況，在 SQL Server tempdb 資料庫中的建議](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)。

### <a name="advanced-configuration"></a>進階的組態

下列建議是，您可以選擇在 Linux 上的 SQL Server 的安裝後執行選擇性的組態設定。 這些選項會根據您的工作負載和設定 Linux 作業系統的需求而定。

- **設定使用 mssql-conf 的記憶體限制**

   為了確保沒有足夠的可用實體記憶體適用於 Linux 作業系統，SQL Server 處理序預設會使用只有 80%的實體 RAM。 某些系統上的大量實體 RAM 的 20%可能為數可觀。 比方說，在系統上使用 1 TB 的 RAM 的預設設定會保留大約 200 GB 的 RAM 未使用。 在此情況下，您可能想要設定記憶體限制較高的值。 請參閱文件**mssql conf**工具並[memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit)設定控制顯示 （單位為 MB） 的 SQL Server 的記憶體。

   在變更此設定，請小心不要設定太高的值。 如果您未保留足夠的記憶體，可能會發生與 Linux 作業系統和其他 Linux 應用程式的問題。

## <a name="linux-os-configuration"></a>Linux OS 設定

請考慮使用下列的 Linux 作業系統組態設定經驗的 SQL Server 安裝的最佳效能。

### <a name="kernel-settings-for-high-performance"></a>高效能的核心設定
這些是建議的 Linux 作業系統設定為 [高] 相關的效能和輸送量的 SQL Server 安裝。 請參閱您的 Linux 作業系統文件的程序來設定這些設定。



> [!Note]
> 針對 Red Hat Enterprise Linux (RHEL) 使用者，輸送量效能設定檔將這些設定自動 （除了 C 狀態）。

下表提供 CPU 設定的建議：

| 設定 | 值 | 詳細資訊 |
|---|---|---|
| CPU 頻率管理員 | 效能 | 請參閱**cpupower**命令 |
| ENERGY_PERF_BIAS | 效能 | 請參閱**x86_energy_perf_policy**命令 |
| min_perf_pct | 100 | Intel p 狀態上看到您的文件 |
| C 狀態 | 只有 C1 | 如何確保只有 C 狀態設為 C1 上看到您的 Linux 或 system 文件 |

下表提供磁碟設定的建議：

| 設定 | 值 | 詳細資訊 |
|---|---|---|
| 磁碟 readahead | 4096 | 請參閱**blockdev**命令 |
| sysctl 設定 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness=10 | 請參閱**sysctl**命令 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>平衡多節點 NUMA 系統的核心設定自動 numa

如果您在多節點上安裝 SQL Server **NUMA**系統，下列**kernel.numa_balancing**預設會啟用核心設定。 若要允許來操作以最有效率的 SQL Server **NUMA**系統中，平衡多節點 NUMA 系統上停用自動 numa:

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>虛擬位址空間的核心設定

預設值**vm.max_map_count** （此為 65536） 可能無法夠高，SQL Server 安裝。 （這是最高的上限） 此值變更為 256 K。

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>停用上次存取日期/時間的檔案系統上的 SQL Server 資料和記錄檔

使用**noatime**使用任何用來儲存 SQL Server 資料和記錄檔的檔案系統的屬性。 請參閱您的 Linux 文件，有關如何設定這個屬性。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>保留透明大型頁面 (THP) 啟用

大部分的 Linux 安裝應該有這個選項預設情況下。 我們建議將啟用此組態選項保持最一致的效能體驗。

### <a name="swapfile"></a>分頁檔

請確定您已設定正確的分頁檔，以避免任何記憶體不足的問題。 請參閱如何建立和適當的大小分頁檔您 Linux 文件。

### <a name="virtual-machines-and-dynamic-memory"></a>虛擬機器 」 與 「 動態記憶體

如果您執行在 Linux 上的 SQL Server 虛擬機器中，請確定您選取選項來修正虛擬機器保留的記憶體數量。 請勿使用像是 HYPER-V 動態記憶體功能。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 功能可改善效能，請參閱[開始使用效能功能](sql-server-linux-performance-get-started.md)。

在 Linux 上 SQL Server 的相關資訊，請參閱[概觀的 SQL Server on Linux](sql-server-linux-overview.md)。
