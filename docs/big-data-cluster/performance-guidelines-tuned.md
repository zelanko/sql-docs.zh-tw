---
title: SQL Server 巨量資料叢集的效能最佳做法
description: 本文提供在 Kubernetes上執行 SQL Server 巨量資料叢集的效能最佳做法與指導方針
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: abb5a73f472ccefa53517c54a3d403af82d0beb2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906230"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-big-data-clusters"></a>SQL Server 巨量資料叢集的效能最佳做法與組態方針

[!INCLUDE [sqlserver2019](../includes/applies-to-version/sqlserver2019.md)]

本文提供最佳做法與建議，以最大化目標服務在巨量資料叢集內所執行應用程式的效能。

下列指導方針專注於設定 Linux 作業系統的建議，該系統裝載將在其中部署 BDC 的 Kubernetes 背景工作節點。 最佳做法是在部署巨量資料叢集之前，先設定微調設定檔。 建議的微調設定檔中所包含設定，已在 Microsoft 與 Intel 所進行的案例研究期間進行驗證。 此研究的結果會在此[白皮書](https://aka.ms/sql-bdc-spark-perf/)中發佈，以供下載。

> [!TIP]
> 如需 Linux 上 SQL Server 特定的微調組態，請參閱 [Linux 上的 SQL Server 效能最佳做法與組態方針](../linux/sql-server-linux-performance-best-practices.md)。 此外，其他最佳做法 (例如 SQL Server 資料庫的索引設計) 仍適用。

## <a name="proposed-linux-settings-using-a-tuned-mssql-bdc-profile"></a>使用經微調 `mssql-bdc` 設定檔的 Linux 建議設定

使用下列內容建立 **tuned.conf** 組態設定檔。

```bash
[main]
summary=Optimize for Microsoft SQL Server Big Data Clusters TPC-DS performance
include=throughput-performance
 
[sysctl]
#network tunings
net.ipv4.conf.default.rp_filter=1
net.ipv4.tcp_timestamps=0
net.ipv4.tcp_sack = 1
net.core.netdev_max_backlog = 25000
net.core.rmem_max = 2147483647
net.core.wmem_max = 2147483647
net.core.rmem_default = 33554431
net.core.wmem_default = 33554432
net.core.optmem_max = 33554432
net.ipv4.tcp_rmem =8192 33554432 2147483647
net.ipv4.tcp_wmem =8192 33554432 2147483647
net.ipv4.tcp_low_latency=1
net.ipv4.tcp_adv_win_scale=1
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv4.conf.all.arp_filter=1
net.ipv4.tcp_retries2=5
net.ipv6.conf.lo.disable_ipv6 = 1
net.core.somaxconn = 65535
 
#memory cache settings
vm.swappiness=1
vm.overcommit_memory=0
vm.dirty_background_ratio=1
 
#kernel NUMA
kernel.numa_balancing=0

#filesystem
fs.aio-max-nr=1048576
 
[vm]
#should be revisited for SQL large pages use in master/data/compute pods
transparent_hugepages=never
```

## <a name="install-tuned-utility-on-all-the-kubernetes-worker-nodes"></a>在所有 Kubernetes 背景工作節點上安裝**微調的**公用程式

若要安裝**微調的**公用程式，請執行：

```bash
apt-get -y install tuned
```

## <a name="apply-tuning-settings-to-all-kubernetes-worker-nodes"></a>將微調設定套用至所有 Kubernetes 背景工作節點

在每個目標背景工作節點上，複製上面所建立的 **tuned.conf** 檔案：

```bash
cd /usr/lib/tuned
scp -r <sourcePath> ./mssql-bdc
```

若要啟用此 **mssql-bdc** 微調的設定檔，請在所有 Kubernetes 背景工作節點上，將這些定義儲存於 `/usr/lib/tuned/mssql-bdc` 資料夾下的 **tuned.conf** 檔案，並允許該設定檔使用：

```bash
chmod +x /usr/lib/tuned/mssql-bdc/tuned.conf
tuned-adm profile mssql-bdc
```

使用此命令來驗證其是否已啟用：

```bash
tuned-adm active
```

或

```bash
tuned-adm list
```

若動態變更設定檔，則必須在所有受影響的背景工作節點上，將**微調的設定檔**重新開機，才能讓新的變更生效：

```bash
systemctl restart tuned
```
 
如需**微調**服務的記錄，請參閱 */var/log/tuned/tuned.log*。

您可選擇在 Kubernetes 叢集中的一個節點上設定微調設定檔，然後使用下列指令碼將其複製，並在其餘節點上設定。

```bash
#!/bin/bash -e
# This script takes a list of servers (IPs like `cat ~administrator/workerhosts)) as input
# and update these servers with the local version of mssql-bdc tuned.conf.
 
is_root() {
    local is_root_set=0
    if [ "$EUID" -ne 0 ]; then
        echo "Please run as root"
    else
        is_root_set=1
    fi
    return "${is_root_set}"
}
 
# function main
if is_root -eq 0; then
    exit 0
fi
 
while [ $# -gt 0 ]
do
    # sometimes, people add non-breaking space characters to their *host* files.
    WORKER_IP=$(echo "$1" | sed -e 's/\xC2\xA0//g')
    echo -e "updating mssql-bdc tuned on \e[42m${WORKER_IP}\e[0m"
    # the following commands assume tuned was not set up and active...
    # TODO: add the tuned install and status checks
    ssh "${WORKER_IP}" mkdir -p /usr/lib/tuned/mssql-bdc
    scp ~administrator/tuned.conf "${WORKER_IP}":/usr/lib/tuned/mssql-bdc/tuned.conf
    ssh "${WORKER_IP}" tuned-adm profile mssql-bdc
    ssh "${WORKER_IP}" systemctl restart tuned
    ssh "${WORKER_IP}" tuned-adm active
    shift
done

```

## <a name="next-steps"></a>後續步驟

如需更多資源，包括 SQL Server 巨量資料叢集的參考架構，請參閱：

* [案例研究：在 MS SQL Server 2019 巨量資料叢集中 Apache Spark 上執行的 SQL 工作負載](https://aka.ms/sql-bdc-spark-perf/)

* [HPE Reference Architecture for delivering insight across all your data with Microsoft SQL Server 2019 Big Data Clusters](https://h20195.www2.hpe.com/V2/GetDocument.aspx?docname=a50001963enw) (使用 Microsoft SQL Server 2019 巨量資料叢集以傳遞所有資料見解的 HPE 參考架構)

* [Dell EMC PowerStore：Microsoft SQL Server 2019 Big Data Clusters](https://www.dellemc.com/resources/en-us/asset/white-papers/products/storage/h18231-dell-emc-powerstore-sql-server-big-data-clusters.pdf) (Dell EMC PowerStore：Microsoft SQL Server 2019 巨量資料叢集)

* [Microsoft SQL Server 2019 Big Data Clusters:A Big Data Solution Using Dell EMC Infrastructure](https://infohub.delltechnologies.com/t/microsoft-sql-server-2019-big-data-clusters-a-big-data-solution-using-dell-emc-infrastructure/) (Microsoft SQL Server 2019 巨量資料叢集：使用 Dell EMC 基礎結構的巨量資料解決方案)

* [Microsoft SQL Server 2019 Big Data Clusters on Cisco UCS Reference Architecture](https://www.cisco.com/c/en/us/solutions/collateral/data-center-virtualization/unified-computing/sql-server-on-big-data-cluster-on-ucs.html) (Cisco UCS 參考架構上的 Microsoft SQL Server 2019 巨量資料叢集)