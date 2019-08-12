---
title: Linux 上的 SQL Server 的效能最佳作法
description: 此文章提供了在 Linux 上執行 SQL Server 的效能最佳作法和方針。
author: rgward
ms.author: bobward
ms.reviewer: vanto
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 543488eada46a088f3c634ce2326c7e2db2a97a5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68105446"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Linux 上 SQL Server 的效能最佳作法和設定方針

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章提供最佳作法和建議，以最大化連線至 Linux 上的 SQL Server 之資料庫應用程式的效能。 這些建議僅適用於在 Linux 平台上執行。 所有一般 SQL Server 建議 (例如索引設計) 仍然適用。

下列方針包含設定 SQL Server 和 Linux 作業系統的建議。

## <a name="sql-server-configuration"></a>SQL Server 設定

建議您在安裝 Linux 上的 SQL Server 之後執行下列設定工作，以達到應用程式的最佳效能。

### <a name="best-practices"></a>最佳做法

- **針對節點和/或 CPU 使用處理程序親和性**

   建議使用 `ALTER SERVER CONFIGURATION` 為 Linux 作業系統上用於 SQL Server (通常用於所有 NODE 和 CPU) 的所有 **NUMANODE** 和/或CPU 設定 `PROCESS AFFINITY`。 處理程序親和性有助於維護有效率的 Linux 和 SQL 排程行為。 使用 **NUMANODE** 選項是最簡單的方法。 請注意，即使您的電腦上只有一個 NUMA 節點，您還是應該使用**處理程序親和性**。  如需如何設定**處理程序親和性**的詳細資訊，請參閱 [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)。

- **設定多個 tempdb 資料檔案**

   由於 Linux 上的 SQL Server 安裝未提供設定多個 tempdb 檔案的選項，因此建議您在安裝之後，考慮建立多個 tempdb 資料檔案。 如需詳細資訊，請參閱文章中的指導方針[避免 SQL Server tempdb 資料庫中配置爭用的建議](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d) \(機器翻譯\)。

### <a name="advanced-configuration"></a>進階設定

下列建議是選擇性的組態設定，您可以選擇在安裝 Linux 上的 SQL Server 之後執行。 這些選擇是根據您的工作負載和 Linux 作業系統設定的需求而定。

- **使用 mssql-conf 設定記憶體限制**

   為了確保 Linux 作業系統有足夠的可用實體記憶體，SQL Server 處理序預設只會使用 80% 的實體 RAM。 對於大量實體 RAM 的某些系統，20% 可能是很大的數字。 例如，在具有 1 TB RAM 的系統上，預設設定會保留大約 200 GB 的 RAM (未使用)。 在此情況下，您可能會想要將記憶體限制設定為較高的值。 請參閱有關 **mssql-conf** 工具的文件，以及控制 SQL Server 可見記憶體的 [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) 設定 (以 MB 為單位)。

   變更此設定時，請小心不要將這個值設得太高。 如果您沒有保留足夠的記憶體，您可能會遇到 Linux 作業系統和其他 Linux 應用程式的問題。

## <a name="linux-os-configuration"></a>Linux OS 設定

請考慮使用下列 Linux 作業系統組態設定，以體驗 SQL Server 安裝的最佳效能。

### <a name="kernel-settings-for-high-performance"></a>高效能的核心設定
這些是建議的 Linux 作業系統設定，與 SQL Server 安裝的高效能和輸送量相關。 如需設定這些設定的程序，請參閱您的 Linux 作業系統文件。



> [!Note]
> 針對 Red Hat Enterprise Linux (RHEL) 使用者，輸送量-效能設定檔會自動設定這些設定 (除了 C-States 以外)。

下表提供 CPU 設定的建議：

| 設定 | ReplTest1 | 詳細資訊 |
|---|---|---|
| CPU 頻率管理員 | 效能 | 請參閱 **cpupower** 命令 |
| ENERGY_PERF_BIAS | 效能 | 請參閱 **x86_energy_perf_policy** 命令 |
| min_perf_pct | 100 | 請參閱 intel p-state 相關文件 |
| C-States | 僅限 C1 | 請參閱您的 Linux 或系統文件，以了解如何確保 C-States 設定為 [僅限 C1] |

下表提供磁碟設定的建議：

| 設定 | ReplTest1 | 詳細資訊 |
|---|---|---|
| 磁碟預先讀取 | 4096 | 請參閱 **blockdev** 命令 |
| sysctl 設定 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | 請參閱 **sysctl** 命令 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>多節點 NUMA 系統的核心設定自動 NUMA 平衡

如果您將 SQL Server 安裝在多節點的 **NUMA** 系統上，則預設會啟用下列 **kernel.numa_balancing** 核心設定。 若要允許 SQL Server 在 **NUMA** 系統上以最高效率運作，請在多節點 NUMA 系統上停用自動 NUMA 平衡：

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>虛擬位址空間的核心設定

**vm.max_map_count** 的預設設定 (也就是 65536) 可能不足以安裝 SQL Server。 將此值 (這是一個上限) 變更為 256K。

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>針對 SQL Server 資料和記錄檔，在檔案系統上停用上次存取日期/時間

將 **noatime** 屬性與用來儲存 SQL Server 資料和記錄檔的任何檔案系統搭配使用。 請參閱您的 Linux 文件，以了解如何設定此屬性。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>讓透明大頁 (THP) 保持啟用

大部分的 Linux 安裝預設都應該為開啟此選項。 為了提供最一致的效能體驗，我們建議您讓此設定選項維持啟用狀態。

### <a name="swapfile"></a>交換檔

請確定您已正確設定交換檔，以避免發生記憶體不足的問題。 請參閱您的 Linux 文件，以了解如何建立和適當地調整交換檔大小。

### <a name="virtual-machines-and-dynamic-memory"></a>虛擬機器和動態記憶體

如果您是在虛擬機器中執行 Linux 上的 SQL Server，請務必選取選項來修正保留給虛擬機器的記憶體數量。 請勿使用 Hyper-V 動態記憶體這類功能。

## <a name="next-steps"></a>後續步驟

若要深入了解可改善效能的 SQL Server 功能，請參閱[開始使用效能功能](sql-server-linux-performance-get-started.md)。

如需 Linux 上的 SQL Server 詳細資訊，請參閱 [Linux 上的 SQL Server 概觀](sql-server-linux-overview.md)。
