---
title: 檢視叢集狀態
titleSuffix: SQL Server big data clusters
description: 本文說明如何使用 Azure Data Studio、Notebook 和 azdata 命令來檢視巨量資料叢集的狀態。
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f5b3b210cb4e20bdf9585a7efdfd0f10aa19f29
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725779"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>如何檢視巨量資料叢集的狀態 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文描述如何存取服務端點，並檢視 SQL Server 巨量資料叢集元件的狀態。 您可以同時使用 Azure Data Studio 和 **azdata**，本文同時涵蓋這兩種技術。

## <a name="use-azure-data-studio"></a><a id="datastudio"></a> 使用 Azure Data Studio

下載 [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) 的最新**測試人員組建**之後，您可以使用 SQL Server 巨量資料叢集儀表板來檢視服務端點和巨量資料叢集的狀態。 以下部分功能僅先在 Azure Data Studio 的測試人員組建中提供。

1. 首先，在 Azure Data Studio 中建立與您巨量資料叢集的連線。 如需詳細資訊，請參閱[使用 Azure Data Studio 連線至 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)。

1. 以滑鼠右鍵按一下巨量資料叢集端點，然後按一下 [管理]  。

   ![以滑鼠右鍵按一下 [管理]](media/view-cluster-status/right-click-manage.png)

1. 選取 [SQL Server 巨量資料叢集]  索引標籤以存取巨量資料叢集儀表板。

   ![巨量資料叢集儀表板](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>服務端點

能夠輕鬆存取巨量資料叢集中的各種服務十分重要。 巨量資料叢集儀表板提供服務端點資料表，可讓您查看並複製服務端點。

![服務端點](media/view-cluster-status/service-endpoints.png)

當您需要端點以連線至這些服務時，這些服務會列出可複製及貼上的端點。 例如，您可以按一下端點右側的複製圖示，然後將其貼入要求該端點的文字視窗中。 若要執行[叢集狀態筆記本](#notebook)，叢集管理服務端點是必要的。

### <a name="dashboards"></a>儀表板

服務端點資料表也會公開數個儀表板以進行監視：

- 計量 (Grafana)
- 記錄 (Kibana)
- Spark 作業監視
- Spark 資源管理

您可以直接按一下這些連結。 存取下列儀表板時，您必須進行驗證。 針對計量和記錄儀表板，請提供您在部署時使用 **AZDATA_USERNAME** 和 **AZDATA_PASSWORD** 環境變數所設定的控制器系統管理員認證。 Spark 儀表板將使用閘道 (Knox) 認證：可為叢集中與 AD 整合的 AD 身分識別，或 **AZDATA_USERNAME** 與 **AZDATA_PASSWORD** (若叢集中使用基本驗證)。

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

### <a name="cluster-status-notebook"></a><a id="notebook"></a> 叢集狀態筆記本

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

5. 如果您成功連線，筆記本其餘部分會顯示巨量資料叢集每個元件的輸出。 當您想要重新執行特定程式碼儲存格時，請將滑鼠停留在程式碼儲存格上，然後按一下**執行**圖示。

## <a name="use-azdata"></a>使用 azdata

您也可以使用 [azdata](../azdata/install/deploy-install-azdata.md) 命令來同時檢視端點和叢集狀態。

### <a name="service-endpoints"></a>服務端點

1. 使用 [azdata login](../azdata/reference/reference-azdata.md) 來登入巨量資料叢集。 將 **--controller-endpoint** 參數設定為控制器端點的外部 IP 位址。

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   指定您在部署期間為控制器所設定的使用者名稱和密碼 (AZDATA_USERNAME 和 AZDATA_PASSWORD)。 
   若為 AD 驗證，命令為：

  ```bash
   azdata login --endpoint https://<control_domain_name>:30080 --auth ad
   ```

1. 請執行 [`azdata bdc endpoint list`](../azdata/reference/reference-azdata-bdc-endpoint.md) 以取得一份清單，其中包含每個端點的描述及其對應 IP 位址和連接埠值。 

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

您可以使用 [`azdata bdc status show`](../azdata/reference/reference-azdata-bdc-status.md) 命令來檢視叢集的狀態。

```bash
azdata bdc status show
```

> [!TIP]
> 若要執行狀態命令，您必須先使用 **azdata login** 命令登入，此動作已於先前的端點一節中示範過。

下列顯示此命令的範例輸出：

```output
 Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 spark          ready    healthy         -
 sql            ready    healthy         -
 hdfs           ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 zookeeper       ready    healthy         StatefulSet zookeeper is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         StatefulSet controldb is healthy
 control         ready    healthy         ReplicaSet control is healthy
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
 controlwd       ready    healthy         ReplicaSet controlwd is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

### <a name="view-specific-resource-status"></a>檢視特定資源狀態

您可以使用 [azdata bdc status show](../azdata/reference/reference-azdata-bdc-status.md) 命令來檢視叢集內特定資源的狀態。 當您使用此命令時，可以使用 `--resource` 參數進行篩選。 `--resource` 參數的幾個輸入範例包括：

- master
- 控制
- compute-0
- storage-0
- gateway

例如，下列命令會顯示儲存集區的狀態：

```bash
azdata bdc status show --all --resource storage-0
```

若要查看正在執行特定服務的所有元件狀態，您必須使用對應的命令群組 `azdata bdc <serviceName> status show`。 例如：

- azdata bdc sql status show --all
- azdata bdc hdfs status show --all
- azdata bdc spark status show --all

以下是範例輸出：

```output
  Storage-0: ready                                                                                                                                                                                                    Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Instances: running                                                                                                                                                                                                  Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


 Dashboards
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Name            Url

 nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
 sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
 logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
 ```

> [!TIP]
> 執行 status 命令與 `--all` 參數以取得其他健全狀況詳細資料，包括對應至特定執行個體的計量和記錄儀表板連結。 以下是使用 `--all` 參數時的範例輸出：

```output
 Spark: ready                                                                                                                                                                                                        Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sparkhead Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 sparkhead-0     running  healthy         Pod sparkhead-0 is healthy
 sparkhead-1     running  healthy         Pod sparkhead-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/logs/ui


 Storage-0 Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
```

`logsUrl` 值會連結至 Kibana 儀表板：

![Kibana 儀表板](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> (舊版) Microsoft Edge 瀏覽器 iOS 與 Kibana 不相容，您必須使用以 Chromium 為基礎的瀏覽器，儀表板才能正常顯示。 當您使用不支援的瀏覽器載入儀表板時，會看到空白頁面。 如需 Kibana 支援的瀏覽器，請參閱這裡。

`nodeMetricsUrl` 和 `sqlMetricsUrl` 值會連結至 Grafana 儀表板，以監視 Kubernetes 節點計量和巨量資料叢集服務計量：

![Grafana 儀表板](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>檢視控制器狀態

您可以使用 [`azdata bdc control status show`](../azdata/reference/reference-azdata-bdc-control-status.md) 命令來檢視控制器狀態。 該命令可提供監視儀表板的類似連結，這些監視儀表板與巨量資料叢集的控制器元件相關。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。