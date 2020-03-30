---
title: 設定持續性記憶體 (PMEM)
description: 本文提供在 Linux 上設定 PMEM 的逐步解說。
ms.custom: seo-lt-2019
author: briancarrig
ms.author: brcarrig
ms.date: 10/31/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 5d98b728a1966861532a30a4b5dd92824d25f1d5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76831965"
---
# <a name="configure-persistent-memory-pmem-for-sql-server-on-linux"></a>設定 Linux 上的 SQL Server 持續性記憶體 (PMEM)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文描述如何為 Linux 上的 [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 設定持續性記憶體 (PMEM)。

## <a name="overview"></a>概觀

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] 有一些使用持續性記憶體的記憶體內部功能。 本文件涵蓋針對 Linux 上 SQL Server 設定持續性記憶體的必要步驟。

> [!NOTE]
> 過去引進「啟用」  一詞是為了傳達使用持續性記憶體感知檔案系統的概念。 使用記憶體對應 (`mmap()`) 方便從使用者空間應用程式直接存取檔案系統。 建立檔案的記憶體對應後，應用程式即可完全略過 I/O 堆疊，發出載入/儲存指示。 就主機延伸模組應用程式的觀點而言，這可視為「啟用」檔案存取方法 (這是允許 SQLPAL 與 Windows 或 Linux 作業系統互動的黑箱程式碼)。

## <a name="create-namespaces-for-pmem-devices"></a>建立 PMEM 裝置的命名空間

### <a name="configure-the-devices"></a>設定裝置

在 Linux 中，使用 `ndctl` 公用程式。

- 安裝 `ndctl` 以設定 PMEM 裝置。 您可以在[這裡](https://docs.pmem.io/getting-started-guide/installing-ndctl)找到。
- 使用 `ndctl` 建立命名空間。 命名空間會跨各 PMEM NVDIMM 交錯，並可提供裝置記憶體區域的不同類型使用者空間存取權。 `fsdax` 是 SQL Server 的預設值及所需模式。

```bash 
ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=dev
```

請注意，我們已選擇 `fsdax` 模式，並正在使用系統記憶體來儲存每頁中繼資料。 建議使用 `--map=dev`。 這會將中繼資料直接儲存在命名空間中。 此時，使用 `--map=mem` 將中繼資料儲存在記憶體中會被視為具有實驗性。

使用 `ndctl` 來驗證命名空間。 
  
範例輸出如下：

```bash
# ndctl list -N
{
  "dev":"namespace0.0",
  "mode":"fsdax",
  "map":"dev",
  "size":4294967296,
  "sector_size":512,
  "blockdev":"pmem0",
  "numa_node":0
}
```

### <a name="create-and-mount-pmem-device"></a>建立並掛接 PMEM 裝置

例如，透過 XFS

```bash
mkfs.xfs -f /dev/pmem0
mount -o dax,noatime /dev/pmem0 /mnt/dax
xfs_io -c "extsize 2m" /mnt/dax
```

例如，透過 EXT4

```bash
mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
mount -o dax,noatime /dev/pmem0 /mnt/dax
```

## <a name="technical-considerations"></a>技術考量

- 如上所述，針對 XFS/EXT4 配置 2MB 的區塊
- 區塊配置和 `mmap` 未對齊會導致無訊息後援為 4KB
- 檔案大小應為 2MB 的倍數 (模數 2MB)
- 請勿停用透明的大型頁面 (THP) (根據預設，大部分的發佈都啟用)

一旦裝置以 `ndctl` 設定，並建立與裝載之後，您就可以將資料庫檔案放在其中或建立新的資料庫。

因為 PMEM 裝置為 O_DIRECT (直接 I/O) 安全，所以請考慮啟用追蹤旗標 3979 以停用強制的排清機制。 如需詳細資訊，請參閱 [FUA 支援](https://support.microsoft.com/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux)。 [FUA 內部](https://blogs.msdn.microsoft.com/bobsql/2018/12/18/sql-server-on-linux-forced-unit-access-fua-internals/)一文涵蓋強制單位存取內部。

## <a name="next-steps"></a>後續步驟

如需 Linux 上 SQL Server 的詳細資訊，請參閱 [Linux 上的 SQL Server](sql-server-linux-overview.md)。
如需 Linux 上的 SQL Server 效能最佳做法，請參閱[效能最佳做法](sql-server-linux-performance-best-practices.md)。
