---
title: 監視和疑難排解
titleSuffix: SQL Server big data clusters
description: 本文章提供有用的命令，來監視和疑難排解 SQL Server 2019 巨量資料叢集 （預覽）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 0548176a191d5c2b16b113b5a931a1ed0435741c
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472302"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>監視和疑難排解 SQL Server 的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文會說明數個實用的 Kubernetes 命令可用來監視和疑難排解 SQL Server 2019 巨量資料叢集 （預覽）。 它會顯示如何檢視 pod 或其他位於巨量資料叢集的 Kubernetes 成品的詳細資料。 本文也涵蓋常見工作，例如將檔案複製或從執行的其中一個 SQL Server 的巨量資料叢集服務的容器。

> [!TIP]
> 執行下列**kubectl** （cmd 或 PS） 的 Windows 或 Linux (bash) 用戶端電腦上的命令。 它們需要先前叢集和叢集內容，對執行中的驗證。 例如，先前建立的 AKS 叢集您可以執行`az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>`下載 Kubernetes 叢集組態檔，並設定叢集內容。

## <a name="get-status-of-pods"></a>取得 pod 的狀態

您可以使用`kubectl get pods`命令，以取得所有命名空間或巨量資料叢集命名空間的叢集中的 pod 的狀態。 下列各節顯示兩者的範例。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>在 Kubernetes 叢集中的所有 pod 的顯示狀態

執行下列命令來取得所有 pod 和其狀態，包括屬於命名空間的 pod 巨量資料叢集的 pod 建立於該 SQL Server:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>在 SQL Server 的巨量資料叢集中顯示的所有 pod 的狀態

使用`-n`參數來指定特定的命名空間。 請注意，在部署組態檔中指定的叢集名稱為基礎的叢集啟動程序時建立的新命名空間中建立 SQL Server 巨量資料叢集的 pod。 預設名稱， `mssql-cluster`，這裡會使用。

```bash
kubectl get pods -n mssql-cluster
```

您應該會看到類似下列的清單，以執行巨量資料叢集的輸出：

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
> 在部署期間，pod 數與**狀態**的**ContainerCreating**仍即將推出。 如果部署停止回應，因為任何原因，這可讓您了解可能的問題。 也看看**準備**資料行。 這會告訴您的 pod 中啟動多少容器。 請注意，部署可能需要 30 分鐘以上，取決於您的組態和網路。 這個時間大部分都是花在下載不同元件的容器映像。

## <a name="get-pod-details"></a>取得 pod 的詳細資料

執行下列命令來取得 JSON 格式輸出中的特定 pod 的詳細的描述。 它包含詳細資料，例如目前執行中 pod，以及用來啟動容器的映像的容器放置 pod，Kubernetes 節點。 也會顯示其他詳細資訊，例如標籤、 狀態，並保存 pod 相關聯的磁碟區宣告。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

下列範例顯示的詳細資料`master-0`中名為巨量資料叢集的 pod `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

如果發生任何錯誤，您有時可以看到 pod 的最新事件中的錯誤訊息。

## <a name="get-pod-logs"></a>取得 pod 記錄檔

您可以擷取執行的 pod 中容器的記錄檔。 下列命令會擷取名為 pod 中執行的所有容器的記錄檔`master-0`並將其輸出的檔案名稱`master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a> 取得服務狀態

執行下列命令來取得巨量資料叢集服務的詳細資料。 這些詳細資料包括其類型，並使用個別的服務和連接埠相關聯的 Ip。 請注意，在部署組態檔中指定的叢集名稱為基礎的叢集啟動程序時建立的新命名空間中建立 SQL Server 的巨量資料叢集服務。

```bash
kubectl get svc -n <namespace_name>
```

