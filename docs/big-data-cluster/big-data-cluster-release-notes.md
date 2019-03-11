---
title: 版本資訊
titleSuffix: SQL Server 2019 big data clusters
description: 本文說明 SQL Server 2019 巨量資料叢集 （預覽） 的已知的問題與最新的更新。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 9dfb6706f27006ccb876615316533bc8e15b3101
ms.sourcegitcommit: 3c4bb35163286da70c2d669a3f84fb6a8145022c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2019
ms.locfileid: "57683628"
---
# <a name="release-notes-for-sql-server-2019-big-data-clusters"></a>SQL Server 2019 巨量資料叢集的版本資訊

這篇文章會提供最新版的 SQL Server 的巨量資料叢集的最新的更新和已知的問題。 下表可連結您的版本 > 一節涵蓋在本文中。

| 版本 | Date |
|---|---|
| [CTP 2.3](#ctp23) | 2019 年 2 月 |
| [CTP 2.2](#ctp22) | 2018 年 12 月 |
| [CTP 2.1](#ctp21) | 2018 年 11 月 |
| [CTP 2.0](#ctp20) | 2018 年 10 月 |

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp23"></a> CTP 2.3 (第 2019 年 2 月)

下列各節說明的新功能與 SQL Server 2019 CTP 2.3 中的巨量資料叢集的已知的問題。

### <a name="whats-in-the-ctp-23-release"></a>什麼是 CTP 2.3 版本？

- [將 SQL Server 巨量資料叢集上在 IntelliJ 中的 Spark 作業提交](spark-submit-job-intellij-tool-plugin.md)。
- [適用於應用程式部署和叢集管理的常見 CLI](big-data-cluster-create-apps.md)。
- [SQL Server 的巨量資料叢集來部署應用程式的 VS Code 延伸模組](app-deployment-extension.md)。
- [若要變更**mssqlctl**工具命令使用方式](#mssqlctlctp23)。
- [在 SQL Server 2019 巨量資料叢集使用 Sparklyr](sparklyr-from-RStudio.md)。
- 使用巨量資料叢集裝載外部的 HDFS 相容儲存體[HDFS 分層](hdfs-tiering.md)。
- 新的統一的連接體驗，如[SQL Server 的主要執行個體和 HDFS/Spark 閘道](connect-to-big-data-cluster.md)。
- 刪除與叢集**mssqlctl 叢集刪除**現在刪除僅物件命名空間中的巨量資料叢集的一部分，但保留命名空間。 先前，此命令會刪除整個命名空間。
- 端點名稱已變更和彙總在此版本中：

   | 先前的端點 | 新的端點 |
   |---|---|
   | **service-security-lb**<br/>**service-security-nodeport** | **endpoint-security** |
   | **service-proxy-lb**<br/>**service-proxy-nodeport** | **endpoint-service-proxy** |
   | **service-mssql-controller-lb**<br/>**service-mssql-controller-nodeport** | **endpoint-controller** |

### <a name="known-issues"></a>已知問題

下列各節提供 SQL Server CTP 2.3 中的巨量資料叢集已知的問題。

#### <a name="deployment"></a>部署

- 不支援從舊版升級的巨量資料的資料叢集。

   > [!IMPORTANT]
   > 您必須備份您的資料，然後再刪除現有的巨量資料叢集 (使用舊版**mssqlctl**) 才能部署最新版本。 如需詳細資訊，請參閱 <<c0> [ 升級到新版](deployment-guidance.md#upgrade)。

- **ACCEPT_EULA**環境變數必須是"yes"或 [是] 以接受使用者授權合約。 舊版允許"y"和"Y"，但是這些不會再接受，且會導致部署失敗。

- **CLUSTER_PLATFORM**環境變數沒有預設值在舊版本中所顯示的一樣。

- 在部署之後在 AKS 上，您可能會看到部署的下列兩個警告事件。 這兩個事件的已知問題，但它們不會防止您成功部署在 AKS 上的巨量資料叢集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果巨量資料叢集部署失敗，不會移除相關聯的命名空間。 這可能會導致失去關聯的命名空間，在叢集上。 因應措施是手動刪除命名空間，才能部署具有相同名稱的叢集。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果您要部署多部電腦上的 Kubernetes 使用 kubeadm，叢集系統管理入口網站不會正確顯示連線至巨量資料叢集所需的端點。 如果您遇到這個問題，使用下列因應措施若要探索的服務端點 IP 位址：

- 如果您從連接在叢集內，查詢服務 IP 端點，您想要連線到 Kubernetes。 例如，下列**kubectl**命令會顯示 SQL Server 的主要執行個體的 IP 位址：

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果您從外部連線的叢集，請使用下列步驟來連接：

   1. 取得執行 SQL Server 的主要執行個體的節點的 IP 位址： `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 連接到 SQL Server 使用此 IP 位址的主要執行個體。

   1. 查詢**cluster_endpoint_table**其他外部端點的 master 資料庫中。

      如果失敗連接逾時，就可以在對應的節點進行防火牆處理。 在此情況下，您必須連絡您的 Kubernetes 叢集系統管理員，並要求為對外公開的節點 IP。 這可能是任何節點。 您接著可以使用該 IP 和對應的連接埠連接到叢集中執行的各種服務。 比方說，系統管理員可以執行以尋找此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="mssqlctlctp23"></a> mssqlctl

- **Mssqlctl**工具變更至名詞動詞命令的順序排序動詞-名詞 」 命令。 例如，`mssqlctl create cluster`現在`mssqlctl cluster create`。

- `--name`參數現在是在建立叢集時所需`mssqlctl cluster create`。

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- 如需升級至最新版的巨量資料叢集的重要資訊和**mssqlctl**，請參閱[升級至新版](deployment-guidance.md#upgrade)。

#### <a name="external-tables"></a>外部資料表

- 可以建立具有不支援的資料行類型為資料表的資料集區外部資料表。 如果您查詢外部資料表時，您收到訊息如下所示：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢儲存體集區外部資料表時，您可能會發生錯誤，如果在相同的時間基礎檔案複製到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果您要建立外部資料表以使用字元資料類型的 Oracle，Azure Data Studio virtualization 精靈會解譯為 VARCHAR 這些資料行中的外部資料表定義。 這會導致外部資料表 DDL 失敗。 請修改使用 NVARCHAR2 類型，或以手動方式建立 EXTERNAL TABLE 陳述式，而不是使用此精靈指定 NVARCHAR 的 Oracle 結構描述。

#### <a name="application-deployment"></a>應用程式部署

- 在呼叫 R、 Python 或 MLeap 應用程式從支援的 RESTful API 時，呼叫會逾時在 5 分鐘內。

#### <a name="spark-and-notebooks"></a>Spark 和 notebook

- POD IP 位址可能變更 Kubernetes 環境中，Pod 重新啟動時。 在案例中，重新啟動主要 pod，Spark 工作階段可能會失敗並`NoRoteToHostException`。 這因為不使用新的 IP 取得重新整理的 JVM 快取的位址。

- 如果您在 Windows 上有已安裝的 Jupyter 和個別的 Python，可能會失敗 Spark notebook。 若要解決此問題，請升級為最新版本的 Jupyter。

- 在筆記本中，如果您按一下**新增文字**命令時，文字資料格會新增 [預覽] 模式，而不是編輯模式。 您可以按一下 [預覽] 圖示，切換至編輯模式和編輯儲存格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下檔案，以進行預覽，HDFS 中，您可能會看到下列錯誤：

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可預覽檔案大於 30 MB 的 Azure Data Studio。

- 不支援對 hdfs-site.xml 變更的 HDFS 組態變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 屬於環境的且可探索 （例如在線傾印檔案）。 您必須在部署之後，重設 SA_PASSWORD 主要執行個體上。 這不是 bug，但安全性步驟。 如需有關如何變更 SA_PASSWORD 的 Linux 容器的詳細資訊，請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄檔可能包含適用於巨量資料叢集部署的 SA 密碼。

## <a id="ctp22"></a> CTP 2.2 (年 12 月 2018)

下列各節說明的新功能和巨量資料中的叢集 SQL Server 2019 CTP 2.2 的已知的問題。

### <a name="whats-in-the-ctp-22-release"></a>什麼是 CTP 2.2 版本？

- 使用叢集系統管理員入口網站存取`/portal`(**https://\<ip 位址\>: 30777/入口網站**)。
- 從主要集區服務名稱變更`service-master-pool-lb`並`service-master-pool-nodeport`至`endpoint-master-pool`。
- 新版**mssqlctl**和更新映像。
- 其他錯誤修正和改進功能。

### <a name="known-issues"></a>已知問題

下列各節提供 SQL Server CTP 2.2 中的巨量資料叢集已知的問題。

#### <a name="deployment"></a>部署

- 不支援從舊版升級的巨量資料的資料叢集。 您必須備份並刪除任何現有的巨量資料叢集，才能部署最新版本。 如需詳細資訊，請參閱 <<c0> [ 升級到新版](deployment-guidance.md#upgrade)。

- 在部署之後在 AKS 上，您可能會看到部署的下列兩個警告事件。 這兩個事件的已知問題，但它們不會防止您成功部署在 AKS 上的巨量資料叢集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果巨量資料叢集部署失敗，不會移除相關聯的命名空間。 這可能會導致失去關聯的命名空間，在叢集上。 因應措施是手動刪除命名空間，才能部署具有相同名稱的叢集。

#### <a name="cluster-administration-portal"></a>叢集系統管理入口網站

叢集系統管理入口網站不會顯示 SQL Server 的主要執行個體的端點。 若要尋找主要執行個體的 IP 位址和連接埠，使用下列項目**kubectl**命令：

```
kubectl get svc endpoint-master-pool -n <your-cluster-name>
```

#### <a name="external-tables"></a>外部資料表

- 可以建立具有不支援的資料行類型為資料表的資料集區外部資料表。 如果您查詢外部資料表時，您收到訊息如下所示：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢儲存體集區外部資料表時，您可能會發生錯誤，如果在相同的時間基礎檔案複製到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和 notebook

- POD IP 位址可能變更 Kubernetes 環境中，Pod 重新啟動時。 在案例中，重新啟動主要 pod，Spark 工作階段可能會失敗並`NoRoteToHostException`。 這因為不使用新的 IP 取得重新整理的 JVM 快取的位址。

- 如果您在 Windows 上有已安裝的 Jupyter 和個別的 Python，可能會失敗 Spark notebook。 若要解決此問題，請升級為最新版本的 Jupyter。

- 在筆記本中，如果您按一下**新增文字**命令時，文字資料格會新增 [預覽] 模式，而不是編輯模式。 您可以按一下 [預覽] 圖示，切換至編輯模式和編輯儲存格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下檔案，以進行預覽，HDFS 中，您可能會看到下列錯誤：

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可預覽檔案大於 30 MB 的 Azure Data Studio。

- 不支援對 hdfs-site.xml 變更的 HDFS 組態變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 屬於環境的且可探索 （例如在線傾印檔案）。 您必須在部署之後，重設 SA_PASSWORD 主要執行個體上。 這不是 bug，但安全性步驟。 如需有關如何變更 SA_PASSWORD 的 Linux 容器的詳細資訊，請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄檔可能包含適用於巨量資料叢集部署的 SA 密碼。

## <a id="ctp21"></a> CTP 2.1 (11 月 2018)

下列各節說明的新功能與 SQL Server 2019 CTP 2.1 中的巨量資料叢集的已知的問題。

### <a name="whats-in-the-ctp-21-release"></a>什麼是 CTP 2.1 版本？

- [將 Python 和 R 的應用程式部署](big-data-cluster-create-apps.md)巨量資料叢集中。
- 新版**mssqlctl**和更新映像。 
- 其他錯誤修正和改進功能。

### <a name="known-issues"></a>已知問題

下列各節提供 SQL Server CTP 2.1 中的巨量資料叢集已知的問題。

#### <a name="deployment"></a>部署

- 不支援從舊版升級的巨量資料的資料叢集。 您必須備份並刪除任何現有的巨量資料叢集，才能部署最新版本。 如需詳細資訊，請參閱 <<c0> [ 升級到新版](deployment-guidance.md#upgrade)。

- 在部署之後在 AKS 上，您可能會看到部署的下列兩個警告事件。 這兩個事件的已知問題，但它們不會防止您成功部署在 AKS 上的巨量資料叢集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果巨量資料叢集部署失敗，不會移除相關聯的命名空間。 這可能會導致失去關聯的命名空間，在叢集上。 因應措施是手動刪除命名空間，才能部署具有相同名稱的叢集。

#### <a name="admin-portal"></a>系統管理員入口網站

- 當您[建立應用程式使用 msqlctl ctp 命令](big-data-cluster-create-apps.md)並將其部署巨量資料叢集，叢集系統管理員入口網站顯示 pod 已部署應用程式為 「 不明 」 的 Admin 部分的 [控制器] 區段中的 SQL Server 上。

#### <a name="external-tables"></a>外部資料表

- 可以建立具有不支援的資料行類型為資料表的資料集區外部資料表。 如果您查詢外部資料表時，您收到訊息如下所示：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢儲存體集區外部資料表時，您可能會發生錯誤，如果在相同的時間基礎檔案複製到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和 notebook

- POD IP 位址可能變更 Kubernetes 環境中，Pod 重新啟動時。 在案例中，重新啟動主要 pod，Spark 工作階段可能會失敗並`NoRoteToHostException`。 這因為不使用新的 IP 取得重新整理的 JVM 快取的位址。

- 如果您在 Windows 上有已安裝的 Jupyter 和個別的 Python，可能會失敗 Spark notebook。 若要解決此問題，請升級為最新版本的 Jupyter。

- 在筆記本中，如果您按一下**新增文字**命令時，文字資料格會新增 [預覽] 模式，而不是編輯模式。 您可以按一下 [預覽] 圖示，切換至編輯模式和編輯儲存格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下檔案，以進行預覽，HDFS 中，您可能會看到下列錯誤：

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可預覽檔案大於 30 MB 的 Azure Data Studio。

- 不支援對 hdfs-site.xml 變更的 HDFS 組態變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 屬於環境的且可探索 （例如在線傾印檔案）。 您必須在部署之後，重設 SA_PASSWORD 主要執行個體上。 這不是 bug，但安全性步驟。 如需有關如何變更 SA_PASSWORD 的 Linux 容器的詳細資訊，請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄檔可能包含適用於巨量資料叢集部署的 SA 密碼。

## <a id="ctp20"></a> CTP 2.0 (第 2018 年 10 月)

下列各節說明的新功能與 SQL Server 2019 CTP 2.0 中的巨量資料叢集的已知的問題。

### <a name="whats-in-the-ctp-20-release"></a>什麼是 CTP 2.0 版中？

- 簡單的部署經驗，使用 mssqlctl 管理工具
- 在 Azure 資料 Studio 中的原生的 notebook 體驗
- 查詢存放區執行個體的 SQL 伺服器透過 HDFS 檔案
- 透過 SQL Server、 Oracle、 MongoDB、 和 HDFS 的主要資料虛擬化
- SQL Server 和 Oracle 在 Azure 資料 Studio 中的資料虛擬化精靈
- 在主機上的 ML 服務
- 您可以使用監視和疑難排解的叢集系統管理入口網站
- 在 Azure 資料 Studio 中提交 Spark 作業 
- 在 叢集系統管理入口網站中的 Spark UI
- 磁碟區掛接到儲存體類別
- 透過從主要的資料集區的查詢
- 在 SSMS 中顯示分散式查詢的計的劃
- Pip 套件 mssqlctl 的管理工具
- 透過控制器服務的內建部署引擎

### <a name="known-issues"></a>已知問題

下列各節提供 SQL Server CTP 2.0 中的巨量資料叢集已知的問題。

#### <a name="deployment"></a>部署

- 如果您使用 Azure Kubernetes Service (AKS)，建議的 Kubernetes 版本是 1.10。 *，不支援調整磁碟大小。 您應該要確定您將會據以調整大小的儲存體在部署階段。 如需有關如何調整儲存體大小的詳細資訊，請參閱 <<c0> [ 資料持續性](concept-data-persistence.md)文章。 針對部署在 Vm 上的 Kubernetes，建議的版本是 1.11。

- 在部署之後在 AKS 上，您可能會看到部署的下列兩個警告事件。 這兩個事件的已知問題，但它們不會防止您成功部署在 AKS 上的巨量資料叢集。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果巨量資料叢集部署失敗，不會移除相關聯的命名空間。 這可能會導致失去關聯的命名空間，在叢集上。 因應措施是手動刪除命名空間，才能部署具有相同名稱的叢集。

#### <a name="external-tables"></a>外部資料表

- 可以建立具有不支援的資料行類型為資料表的資料集區外部資料表。 如果您查詢外部資料表時，您收到訊息如下所示：

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢儲存體集區外部資料表時，您可能會發生錯誤，如果在相同的時間基礎檔案複製到 HDFS。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和 notebook

- POD IP 位址可能變更 Kubernetes 環境中，Pod 重新啟動時。 在案例中，重新啟動主要 pod，Spark 工作階段可能會失敗並`NoRoteToHostException`。 這因為不使用新的 IP 取得重新整理的 JVM 快取的位址。

- 如果您在 Windows 上有已安裝的 Jupyter 和個別的 Python，可能會失敗 Spark notebook。 若要解決此問題，請升級為最新版本的 Jupyter。

- 在筆記本中，如果您按一下**新增文字**命令時，文字資料格會新增 [預覽] 模式，而不是編輯模式。 您可以按一下 [預覽] 圖示，切換至編輯模式和編輯儲存格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下檔案，以進行預覽，HDFS 中，您可能會看到下列錯誤：

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可預覽檔案大於 30 MB 的 Azure Data Studio。

- 不支援對 hdfs-site.xml 變更的 HDFS 組態變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 屬於環境的且可探索 （例如在線傾印檔案）。 您必須在部署之後，重設 SA_PASSWORD 主要執行個體上。 這不是 bug，但安全性步驟。 如需有關如何變更 SA_PASSWORD 的 Linux 容器的詳細資訊，請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄檔可能包含適用於巨量資料叢集部署的 SA 密碼。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 的巨量資料叢集的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
