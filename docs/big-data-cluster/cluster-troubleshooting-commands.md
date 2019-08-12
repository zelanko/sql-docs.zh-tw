---
title: 監視和疑難排解
titleSuffix: SQL Server big data clusters
description: 此文章提供用來監視和針對 SQL Server 2019 巨量資料叢集 (預覽) 進行疑難排解的實用命令。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ccdfe31f7873c44ea09e273d5d9afb2361f9b36b
ms.sourcegitcommit: 9702dd51410dd610842d3576b24c0ff78cdf65dc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68841556"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>監視 SQL Server 巨量資料叢集並進行疑難排解

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

此文章說明數個實用的 Kubernetes 命令，可讓您用來監視和針對 SQL Server 2019 巨量資料叢集 (預覽) 進行疑難排解。 它會示範如何檢視位於巨量資料叢集中的 Pod 或其他 Kubernetes 成品的深入詳細資料。 此文章也涵蓋一般工作，例如，將檔案複製到執行其中一項 SQL Server 巨量資料叢集服務的容器，或從其中複製檔案。

> [!TIP]
> 在 Windows (cmd or PS) 或 Linux (bash) 用戶端電腦上執行下列 **kubectl** 命令。 它們需要叢集中先前的驗證，以及要執行的目標叢集內容。 例如，針對先前建立的 AKS 叢集，您可以執行 `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` 來下載 Kubernetes 叢集組態檔並設定叢集內容。

## <a name="get-status-of-pods"></a>取得 Pod 的狀態

您可以使用 `kubectl get pods` 命令來取得所有命名空間或巨量資料叢集命名空間之叢集中的 Pod 狀態。 下列各節顯示兩者的範例。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>顯示 Kubernetes 叢集中所有 Pod 的狀態

執行下列命令來取得所有 Pod 及其狀態，包括屬於命名空間的 Pod，而這些命名空間其中建立了 SQL Server 巨量資料叢集 Pod：

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>顯示 SQL Server 巨量資料叢集中所有 Pod 的狀態

使用 `-n` 參數來指定特定的命名空間。 請注意，SQL Server 巨量資料叢集 Pod 會根據部署組態檔中指定的叢集名稱，在叢集啟動程式期間建立的新命名空間中建立。 這裡會使用預設名稱 `mssql-cluster`。

```bash
kubectl get pods -n mssql-cluster
```

對於執行中的巨量資料叢集，您應該會看到類似下列清單的輸出：

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> 在部署期間，[狀態] 為 **ContainerCreating** 的 Pod 仍會上線。 如果部署因任何原因而停止回應，這可能會讓您了解問題所在。 另請查看 [就緒] 資料行。 這會告訴您已在 Pod 中啟動多少容器。 請注意，部署可能需要 30 分鐘或更久的時間，視您的設定和網路而定。 在這段時間內，大部分會花在下載不同元件的容器映像。

## <a name="get-pod-details"></a>取得 Pod 詳細資料

執行下列命令，以取得特定 Pod 的詳細描述 (JSON 格式輸出)。 其中包含詳細資料，例如 Pod 所在的目前 Kubernetes 節點、在 Pod 中執行的容器，以及用來啟動容器的映像。 它也會顯示其他詳細資料，例如與 Pod 相關聯的標籤、狀態和持續性磁碟區宣告。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

下列範例會在名為 `mssql-cluster` 的巨量資料叢集中顯示 `master-0` Pod 的詳細資料：

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

如果發生任何錯誤，您有時可以在最新的 Pod 事件中看到錯誤。

## <a name="get-pod-logs"></a>取得 Pod 記錄

