---
title: 機器學習服務 (Python、R)
titleSuffix: SQL Server Big Data Clusters
description: 了解如何對安裝有機器學習服務的 SQL Server 巨量資料叢集主要執行個體，執行 Python 與 R 指令碼。
author: dphansen
ms.author: davidph
ms.date: 04/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
ms.openlocfilehash: d105db3da8a6732c2884af7e42a71441eef6f077
ms.sourcegitcommit: ed5f063d02a019becf866c4cb4900e5f39b8db18
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643333"
---
# <a name="run-python-and-r-scripts-with-machine-learning-services-on-sql-server-big-data-clusters"></a>對安裝有機器學習服務的 SQL Server 巨量資料叢集執行 Python 與 R 指令碼

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

您可以對安裝有[機器學習服務](../machine-learning/index.yml)的 [SQL Server 巨量資料叢集](big-data-cluster-overview.md)主要執行個體，執行 Python 與 R 指令碼。

> [!NOTE]
> 您也可以對 [SQL Server 語言延伸模組](../language-extensions/language-extensions-overview.md)的主要執行個體，執行 JAVA 程式碼。 執行下列步驟也能啟用語言延伸模組。

## <a name="enable-machine-learning-services"></a>啟用機器學習服務

根據預設，機器學習服務會安裝在巨量資料叢集上，而且不需要個別安裝。

若要啟用機器學習服務，請對主要執行個體上執行下列陳述式：

```sql
EXEC sp_configure 'external scripts enabled', 1
RECONFIGURE WITH OVERRIDE
GO
```

您現在已可對巨量資料叢集的主要執行個體執行 Python 與 R 指令碼。 請參閱[後續步驟](#next-steps)下的快速入門來執行第一個指令碼。

>[!NOTE]
>無法在可用性群組接聽程式連線上設定組態設定。 如果以高可用性部署巨量資料叢集，則會在每個複本上設定 `external scripts enabled`。 請參閱[在具有高可用性的叢集上啟用](#enable-on-cluster-with-high-availability)。

## <a name="enable-on-cluster-with-high-availability"></a>在具有高可用性的叢集上啟用

當[以高可用性部署 SQL Server 巨量資料叢集](deployment-high-availability.md)時，部署會建立主要執行個體的可用性群組。 若要啟用機器學習服務，請在可用性群組的每個執行個體上設定 `external scripts enabled`。 針對巨量資料叢集，則必須在 SQL Server 主要執行個體的每個複本上執行 `sp_configure`

下一節描述如何在每個執行個體上啟用外部指令碼。

### <a name="create-an-external-load-balancer-for-each-instance"></a>為每個執行個體建立外部負載平衡器

針對可用性群組上的每個複本建立負載平衡器，其可供連線到執行個體。 

`kubectl expose pod <pod-name> --port=<connection port number> --name=<load-balancer-name> --type=LoadBalancer -n <kubernetes namespace>`

本文中範例使用下列值：

- `<pod-name>`: `master-#`
- `<connection port number>`: `1533`
- `<load-balancer-name>`: `mymaster-#`
- `<kubernetes namespace>`: `mssql-cluster`

更新環境中的下列指令碼，然後執行命令：

```bash
kubectl expose pod master-0 --port=1533 --name=mymaster-0 --type=LoadBalancer -n mssql-cluster 
kubectl expose pod master-1 --port=1533 --name=mymaster-1 --type=LoadBalancer -n mssql-cluster
kubectl expose pod master-2 --port=1533 --name=mymaster-2 --type=LoadBalancer -n mssql-cluster 
```

`kubectl` 會傳回下列輸出。

```bash
service/mymaster-0 exposed
service/mymaster-1 exposed
service/mymaster-2 exposed
```

每個負載平衡器都是主要複本端點。

### <a name="enable-script-execution-on-each-replica"></a>在每個複本上啟用指令碼執行

1. 取得主要複本端點的 IP 位址。

   下列命令會傳回複本端點的外部 IP 位址。 

   `kubectl get services <load-balancer-name> -n <kubernetes namespace>`

   若要取得此案例中每個複本的外部 IP 位址，請執行下列命令：

   ```bash
   kubectl get services mymaster-0 -n mssql-cluster
   kubectl get services mymaster-1 -n mssql-cluster
   kubectl get services mymaster-2 -n mssql-cluster
   ```

   >[!NOTE]
   > 可能需要一些時間才能使用外部 IP 位址。 定期執行上述指令碼，直到每個端點傳回外部 IP 位址為止。

1. 連線到主要複本端點，並啟用指令碼執行。

    執行下列陳述式：

    ```sql
    EXEC sp_configure 'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    GO
    ```

   例如，您可使用 `sqlcmd` 來執行上述命令。 下列範例會連線到主要複本端點，並啟用指令碼執行。 以您環境中值來更新指令碼中的值。

   ```bash
   sqlcmd -S <IP address>,1533 -U <user name> -P <password> -Q "EXEC sp_configure 'external scripts enabled', 1; RECONFIGURE WITH OVERRIDE;"
   ```

   針對每個複本重複此步驟。

### <a name="demonstration"></a>示範

下圖示範這項程序。

[![](media/machine-learning-services/example-kube-enable-scripts.png "Demonstrate enable feature on Kubernetes")](media/machine-learning-services/example-kube-enable-scripts.png#lightbox)

您現在已可對巨量資料叢集的主要執行個體執行 Python 與 R 指令碼。 請參閱[後續步驟](#next-steps)下的快速入門來執行第一個指令碼。

### <a name="delete-the-master-replica-endpoints"></a>刪除主要複本端點

在 Kubernetes 叢集上，刪除每個複本的端點。 端點會在 Kubernetes 中公開為負載平衡服務。

下列命令可刪除負載平衡服務。

`kubectl delete svc <load-balancer-name> -n mssql-cluster`

針對本文中的範例，請執行下列命令。

```bash
kubectl delete svc mymaster-0 -n mssql-cluster
kubectl delete svc mymaster-1 -n mssql-cluster
kubectl delete svc mymaster-2 -n mssql-cluster
```

## <a name="next-steps"></a>後續步驟

+ [快速入門：使用 SQL Server 機器學習服務，建立及執行簡單的 Python 指令碼](../machine-learning/tutorials/quickstart-python-create-script.md)
+ [快速入門：使用 SQL Server 機器學習服務在 Python 中建立預測模型並計算其分數](../machine-learning/tutorials/quickstart-python-train-score-model.md)
+ [快速入門：使用 SQL Server 機器學習服務建立及執行簡單的 R 指令碼](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [快速入門：使用 SQL Server 機器學習服務在 R 中建立預測模型並計算其分數](../machine-learning/tutorials/quickstart-r-train-score-model.md)