下列範例會顯示服務的狀態中名為巨量資料叢集`mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

支援巨量資料叢集的外部連線的服務如下：

| 服務 | 描述 |
|---|---|
| **master-svc-external** | 提供存取權的主要執行個體。<br/>(**EXTERNAL-IP，31433**並**SA**使用者) |
| **controller-svc-external** | 支援工具和管理叢集的用戶端。 |
| **mgmtproxy-svc-external** | 提供存取權[叢集管理網站](cluster-admin-portal.md)。<br/>(https://**EXTERNAL-IP**: 30777/入口網站) |
| **gateway-svc-external** | 可存取 HDFS/Spark 閘道。<br/>(**EXTERNAL-IP**並**根**使用者) |
| **appproxy-svc-external** | 支援應用程式的部署案例。 |

> [!TIP]
> 這是一種檢視的服務**kubectl**，但也可以使用`mssqlctl cluster endpoints list`命令來檢視這些端點。 如需詳細資訊，請參閱 <<c0> [ 取得巨量資料叢集端點](deployment-guidance.md#endpoints)。

## <a name="get-service-details"></a>取得服務詳細資料

執行此命令來取得 JSON 格式輸出中的一項服務的詳細的描述。 它會包含詳細資料例如標籤、 選取器中，IP、 外部 IP （如果服務的負載平衡器的型別）、 連接埠等。

```bash
kubectl describe service <service_name> -n <namespace_name>
```

下列範例會擷取詳細資料**主要 svc 外部**服務：

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>在容器中執行的命令

如果現有的工具或基礎結構不會讓您執行特定工作，而不實際是在容器的內容，您可以登入容器使用`kubectl exec`命令。 例如，您可能需要檢查是否有特定的檔案，或您可能需要重新啟動服務容器中。 

若要使用`kubectl exec`命令，請使用下列語法：

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

下列兩節會提供特定容器中執行命令的兩個範例。

### <a id="restartsql"></a> 登入特定的容器，然後重新啟動 SQL Server 處理序

下列範例示範如何重新啟動 SQL Server 處理序`mssql-server`容器中的`master-0`pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> 登入特定的容器，並在容器中重新啟動服務
 
下列範例示範如何重新啟動所有服務，受**監督**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a> 將檔案複製

如果您要將容器中的檔案複製到本機電腦，使用`kubectl cp`命令搭配下列語法：

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

同樣地，您可以使用`kubectl cp`將檔案從本機電腦複製到特定的容器。

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> 將檔案從一個容器

下列範例會將 SQL Server 記錄檔複製到容器`~/temp/sqlserverlogs`（在此範例中，本機電腦是 Linux 用戶端） 的本機電腦上的路徑：

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> 將檔案複製到容器

下列範例複製**將 AdventureWorks2016CTP3.bak**至 SQL Server 的主要執行個體容器從本機電腦檔案 (`mssql-server`) 中`master-0`pod。 將檔案複製到`/tmp`目錄中的容器。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> 強制刪除 pod
 
它不被建議強制刪除 pod。 測試可用性、 復原或資料持續性，您可以刪除 pod 來模擬 pod 失敗但`kubectl delete pods`命令。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

下列範例會刪除儲存體集區的 pod， `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> 取得 pod IP
 
如需疑難排解用途，您可能需要取得 pod 目前執行所在節點的 IP。 若要取得的 IP 位址，請使用`kubectl get pods`命令搭配下列語法：

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

下列範例會取得節點的 IP 位址， `master-0` pod 上執行：

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="cluster-administration-portal"></a>叢集系統管理入口網站

使用[叢集管理網站](cluster-admin-portal.md)來監視您的巨量資料叢集的狀態。 例如，在部署中，您可以使用**部署** 索引標籤。您必須等到**mgmtproxy svc 外部**服務存取此入口網站，讓其無法在部署開始之前啟動。

## <a name="kubernetes-dashboard"></a>Kubernetes 儀表板

您可以啟動 Kubernetes 儀表板，如需有關叢集的詳細資訊。 下列各節說明如何在 AKS 的 Kubernetes 和 Kubernetes 啟動使用 kubeadm 啟動儀表板。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>當叢集正在執行 AKS 中啟動儀表板

若要啟動 Kubernetes 儀表板執行：

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 如果您收到下列錯誤：*無法接聽連接埠 8001 來：所有的接聽程式無法建立因下列錯誤：無法建立接聽程式：錯誤接聽 tcp4 127.0.0.1:8001: > 繫結：通常允許只有一個使用的每個通訊端位址 （網路通訊協定/位址/連接埠）。無法建立接聽程式：錯誤接聽 tcp6： 位址 [[:: 1]]: 8001： 遺漏中的連接埠 > 解決錯誤：無法在任何要求的連接埠上接聽: [{8001 9090}]*，請確定您沒有啟動儀表板已經從另一個視窗。

當您在 在您的瀏覽器上啟動 儀表板時，您可能會因為在 AKS 叢集中，預設為啟用的 RBAC 權限警告而儀表板所使用的服務帳戶沒有足夠的權限存取的所有資源 (例如*禁止 pod:使用者"系統： serviceaccount:kube-系統： kubernetes-儀表板上 「 無法列出 「 預設 」 的命名空間中的 pod*)。 執行下列命令，以提供必要的權限`kubernetes-dashboard`，然後重新啟動儀表板：

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>啟動儀表板時使用 kubeadm 啟動 Kubernetes 叢集

如需詳細指示如何部署和設定您的 Kubernetes 叢集中的儀表板，請參閱[Kubernetes 文件](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)。 若要啟動 Kubernetes 儀表板，執行此命令：

```bash
kubectl proxy
```

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 的巨量資料叢集](big-data-cluster-overview.md)。