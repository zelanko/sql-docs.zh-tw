---
title: 檢視叢集狀態
titleSuffix: SQL Server big data clusters
description: 這篇文章說明如何使用 Azure Data Studio、 筆記型電腦和 mssqlctl 命令的巨量資料叢集的狀態。
author: yualan
ms.author: alayu
manager: jroth
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2edd49c37655d420cf8022677c0d0287028a0b93
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413965"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何檢視的巨量資料叢集狀態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何存取服務端點，並檢視 SQL Server 的巨量資料叢集 （預覽） 的狀態。 您可以使用這兩個 Azure Data Studio 並**mssqlctl**，和本文章涵蓋這兩種技巧。

## <a id="datastudio"></a> 使用 Azure Data Studio

下載最新版本後**測試人員組建**的[Azure Data Studio](https://aka.ms/azdata-insiders)，您可以檢視服務端點，而且叢集與 SQL Server 巨量資料叢集儀表板的巨量資料的狀態。 請注意，下列功能的一些僅第一次使用 Azure Data Studio 的測試人員組建中。

1. 首先，建立在 Azure 資料 Studio 中的巨量資料叢集的連線。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 巨量資料叢集使用 Azure Data Studio](connect-to-big-data-cluster.md)。

1. 以滑鼠右鍵按一下巨量資料叢集端點，然後按一下 **管理**。

   ![以滑鼠右鍵按一下管理](media/view-cluster-status/right-click-manage.png)

1. 選取 [ **SQL Server 巨量資料叢集**存取巨量資料叢集儀表板] 索引標籤。

   ![巨量資料叢集儀表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服務端點

請務必要能夠輕鬆地存取巨量資料叢集內的各種服務。 巨量資料叢集儀表板會提供可讓您查看，並複製 服務端點的服務端點資料表。

![服務端點](media/view-cluster-status/service-endpoints.png)

第一次的數個資料列會公開下列服務：

- 應用程式 Proxy
- 叢集管理服務
- HDFS 和 Spark
- 管理 Proxy

這些服務會列出可以複製及貼上，當您連接到這些服務需要端點的端點。 比方說，您可以按一下複製圖示右邊的端點，並再將其貼入文字視窗，要求該端點。 叢集管理服務端點，才能執行[叢集狀態 notebook](#notebook)。

### <a name="dashboards"></a>儀表板

服務端點資料表也會公開數個儀表板監視：

- 計量 (Grafana)
- 記錄檔 (Kibana)
- Spark 作業監視
- Spark 資源管理

您可以直接按一下這些連結。 系統會要求您兩次連線到服務之前，提供您的使用者名稱和密碼。

### <a id="notebook"></a> 叢集狀態 notebook

1. 您也可以啟動叢集狀態 notebook，以檢視叢集狀態的巨量資料叢集。 若要啟動的 notebook，按一下**叢集狀態**工作。

    ![啟動](media/view-cluster-status/cluster-status-launch.png)

2. 在開始之前，您將需要下列項目：

    - 巨量資料叢集名稱
    - 控制器的使用者名稱
    - 控制站密碼
    - 控制器端點

    預設的巨量資料叢集名稱是**mssql 叢集**除非您在部署期間自訂它。 您可以尋找控制器端點從巨量資料叢集儀表板中的服務端點的資料表。 端點會列為**叢集管理服務**。 如果您不知道認證，要求的系統管理員將叢集部署。

3. 按一下 **執行的資料格**頂端的工具列上。

4. 請依照下列提示字元中，輸入您的認證。 按下的按 ENTER 鍵之後輸入每個巨量資料叢集名稱、 控制器名稱和控制站密碼的認證。

    > [!Note]
    > 如果您沒有與您的巨量資料設定檔安裝程式，將要求的控制站的端點。 輸入或貼上，然後按 ENTER，以繼續。

5. 如果您連線成功時，筆記本的其餘部分會顯示巨量資料叢集的每個元件的輸出。 當您想要重新執行特定程式碼單元時，將滑鼠停留在程式碼儲存格上方，然後按一下**執行**圖示。

## <a name="use-mssqlctl"></a>使用 mssqlctl

您也可以使用[mssqlctl](deploy-install-mssqlctl.md)命令以檢視端點和叢集狀態。

### <a name="service-endpoints"></a>服務端點

您可以取得使用下列步驟的巨量資料叢集的外部端點的 IP 位址。

1. 來看看下列的外部 IP 輸出中尋找控制器端點的 IP 位址**kubectl**命令：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您沒有在部署期間變更預設名稱，使用`-n mssql-cluster`中前一個命令。 **mssql 叢集**是巨量資料叢集的預設名稱。

1. 登入的巨量資料叢集[mssqlctl 登入](reference-mssqlctl.md)。 設定 **-控制站端點**參數來控制站端點的外部 IP 位址。

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   在部署期間指定的使用者名稱和您設定控制站 （CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD） 的密碼。

1. 執行[mssqlctl bdc 端點清單](reference-mssqlctl-bdc-endpoint.md)來取得每個端點和其對應的 IP 位址和連接埠值的描述與清單。 

   ```bash
   mssqlctl bdc endpoint list -o table
   ```

   下列清單顯示此命令的範例輸出：

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

### <a name="view-cluster-status"></a>檢視叢集狀態

您可以檢視與叢集的狀態[mssqlctl bdc 狀態顯示](reference-mssqlctl-bdc-status.md)命令。

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> 若要執行狀態的命令，您必須先登入**mssqlctl 登入**上的 「 端點 」 一節中所示的命令。

下圖顯示此命令的範例輸出：

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

### <a name="view-pool-status"></a>檢視集區狀態

您可以檢視與叢集內的集區的狀態[mssqlctl bdc 集區狀態顯示](reference-mssqlctl-bdc-pool-status.md)命令。 若要使用此命令，指定集區的型別`--kind`參數。 集區類型為：

- 計算
- data
- master
- Spark
- 儲存體

例如，下列命令會顯示存放集區的集區狀態：

```bash
mssqlctl bdc pool status show --kind storage
```

您應該會看到類似下列輸出的文字：

```output
[
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/logs/ui",
    "name": "storage-0-0",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/sqlmetrics/ui",
    "state": "Running"
  },
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/logs/ui",
    "name": "storage-0-1",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/sqlmetrics/ui",
    "state": "Running"
  }
]
```

`logsUrl`值 kibana 儀表板與記錄資訊的連結：

![kibana 儀表板](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl`和`sqlMetricsUrl`值連結至的 grafana 儀表板監視節點健全狀況和 SQL 計量：

![Grafana 儀表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>檢視控制器的狀態

您可以檢視與控制器狀態[mssqlctl bdc 控制項狀態顯示](reference-mssqlctl-bdc-control-status.md)命令。 它提供類似的巨量資料叢集的控制站節點相關的監視儀表板的連結。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 的巨量資料叢集](big-data-cluster-overview.md)。
