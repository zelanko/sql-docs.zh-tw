---
title: 部署的資源
titleSuffix: SQL Server Big Data Clusters
description: 描述一般部署在 SQL Server 巨量資料叢集中的 Pod。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ad3cc263ea81b9e3bda5cb34ea27cfabba1ae716
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730711"
---
# <a name="resources-deployed-with-big-data-cluster"></a>以巨量資料叢集部署的資源

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文描述 SQL Server 巨量資料叢集所部署的資源。

巨量資料叢集會根據部署設定檔來部署 Pod。 如需詳細資料，請參閱[預設組態](deployment-guidance.md#configfile)。 

本文描述以 `aks-dev-test-ha` 設定檔部署的 Pod，並包含 Spark 集區。 查詢 Kubernetes 以查看部署在叢集中的 Pod。 下列範例會傳回特定命名空間下的 Pod 清單。

```bash
kubectl get pods -n <namespace>
```

將 `<namespace>` 替換為您的巨量資料叢集名稱。 

如需詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md#configfile)。

下圖顯示部署在巨量資料叢集中的元件：

:::image type="content" source="media/big-data-cluster-overview/architecture-diagram-overview.png" alt-text="巨量資料叢集圖表":::

如需架構的資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)。

## <a name="deployed-pods"></a>部署的 Pod

下表列出部署在巨量資料叢集中的 Pod。

