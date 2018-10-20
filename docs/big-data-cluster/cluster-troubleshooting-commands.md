---
title: 使用 kubectl 來監視 SQL Server 的巨量資料叢集 |Microsoft Docs
description: 這篇文章會提供有用的 kubectl 命令，來監視和疑難排解 SQL Server 2019 巨量資料叢集 （預覽）。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/15/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: a47726e86bd1f10cda4db55bec6eac995344da38
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356590"
---
# <a name="kubectl-commands-for-monitoring-and-troubleshooting-sql-server-big-data-clusters"></a>監視和疑難排解 SQL Server 的巨量資料叢集的 Kubectl 命令

本文會說明數個實用的 Kubernetes 命令可用來監視和疑難排解 SQL Server 2019 巨量資料叢集 （預覽）。 本文章涵蓋一般工作，例如將檔案複製或從執行的其中一個 SQL Server 的巨量資料叢集服務的容器。 它也會顯示如何檢視 pod 或其他位於巨量資料叢集的 Kubernetes 成品的詳細資料。

## <a name="kubectl-command-examples"></a>Kubectl 命令範例

執行下列**kubectl** （cmd 或 PS） 的 Windows 或 Linux (bash) 用戶端電腦上的命令。 它們需要先前叢集和叢集內容，對執行中的驗證。 例如，先前建立的 AKS 叢集您可以執行`az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>`下載 Kubernetes 叢集組態檔，並設定叢集內容。

## <a name="get-status-of-pods"></a>取得 pod 的狀態

您可以使用`kubectl get pods`命令，以取得所有命名空間或巨量資料叢集命名空間的叢集中的 pod 的狀態。 下列各節顯示兩者的範例。

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>在 Kubernetes 叢集中的所有 pod 的顯示狀態

執行下列命令來取得所有 pod 和其狀態，包括屬於命名空間的 pod 巨量資料叢集的 pod 建立於該 SQL Server:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>在 SQL Server 的巨量資料叢集中顯示的所有 pod 的狀態

使用`-n`參數來指定特定的命名空間。 請注意，在叢集啟動程序時建立的新命名空間中建立巨量資料叢集的 pod 的 SQL Server 基礎中指定的叢集名稱`mssqlctl create cluster <cluster_name>`命令。

```bash
kubectl get pods -n <namespace_name>
```

比方說，下列命令會顯示狀態的 pod 中名為巨量資料叢集`big_data_cluster`:

```bash
kubectl get pods -n big_data_cluster
```

## <a name="get-pod-details"></a>取得 pod 的詳細資料

執行下列命令來取得 json 格式輸出中的特定 pod 的詳細的描述。 它包含詳細資料，例如目前執行中 pod，以及用來啟動容器的映像的容器放置 pod，Kubernetes 節點。 也會顯示其他詳細資訊，例如標籤、 狀態，並保存 pod 相關聯的磁碟區宣告。

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

下列範例顯示的詳細資料`mssql-data-pool-master-0`中名為巨量資料叢集的 pod `big_data_cluster`:

```bash
kubectl describe pod  mssql-data-pool-master-0 -n big_data_cluster
```

## <a name="get-status-of-services"></a>取得服務狀態

執行下列命令來取得巨量資料叢集服務的詳細資料。 這些詳細資料包括其類型，並使用個別的服務和連接埠相關聯的 Ip。 請注意，在中指定的叢集名稱為基礎的叢集啟動程序時建立的新命名空間中建立 SQL Server 的巨量資料叢集服務`mssqlctl create cluster <cluster_name>`命令。

```bash
kubectl get svc -n <namespace_name>
```

下列範例會顯示服務的狀態中名為巨量資料叢集`big_data_cluster`:

```bash
kubectl get svc -n big_data_cluster
```

## <a name="get-service-details"></a>取得服務詳細資料

執行此命令來取得 json 格式輸出中的一項服務的詳細的描述。 它會包含詳細資料例如標籤、 選取器中，IP、 外部 IP （如果服務的負載平衡器的型別）、 連接埠等。
```
kubectl describe pod  <pod_name> -n <namespace_name>
```

範例
```
kubectl describe pod  mssql-data-pool-master-0 -n big_data_cluster
```

## <a name="run-commands-in-a-container"></a>在容器中執行的命令

