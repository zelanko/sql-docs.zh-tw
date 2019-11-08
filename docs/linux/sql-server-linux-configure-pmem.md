---
title: 如何設定 Linux 上的 SQL Server 持續性記憶體 (PMEM)
description: 本文提供在 Linux 上設定 PMEM 的逐步解說。
author: briancarrig
ms.author: brcarrig
ms.reviewer: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6e1a935dcaa605caf9483fadd5707bafbfb6b83b
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531295"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>如何設定 Linux 上的 SQL Server 持續性記憶體 (PMEM)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文描述如何設定 Linux 上的 SQL Server 持續性記憶體 (PMEM)。 SQL Server 2019 已引進 Linux 上的 PMEM 支援。

## <a name="overview"></a>概觀

SQL Server 2016 引進了非揮發性 DIMM 的支援，以及稱為 [Tail of the Log Caching on NVDIMM]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/) (NVDIMM 上的記錄檔快取結尾) 的最佳化。 這些最佳化會減少將記錄緩衝區強化為永續性儲存體所需的作業數目。 這可以利用 Windows Server 直接存取 DAX 模式中的持續性記憶體裝置。

SQL Server 2019 將持續性記憶體 (PMEM) 裝置的支援擴充至 Linux，徹底強化放置在 PMEM 上的資料及交易記錄檔。 啟蒙是指使用有效率的使用者空間 `memcpy()` 作業，來存取存放裝置的方法。 SQL Server 利用 Linux 上的 DAX 支援 (而不是逐步執行檔案系統和儲存體堆疊) 直接將資料放入裝置，可降低延遲。

## <a name="enable-enlightenment-of-database-files"></a>啟用資料庫檔案的啟蒙
若要在 Linux 上 SQL Server 中啟用資料庫檔案的啟蒙，請遵循下列步驟：

1. 設定裝置。

  在 Linux 中，使用 `ndctl` 公用程式。

  - 安裝 `ndctl` 以設定 PMEM 裝置。 您可以在[這裡](https://docs.pmem.io/getting-started-guide/installing-ndctl)找到。
  - 使用 [ndctl] 來建立命名空間。

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >如果您使用的 `ndctl` 版本低於 59，則請使用 `--mode=memory`。

  使用 `ndctl` 來驗證命名空間。 範例輸出如下：

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - 建立並掛接 PMEM 裝置

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

  一旦裝置以 ndctl 設定，並格式化與掛接之後，您就可以將資料庫檔案放在其中。 您也可以建立新的資料庫 

1. 由於 PMEM 裝置是 O_DIRECT 安全的，所以請啟用追蹤旗標 3979 來停用強制的清除機制。 此追蹤旗標是啟動追蹤旗標，因此必須使用 mssql-conf 公用程式來啟用。 請注意，這是全伺服器的設定變更，如果您擁有任何 O_DIRECT 非相容裝置，而這些裝置需要強制清除機制來確保資料完整性，則不應使用此追蹤旗標。 如需詳細資訊，請參閱＜ https://support.microsoft.com/en-us/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux ＞。

1. 重新啟動 SQL Server。

## <a name="next-steps"></a>後續步驟

如需 Linux 上 SQL Server 的詳細資訊，請參閱 [Linux 上的 SQL Server](sql-server-linux-overview.md)。