|名稱  |區域|
|---------|---------|
|`control-<nnnn>`        |[控制](#control)|
|`controldb-<#>`         |[控制](#control)|
|`controlwd-<nnnn>`      |[控制](#control)|
|`logsdb-<#>`            |[控制](#control)|
|`logsui-<nnnn>`         |[控制](#control)|
|`metricsdb-<#>`         |[控制](#control)|
|`metricsdc-<nnnn>`      |[控制](#control)|
|`metricsui-<nnnn>`      |[控制](#control)|
|`mgmtproxy-<nnnn>`      |[控制](#control)|
|`zookeeper-<#>`         |[控制](#control)|
|`dns-<nnnn>`            |[控制](#control)|
|`master-<#n>`           |[主要執行個體](#master-instance)|
|`operator-<nnnn>`       |[主要執行個體](#master-instance)
|`compute-<#n>-<#m>`     |[計算集區](#compute-pool)|
|`data-<#>-<#>`          |[資料集區](#data-pool) |
|`storage-<#>-<#>`       |[存放集區](#storage-pool)|
|`nmnode-<#>-<#>`        |[存放集區](#storage-pool)|
|`sparkhead-<#>`         |[存放集區](#storage-pool)|
|`appproxy-<#m>`         |[應用程式集區](#application-pool)|
|`gateway-<#>`           |[閘道器服務](#gateway-service)|

並非每個 BDC 叢集中都會包含所有的 Pod。 高可用性部署或 Active Directory 整合會包含特定的 Pod。 

### <a name="high-availability-specific-pods"></a>高可用性特定的 Pod：

- `operator-<nnnn>`
- `zookeeper-<#>`

### <a name="active-directory-specific-pods"></a>Active Directory 特定的 Pod：

- `dns-<nnnn>`

下列各節描述這些 Pod，並列出每個 Pod 中的容器。

## <a name="control"></a>控制

控制 Pod 提供控制服務。

|Pod 名稱 |Count| Kubernetes 控制器類型 | 容器 |
|--------|----|------|--------|-------|
|`control-#`|1| ReplicaSet |- `controller`<br><br>- `security-support`<br><br>- `fluentbit`
|`controldb`|1| StatefulSet |- `mssql-server`<br><br>- `fluentbit`
|`controlwd`|1|  ReplicaSet |- `controlwatchdog`
|`logsdb-#` |1| StatefulSet |- `elasticsearch`
|`logsui`   |1| ReplicaSet |- `kibana`
|`metricsdb-#`|1| StatefulSet |- `influxdb`
|`metricsdc`|每個 Kubernetes 節點 1 個。 | DaemonSet |- `telegraf` |
|`metricsui-nnnn`|1| ReplicaSet |- `grafana` |
|`mgmtproxy-nnnn`|1| ReplicaSet |- `service-proxy`<br><br>- `fluentbit`|
|`dns-nnnn`|0 或 1 (如需 Active Directory 整合)| ReplicaSet |- `dns`<br><br>- `fluentbit`|

## <a name="master-instance"></a>主要執行個體

`master-<#n>` 是 SQL Server 主要執行個體。

- 透過 DDL 管理資料集區
- 透過 DML 操作資料集區中的資料
- 將分析查詢執行卸載到資料集區

|Pod 名稱 |Count| Kubernetes 控制器類型 | 容器 |
|--------|----|------|--------|
|`master-<#n>`|1 或更多 (如需高可用性)。| StatefulSet|- `mssql-server`<br><br>- `fluentbit`<br><br>- `collectd`<br><br>- `mssql-ha-supervisor` <sup>*</sup>|
|`operator`<sup>*</sup>| 0 或 1 (如需高可用性) | ReplicaSet |- `mssql-ha-operator`

<sup>*</sup> 僅限高可用性部署。 此運算子會實作及註冊 SQL Server 和可用性群組資源的自訂資源定義。 此運算子會在部署後自動註冊為接聽項，以在 Kubernetes 叢集中要部署 SQL Server 資源時收到通知。 `mssql-ha-supervisor` 支援可用性群組。

每個 `master` Pod 都會包含一個 SQL Server 執行個體。 高可用性部署包含 3 個 Pod。 每個 Pod 都會包含一個 SQL Server 執行個體，其中具有 SQL Server Always On 可用性群組中的所有資料庫。

視工作負載而定，在部署時會包含其他 Pod。 

## <a name="compute-pool"></a>計算集區

計算集區提供用於計算的 SQL Server 執行個體。

|Pod 名稱 |Count| Kubernetes 控制器類型 | 容器 |
|--------|----|------|--------|
|`compute-<#n>-<#m>`|1 或更多。| StatefulSet |- `mssql-server`<br><br>- `fluentbit`<br><br>- `collectd`

- `#n` 會識別計算集區。
- `#m` 會識別集區內的執行個體識別碼。

計算集區 SQL Server 執行個體為無狀態。 只需要 `tempdb` 的儲存空間。

視工作負載而定，在部署時會包含其他 Pod。 

## <a name="data-pool"></a>資料集區

資料集區提供用於儲存和計算的 SQL Server 執行個體。

|Pod 名稱 |Count| Kubernetes 控制器類型 | 容器 |
|--------|----|------|--------|-------|
|`data-<#n>-<#m>` | 0 或更多 | StatefulSet | -` mssql-server` <br><br>- `fluentbit`<br><br>- `collectd`|

- `#n` 會識別資料集區。
- `#m` 會識別集區內的執行個體識別碼。

視工作負載而定，在部署時會包含其他 Pod。

## <a name="storage-pool"></a>儲存體集區

存放集區可供透過 Spark 進行資料擷取、在 HDFS 中儲存，以及透過 HDFS 和 SQL Server 端點進行資料存取。

|Pod 名稱 |Count| Kubernetes 控制器類型 | 容器 |
|--------|----|------|--------|
|`storage-0-#`|1 或更多。 視工作負載而定，在部署時會包含其他 Pod。 | StatefulSet |- `hadoop`<br><br>- `mssql-server`<br><br>- `fluentbit`<br><br>
|`nmnode-0-#`|1 或更多 (如需高可用性)| StatefulSet |- `hadoop`<br><br>- `fluentbit`
|`sparkehead-#`|1 或更多 (如需高可用性)| StatefulSet |- `hadoop-yarn-jobhistory`<br><br>- `hadoop-livy-sparkhistory`<br><br>- `hadoop-hivemetastore`<br><br>-- `fluentbit`
|`zookeeper`|0 或 3 (如需高可用性)。 | StatefulSet |- `zookeeper`<br><br>- `fluentbit`

## <a name="application-pool"></a>應用程式集區

部分測試組態設定檔中包含應用程式集區。 應用程式集區會裝載在部署巨量資料叢集的應用程式時所定義應用程式服務 Proxy。 

`appproxy` 是位於應用程式集區應用程式前方的 Web API。 其會驗證使用者，然後將要求路由傳送至應用程式。

|Pod 名稱 | Kubernetes 控制器類型 | 容器  |
|--------|----|------|
|`appproxy`| ReplicaSet |- `app-service-proxy`<br><br>- `fluentbit`

如需詳細資訊，請參閱[什麼是巨量資料叢集上的應用程式部署](concept-application-deployment.md)。

視工作負載而定，在部署時會包含其他 Pod。 

## <a name="gateway-service"></a>閘道器服務

閘道服務為 Spark、HDFS、[Yarn](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html)、Yarn UI 和 Spark UI 提供 Knox 閘道。

|Pod 名稱 | Kubernetes 控制器類型 | 容器 |
|--------|-----|-----|
|`gateway-<#>`| StatefulSet |- `knox`<br><br>- `fluentbit`

僅支援一個閘道。

## <a name="open-source-container-references"></a>開放原始碼容器參考

有些容器是由開放原始碼專案所開發。 如需所使用開放原始碼容器的資訊，請參閱：

- [Elasticsearch](https://www.elastic.co/)
- [Kibana](https://www.elastic.co/kibana)
- [InfluxDB](https://www.influxdata.com)
- [Grafana](https://grafana.com/)
- [Fluent Bit](https://docs.fluentbit.io/manual/about/what-is-fluent-bit)
- [HDFS DataNode](concept-storage-pool.md)
- [HDFS NameNode](https://cwiki.apache.org/confluence/display/HADOOP2/NameNode) 
- [Spark](configure-spark-hdfs.md)
- [ZooKeeper](https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/) 


## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列資源：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters) \(英文\)
- [如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md#configfile)
