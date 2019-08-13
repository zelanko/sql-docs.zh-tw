---
title: 檢視叢集狀態
titleSuffix: SQL Server big data clusters
description: 本文說明如何使用 Azure Data Studio、Notebook 和 azdata 命令來檢視巨量資料叢集的狀態。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419284"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何檢視巨量資料叢集的狀態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述如何存取服務端點，並檢視 SQL Server 巨量資料叢集 (預覽) 的狀態。 您可以同時使用 Azure Data Studio 和 **azdata**，本文同時涵蓋這兩種技術。

## <a id="datastudio"></a> 使用 Azure Data Studio

下載 [Azure Data Studio](https://aka.ms/azdata-insiders) 的最新**測試人員組建**之後，您可以使用 SQL Server 巨量資料叢集儀表板來檢視服務端點和巨量資料叢集的狀態。 請注意，以下部分功能僅適用於 Azure Data Studio 的測試人員組建。

1. 首先，在 Azure Data Studio 中建立與您巨量資料叢集的連線。 如需詳細資訊，請參閱[使用 Azure Data Studio 連線至 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)。

1. 以滑鼠右鍵按一下巨量資料叢集端點，然後按一下 [管理]  。

   ![以滑鼠右鍵按一下 [管理]](media/view-cluster-status/right-click-manage.png)

1. 選取 [SQL Server 巨量資料叢集]  索引標籤以存取巨量資料叢集儀表板。

   ![巨量資料叢集儀表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服務端點

能夠輕鬆存取巨量資料叢集中的各種服務十分重要。 巨量資料叢集儀表板提供服務端點資料表，可讓您查看並複製服務端點。

![服務端點](media/view-cluster-status/service-endpoints.png)

前幾個資料列會公開下列服務：

- 應用程式 Proxy
- 叢集管理服務
- HDFS 和 Spark
- 管理 Proxy

當您需要端點以連線至這些服務時，這些服務會列出可複製及貼上的端點。 例如，您可以按一下端點右側的複製圖示，然後將其貼入要求該端點的文字視窗中。 若要執行[叢集狀態筆記本](#notebook)，叢集管理服務端點是必要的。

### <a name="dashboards"></a>儀表板

服務端點資料表也會公開數個儀表板以進行監視：

- 計量 (Grafana)
- 記錄 (Kibana)
- Spark 作業監視
- Spark 資源管理

您可以直接按一下這些連結。 在您連線至服務之前，系統會要求您提供使用者名稱和密碼兩次。

### <a id="notebook"></a> 叢集狀態筆記本

1. 您也可以藉由啟動 [叢集狀態] 筆記本來檢視巨量資料叢集的叢集狀態。 若要啟動筆記本，請按一下 [叢集狀態]  工作。

    ![啟動](media/view-cluster-status/cluster-status-launch.png)

2. 開始之前，您需要下列項目：

    - 巨量資料叢集名稱
    - 控制器使用者名稱
    - 控制器密碼
    - 控制器端點

    預設的巨量資料叢集名稱是 **mssql-cluster** (除非您在部署期間自訂名稱)。 您可以從 [服務端點] 資料表中的 [巨量資料叢集] 儀表板找到控制器端點。 端點會列為**叢集管理服務**。 如果您沒有認證資訊，請洽詢為您部署叢集的系統管理員。

3. 按一下頂端工具列上的 [執行資料格]  。

4. 遵循提示輸入您的認證。 在您為巨量資料叢集名稱、控制器使用者名稱和控制器密碼鍵入每個認證後，請按下 Enter。

    > [!Note]
    > 如果您沒有設定巨量資料的設定檔，系統會要求您提供控制器端點。 請鍵入或貼上控制器端點，然後按 Enter 鍵以繼續。

5. 如果您成功連線，筆記本其餘部分會顯示巨量資料叢集每個元件的輸出。 當您想要重新執行特定程式碼資料格時，請將滑鼠停留在程式碼資料格上，然後按一下 [執行]  圖示。

## <a name="use-azdata"></a>使用 azdata

您也可以使用 [azdata](deploy-install-azdata.md) 命令來同時檢視端點和叢集狀態。

### <a name="service-endpoints"></a>服務端點

您可以使用下列步驟來取得巨量資料叢集的外部端點 IP 位址。

1. 查看下列 **kubectl** 命令的外部 IP 輸出，以尋找控制器端點的 IP 位址：

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > 如果您未在部署期間變更預設名稱，則在上一個命令中使用 `-n mssql-cluster`。 **mssql-cluster** 是巨量資料叢集的預設名稱。

1. 使用 [azdata login](reference-azdata.md) 來登入巨量資料叢集。 將 **--controller-endpoint** 參數設定為控制器端點的外部 IP 位址。

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   指定您在部署期間為控制器所設定的使用者名稱和密碼 (CONTROLLER_USERNAME 和 CONTROLLER_PASSWORD)。

1. 執行 [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) 來取得一份清單，其中包含每個端點的描述及其對應 IP 位址和連接埠值。 

   ```bash
   azdata bdc endpoint list -o table
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

您可以使用 [azdata bdc status show](reference-azdata-bdc-status.md) 命令來檢視叢集的狀態。

```bash
azdata bdc status show -o table
```

> [!TIP]
> 若要執行狀態命令，您必須先使用 **azdata login** 命令登入，此動作已於先前的端點一節中示範過。

下列顯示此命令的範例輸出：

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

您可以使用 [azdata bdc pool status show](reference-azdata-bdc-pool-status.md) 命令來檢視叢集內的集區狀態。 若要使用此命令，請使用 `--kind` 參數指定集區的類型。 集區類型如下：

- 計算
- data
- master
- Spark
- 儲存

例如，下列命令會顯示儲存集區的集區狀態：

```bash
azdata bdc pool status show --kind storage
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

`logsUrl` 值會連結至具有記錄資訊的 Kibana 儀表板：

![Kibana 儀表板](./media/view-cluster-status/kibana-dashboard.png)

`nodeMetricsUrl` 和 `sqlMetricsUrl` 值會連結至 Grafana 儀表板以監視節點健康狀態和 SQL 計量：

![Grafana 儀表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>檢視控制器狀態

您可以使用 [azdata bdc status show](reference-azdata-bdc-control-status.md) 命令來檢視叢集的狀態。 該命令提供與巨量資料叢集控制器節點相關之監視儀表板的類似連結。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集](big-data-cluster-overview.md)。