您可以取出在 Pod 中執行之容器的記錄。 下列命令會取出在 Pod `master-0` 中執行之所有容器的記錄，並將其以檔案名稱 `master-0-pod-logs.txt` 輸出：

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluster > master-0-pod-logs.txt
```

## <a id="services"></a> 取得服務的狀態

執行下列命令，以取得巨量資料叢集服務的詳細資料。 這些詳細資料包含其類型，以及與個別服務和連接埠相關聯的 IP。 請注意，SQL Server 巨量資料叢集服務會根據部署設定檔中指定的叢集名稱，於叢集啟動程式期間建立的新命名空間中建立。

```bash
kubectl get svc -n <namespace_name>
```

下列範例會顯示巨量資料叢集 (名稱為 `mssql-cluster`) 中的服務狀態：

```bash
kubectl get svc -n mssql-cluster
```

下列服務支援對巨量資料叢集的外部連線：

| 服務 | 描述 |
|---|---|
| **master-svc-external** | 提供主要執行個體的存取權。<br/>(**EXTERNAL-IP,31433** 和 **SA** 使用者) |
| **controller-svc-external** | 支援管理叢集的工具和用戶端。 |
| **gateway-svc-external** | 提供 HDFS/Spark 閘道的存取權。<br/>(**EXTERNAL-IP** 和 **root** 使用者) |
| **appproxy-svc-external** | 支援應用程式部署情節。 |

> [!TIP]
> 這是使用 **kubectl** 來檢視服務的方法，但也可以使用 `azdata bdc endpoint list` 命令來檢視這些端點。 如需詳細資訊，請參閱[取得巨量資料叢集端點](deployment-guidance.md#endpoints)。

## <a name="get-service-details"></a>取得服務詳細資料

執行此命令以取得服務的詳細描述 (JSON 格式輸出)。 其中會包含標籤、選取器、IP、外部 IP (如果服務是 LoadBalancer 類型)、連接埠等詳細資料。

```bash
kubectl describe service <service_name> -n <namespace_name>
```

下列範例會取出 **master-svc-external** 服務的詳細資料：

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a id="copy"></a> 複製檔案

如果您需要將檔案從容器複製到本機電腦，請使用 `kubectl cp` 命令搭配下列語法：

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

同樣地，您可以使用 `kubectl cp` 將檔案從本機電腦複製到特定的容器。

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> 從容器複製檔案

下列範例會將 SQL Server 記錄檔從容器複製到本機電腦上的 `~/temp/sqlserverlogs` 路徑 (在此範例中，本機電腦是 Linux 用戶端)：

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> 將檔案複製到容器

下列範例會將 **AdventureWorks2016CTP3.bak** 檔案從本機電腦複製到 `master-0` Pod 中的 SQL Server 主要執行個體容器 (`mssql-server`)。 檔案會複製到容器中的 `/tmp` 目錄。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> 強制刪除 Pod
 
不建議您強制刪除 Pod。 但是，若要測試可用性、復原或資料持續性，您可以使用 `kubectl delete pods` 命令刪除 Pod 以模擬 Pod 失敗。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

下列範例會刪除存放集區 Pod `storage-0-0`：

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> 取得 Pod IP
 
基於疑難排解目的，您可能需要取得 Pod 目前執行所在節點的 IP。 若要取得 IP 位址，請使用 `kubectl get pods` 命令搭配下列語法：

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

下列範例會取得 `master-0` Pod 執行所在節點的 IP 位址：

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Kubernetes 儀表板

您可以啟動 Kubernetes 儀表板，以取得叢集的其他相關資訊。 下列各節說明如何在 AKS 上啟動 Kubernetes 儀表板，以及使用 kubeadm 來進行 Kubernetes 啟動程序。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>在 AKS 中執行叢集時啟動儀表板

若要啟動 Kubernetes 儀表板，請執行：

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 如果您收到下列錯誤訊息：*Unable to listen on port 8001:All listeners failed to create with the following errors:Unable to create listener:Error listen tcp4 127.0.0.1:8001: >bind:Only one usage of each socket address (protocol/network address/port) is normally permitted.Unable to create listener:Error listen tcp6: address [[::1]]:8001: missing port in >address error:Unable to listen on any of the requested ports: [{8001 9090}]* ，請確定您沒有從另一個視窗啟動儀表板。

當您在瀏覽器上啟動儀表板時，您可能會因為在 AKS 叢集中預設啟用 RBAC 而收到許可權警告，而且儀表板所使用的服務帳戶沒有足夠的許可權可以存取所有資源 (例如，*pods is forbidden:User "system:serviceaccount:kube-system:kubernetes-dashboard" cannot list pods in the namespace "default"* )。 執行下列命令，將所需的許可權授與 `kubernetes-dashboard`，然後重新啟動儀表板：

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>使用 kubeadm 啟動 Kubernetes 叢集時啟動儀表板

如需如何在 Kubernetes 叢集中部署及設定儀表板的詳細指示，請參閱 [Kubernetes 文件](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) \(英文\)。 若要啟動 Kubernetes 儀表板，請執行此命令：

```bash
kubectl proxy
```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集](big-data-cluster-overview.md)。
