---
title: 監視和疑難排解
titleSuffix: SQL Server big data clusters
description: 本文提供用來監視和疑難排解 SQL Server 2019 big data cluster (預覽) 的實用命令。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 272249b7bd6c22895b7d10e7fbce4a20cb647a49
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419476"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>監視和疑難排解 SQL Server big data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明數個實用的 Kubernetes 命令, 可讓您用來監視和疑難排解 SQL Server 2019 big data cluster (預覽)。 它會示範如何查看位於大型資料叢集中的 pod 或其他 Kubernetes 成品的深入詳細資料。 本文也涵蓋一般工作, 例如, 將檔案複製到執行其中一項 SQL Server big data cluster 服務的容器或從其中複製檔案。

> [!TIP]
> 在 Windows (cmd 或 PS) 或 Linux (bash) 用戶端電腦上執行下列**kubectl**命令。 它們需要在叢集中進行先前的驗證, 並使用叢集內容來執行。 例如, 針對先前建立的 AKS 叢集, 您可以執行`az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>`來下載 Kubernetes 叢集設定檔並設定叢集內容。

## <a name="get-status-of-pods"></a>取得 pod 的狀態

您可以使用`kubectl get pods`命令來取得所有命名空間或 big data cluster 命名空間的叢集中 pod 的狀態。 下列各節顯示兩者的範例。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>顯示 Kubernetes 叢集中所有 pod 的狀態

執行下列命令來取得所有 pod 及其狀態, 包括屬於命名空間的 pod, 而這些 pod 是 SQL Server big data cluster pod 建立在其中:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>顯示 SQL Server big data 叢集中所有 pod 的狀態

`-n`使用參數來指定特定的命名空間。 請注意, 根據部署設定檔中指定的叢集名稱, 在叢集啟動程式期間建立的新命名空間中, 會建立 SQL Server big data cluster pod。 這裡會使用預設`mssql-cluster`名稱。

```bash
kubectl get pods -n mssql-cluster
```

您應該會看到類似下列清單的輸出, 其中會顯示執行中的 big data 叢集:

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
> 在部署期間, 具有 ContainerCreating**狀態**的 pod 仍會上線。 如果部署因任何原因而停止回應, 這可能會讓您瞭解問題所在。 另請查看 [**就緒**] 資料行。 這會告訴您已在 pod 中啟動多少容器。 請注意, 部署可能需要30分鐘或更久的時間, 視您的設定和網路而定。 在這段時間內, 大部分會花在下載不同元件的容器映射。

## <a name="get-pod-details"></a>取得 pod 詳細資料

執行下列命令, 以取得 JSON 格式輸出中特定 pod 的詳細描述。 其中包含詳細資料, 例如 pod 所在的目前 Kubernetes 節點、在 pod 中執行的容器, 以及用來啟動容器的映射。 它也會顯示其他詳細資料, 例如與 pod 相關聯的標籤、狀態和持續性磁片區宣告。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

下列範例會在名為`master-0` `mssql-cluster`的 big data 叢集中顯示 pod 的詳細資料:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

如果發生任何錯誤, 您有時可以在最新的 pod 事件中看到錯誤。

## <a name="get-pod-logs"></a>取得 pod 記錄

您可以抓取在 pod 中執行之容器的記錄檔。 下列命令會抓取在 pod `master-0`中`master-0-pod-logs.txt`執行之所有容器的記錄檔, 並將其輸出至檔案名:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a>取得服務的狀態

執行下列命令以取得 big data cluster 服務的詳細資料。 這些詳細資料包含其類型, 以及與個別服務和埠相關聯的 Ip。 請注意, SQL Server big data 叢集服務會根據部署設定檔中指定的叢集名稱, 建立于叢集啟動程式期間建立的新命名空間中。

```bash
kubectl get svc -n <namespace_name>
```

下列範例會顯示名`mssql-cluster`為的大型資料叢集中服務的狀態:

```bash
kubectl get svc -n mssql-cluster
```

下列服務支援對 big data cluster 的外部連線:

| 服務 | 描述 |
|---|---|
| **master-svc-external** | 提供主要實例的存取權。<br/>(**外部 IP、31433來**和**SA**使用者) |
| **controller-svc-external** | 支援管理叢集的工具和用戶端。 |
| **gateway-svc-external** | 提供 HDFS/Spark 閘道的存取權。<br/>(**外部 IP**和**根**使用者) |
| **appproxy-svc-external** | 支援應用程式部署案例。 |