如果現有的工具或基礎結構不會讓您執行特定工作，而不實際是在容器的內容，您可以登入容器使用`kubectl exec`命令。 例如，您可能需要檢查是否有特定的檔案，或您可能需要重新啟動服務容器中。 

若要使用`kubectl exec`命令，請使用下列語法：

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

下列兩節會提供特定容器中執行命令的兩個範例。

### <a id="restartsql"></a> 登入特定的容器，然後重新啟動 SQL Server 處理序

下列範例示範如何重新啟動 SQL Server 處理序`mssql-server`容器中的`mssql-master-pool-0`pod:

```bash
kubectl exec -it mssql-master-pool-0  -c mssql-server -n big_data_cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> 登入特定的容器，並在容器中重新啟動服務
 
下列範例示範如何重新啟動所有服務，受**監督**: 

```bash
kubectl exec -it mssql-master-pool-0  -c mssql-server -n big_data_cluster -- /bin/bash 
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
kubectl cp mssql-master-pool-0:/var/opt/mssql/log -c mssql-server -n big_data_cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> 將檔案複製到容器

下列範例複製**將 AdventureWorks2016CTP3.bak**至 SQL Server 的主要執行個體容器從本機電腦檔案 (`mssql-server`) 中`mssql-master-pool-0`pod。 將檔案複製到`/tmp`目錄中的容器。 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n big_data_cluster
```

## <a id="forcedelete"></a> 強制刪除 pod
 
它不被建議強制刪除 pod。 測試可用性、 復原或資料持續性，您可以刪除 pod 來模擬 pod 失敗但`kubectl delete pods`命令。

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

下列範例會刪除儲存體集區的 pod， `mssql-storage-pool-default-0`:

```bash
kubectl delete pods mssql-storage-pool-default-0 -n big_data_cluster --grace-period=0 --force
```

## <a id="getip"></a> 取得 pod IP
 
如需疑難排解用途，您可能需要取得 pod 目前執行所在節點的 IP。 若要取得的 IP 位址，請使用`kubectl get pods`命令搭配下列語法：

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

下列範例會取得節點的 IP 位址， `mssql-master-pool-0` pod 上執行：

```bash
kubectl get pods mssql-master-pool-0 -o yaml -n big_data_cluster | grep hostIP
```

## <a name="start-the-kubernetes-dashboard"></a>啟動 Kubernetes 儀表板

您可以啟動 Kubernetes 儀表板，如需有關叢集的詳細資訊。 下列各節說明如何在 AKS 的 Kubernetes 和 Kubernetes 啟動使用 kubeadm 啟動儀表板。
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>當叢集正在執行 AKS 中啟動儀表板

若要啟動 Kubernetes 儀表板執行：
 
```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> 如果您收到下列錯誤：*無法接聽連接埠 8001： 所有接聽程式無法建立因下列錯誤： 無法建立接聽程式： 錯誤接聽 tcp4 127.0.0.1:8001: > 繫結： 只有一個使用的每個通訊端位址 （通訊協定/網路通常允許位址/連接埠）。無法建立接聽程式： 錯誤接聽 tcp6： 位址 [[:: 1]]: 8001： 遺漏中的連接埠 > 解決錯誤： 無法在任何要求的連接埠上接聽: [{8001 9090}]*，請確定您沒有啟動儀表板已經從另一個視窗。

當您在 在您的瀏覽器上啟動 儀表板時，您可能會因為在 AKS 叢集中，預設為啟用的 RBAC 權限警告而儀表板所使用的服務帳戶沒有足夠的權限存取的所有資源 (例如*禁止 pod： 使用者 」 系統： serviceaccount:kube-系統： kubernetes-儀表板上 「 無法列出 「 預設 」 的命名空間中的 pod*)。 執行下列命令，以提供必要的權限`kubernetes-dashboard`，然後重新啟動儀表板：

```
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>啟動儀表板時使用 kubeadm 啟動 Kubernetes 叢集

如需詳細指示如何部署和設定您的 Kubernetes 叢集中的儀表板，請參閱[Kubernetes 文件](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)。 若要啟動 Kubernetes 儀表板，執行此命令：

```
kubectl proxy
```

## <a name="next-steps"></a>後續步驟

監視和疑難排解也就 SQL Server 特定的巨量資料叢集，請參閱[叢集管理網站](cluster-admin-portal.md)。