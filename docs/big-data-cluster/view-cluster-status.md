---
title: 檢視叢集狀態
titleSuffix: SQL Server big data clusters
description: 本文說明如何使用 Azure Data Studio、筆記本和 azdata 命令來查看 big data 叢集的狀態。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419284"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何查看 big data 叢集的狀態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何存取服務端點, 並查看 SQL Server big data cluster (預覽) 的狀態。 您可以同時使用 Azure Data Studio 和**azdata**, 這篇文章同時涵蓋這兩種技術。

## <a id="datastudio"></a>使用 Azure Data Studio

下載[Azure Data Studio](https://aka.ms/azdata-insiders)的最新內部人員**組建**之後, 您可以使用 [SQL Server big data cluster] 儀表板來查看服務端點和 big data 叢集的狀態。 請注意, 以下的部分功能僅適用于 Azure Data Studio 的內部人員組建。

1. 首先, 在 Azure Data Studio 中建立與您的 big data 叢集的連接。 如需詳細資訊, 請參閱[使用 Azure Data Studio 連接到 SQL Server big data](connect-to-big-data-cluster.md)叢集。

1. 以滑鼠右鍵按一下 [big data cluster] 端點, 然後按一下 [**管理**]。

   ![以滑鼠右鍵按一下 [管理]](media/view-cluster-status/right-click-manage.png)

1. 選取 [ **SQL Server Big Data cluster** ] 索引標籤, 以存取 big data cluster 儀表板。

   ![Big data cluster 儀表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服務端點

很重要的是, 您必須能夠輕鬆地存取大型資料叢集中的各種服務。 Big data cluster 儀表板提供服務端點資料表, 可讓您查看及複製服務端點。

![服務端點](media/view-cluster-status/service-endpoints.png)

前幾個資料列會公開下列服務:

- 應用程式 Proxy
- 叢集管理服務
- HDFS 和 Spark
- 管理 Proxy

當您需要端點連接到這些服務時, 這些服務會列出可複製及貼上的端點。 例如, 您可以按一下端點右邊的複製圖示, 然後將它貼入要求該端點的文字視窗中。 需要叢集管理服務端點, 才能執行叢集[狀態筆記本](#notebook)。

### <a name="dashboards"></a>儀表板

服務端點資料表也會公開數個儀表板來進行監視:

- 計量 (Grafana)
- 記錄檔 (Kibana)
- Spark 作業監視
- Spark 資源管理

您可以直接按一下這些連結。 在您連接到服務之前, 系統會要求您提供使用者名稱和密碼兩次。

### <a id="notebook"></a>叢集狀態筆記本

1. 您也可以藉由啟動叢集狀態筆記本, 來查看 big data 叢集的叢集狀態。 若要啟動筆記本, 請按一下 [叢集**狀態**] 工作。

    ![產品](media/view-cluster-status/cluster-status-launch.png)

2. 開始之前, 您將需要下列專案:

    - Big data 叢集名稱
    - 控制器使用者名稱
    - 控制器密碼
    - 控制器端點

    預設的 big data 叢集名稱是**mssql-** 叢集, 除非您在部署期間進行自訂。 您可以從 [服務端點] 資料表中的 [big data cluster] 儀表板找到控制器端點。 端點會列為 [叢集**管理服務**]。 如果您不知道認證, 請洽詢部署叢集的系統管理員。

3. 按一下頂端工具列上的 [**執行儲存格**]。

4. 依照提示輸入您的認證。 輸入 [big data 叢集名稱]、[控制器使用者名稱] 和 [控制器密碼] 的每個認證後, 按下 enter。

    > [!Note]
    > 如果您沒有設定海量資料的設定檔, 系統會要求您提供控制器端點。 輸入或貼上它, 然後按 ENTER 鍵以繼續。

5. 如果您成功連線, 則筆記本的其餘部分會顯示 big data 叢集每個元件的輸出。 當您想要重新執行特定的程式碼資料格時, 請將滑鼠停留在程式碼資料格上, 然後按一下 [**執行**] 圖示。

## <a name="use-azdata"></a>使用 azdata

您也可以使用[azdata](deploy-install-azdata.md)命令來同時查看端點和叢集狀態。

### <a name="service-endpoints"></a>服務端點

您可以使用下列步驟, 取得 big data 叢集之外部端點的 IP 位址。

1. 查看下列**kubectl**命令的外部 ip 輸出, 以尋找控制器端點的 ip 位址:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未在部署期間變更預設名稱, 請在`-n mssql-cluster`上一個命令中使用。 **mssql-** 叢集是 big data cluster 的預設名稱。

1. 使用[azdata 登](reference-azdata.md)入來登入 big data 叢集。 將 **--controller-endpoint**參數設定為控制器端點的外部 IP 位址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定在部署期間為控制器設定的使用者名稱和密碼 (CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD)。

1. 執行[azdata bdc 端點清單](reference-azdata-bdc-endpoint.md)來取得清單, 其中包含每個端點的描述及其對應的 IP 位址和埠值。 

   ```bash
   azdata bdc endpoint list -o table
   ```

   下列清單顯示此命令的範例輸出:

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

您可以使用 [ [azdata bdc status show](reference-azdata-bdc-status.md) ] 命令來查看叢集的狀態。

```bash
azdata bdc status show -o table
```

> [!TIP]
> 若要執行狀態命令, 您必須先使用**azdata login**命令進行登入, 這會顯示在先前的端點一節中。

以下顯示此命令的範例輸出:

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

### <a name="view-pool-status"></a>視圖集區狀態

您可以使用 [ [azdata bdc pool status show](reference-azdata-bdc-pool-status.md) ] 命令來查看叢集中的集區狀態。 若要使用此命令, 請使用`--kind`參數指定集區的類型。 集區類型如下:

- 密集型
- data
- master
- 引起
- 容量

例如, 下列命令會顯示存放集區的集區狀態:

```bash
azdata bdc pool status show --kind storage
```

您應該會看到類似下列輸出的文字:

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

`logsUrl`值會連結至具有記錄資訊的 kibana 儀表板:

![Kibana 儀表板](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl` 和`sqlMetricsUrl`值會連結至 grafana 儀表板, 以監視節點健全狀況和 SQL 計量:

![Grafana 儀表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>查看控制器狀態

您可以使用 [ [azdata bdc 控制狀態顯示](reference-azdata-bdc-control-status.md)] 命令來查看控制器狀態。 它提供與大型資料叢集的控制器節點相關之監視儀表板的類似連結。

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server big data](big-data-cluster-overview.md)叢集。