> [!TIP]
> 這是使用**kubectl**來查看服務的方法, 但也可以使用`azdata bdc endpoint list`命令來查看這些端點。 如需詳細資訊, 請參閱[取得 big data 叢集端點](deployment-guidance.md#endpoints)。

## <a name="get-service-details"></a>取得服務詳細資料

執行此命令以取得 JSON 格式輸出中服務的詳細描述。 其中會包含標籤、選取器、IP、外部 IP (如果服務是 LoadBalancer 類型)、埠等等等詳細資料。

```bash
kubectl describe service <service_name> -n <namespace_name>
```

下列範例會抓取**主要-svc-外部**服務的詳細資料:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>在容器中執行命令

如果現有的工具或基礎結構無法讓您執行特定工作, 而不是實際在容器的內容中, 您可以使用`kubectl exec`命令來登入容器。 例如, 您可能需要檢查特定檔案是否存在, 或者您可能需要重新開機容器中的服務。 

若要使用`kubectl exec`命令, 請使用下列語法:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

下列兩節提供兩個範例, 說明如何在特定容器中執行命令。

### <a id="restartsql"></a>登入特定容器, 然後重新開機 SQL Server 進程

下列範例示範如何在`mssql-server` `master-0` pod 的容器中重新開機 SQL Server 進程:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a>登入特定容器並重新啟動容器中的服務
 
下列範例顯示如何重新開機**supervisord**所管理的所有服務: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a>複製檔案

如果您需要將檔案從容器複製到本機電腦, 請使用`kubectl cp`命令搭配下列語法:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

同樣地, 您可以`kubectl cp`使用, 將檔案從本機電腦複製到特定的容器。

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a>從容器複製檔案

下列範例會將 SQL Server 記錄檔從容器複製到本機電腦`~/temp/sqlserverlogs`上的路徑 (在此範例中, 本機電腦是 Linux 用戶端):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a>將檔案複製到容器中

下列範例會將**來自 adventureworks2016ctp3**的檔案從本機電腦複製到`mssql-server` `master-0` pod 中的 SQL Server 主要實例容器 ()。 檔案會複製到容器中`/tmp`的目錄。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a>強制刪除 pod
 
不建議您強制刪除 pod。 但若要測試可用性、復原或資料持續性, 您可以使用`kubectl delete pods`命令刪除 pod 以模擬 pod 失敗。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

下列範例會刪除存放集區 pod `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a>取得 pod IP
 
基於疑難排解目的, 您可能需要取得 pod 目前執行所在節點的 IP。 若要取得 IP 位址, 請使用`kubectl get pods`命令搭配下列語法:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

下列範例會取得`master-0` pod 執行所在節點的 IP 位址:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Kubernetes 儀表板

您可以啟動 Kubernetes 儀表板, 以取得叢集的其他相關資訊。 下列各節說明如何在 AKS 上啟動 Kubernetes 的儀表板, 以及使用 kubeadm 來進行 Kubernetes 引導。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>在 AKS 中執行叢集時啟動儀表板

若要啟動 Kubernetes 儀表板, 請執行:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 如果您收到下列錯誤:*無法接聽埠 8001:所有接聽程式都無法建立, 發生下列錯誤:無法建立接聽程式:錯誤接聽 tcp4 127.0.0.1: 8001: > bind:通常只允許每個通訊端位址 (通訊協定/網路位址/埠) 的其中一種使用方式。無法建立接聽程式:接聽 tcp6 時發生錯誤: 位址 [[:: 1]]: 8001: > 位址錯誤中遺漏埠:無法接聽任何要求的埠: [{8001 9090}]* , 請確定您未從另一個視窗啟動儀表板。

當您在瀏覽器上啟動儀表板時, 您可能會因為預設在 AKS 叢集中啟用 RBAC 而收到許可權警告, 而且儀表板所使用的服務帳戶沒有足夠的許可權可以存取所有資源 (例如, *禁止 pod:使用者 "system: serviceaccount: kube-system: kubernetes-儀表板" 無法列出命名空間 "default"* 中的 pod)。 執行下列命令, 將所需的許可權授`kubernetes-dashboard`與, 然後重新開機儀表板:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>使用 kubeadm 啟動 Kubernetes 叢集時啟動儀表板

如需如何在 Kubernetes 叢集中部署及設定儀表板的詳細指示, 請參閱[Kubernetes 檔](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)。 若要啟動 Kubernetes 儀表板, 請執行此命令:

```bash
kubectl proxy
```

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server big data](big-data-cluster-overview.md)叢集。
