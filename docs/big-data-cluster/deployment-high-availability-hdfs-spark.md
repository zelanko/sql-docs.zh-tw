---
title: 部署高可用性 HDFS 或 Spark
titleSuffix: SQL Server Big Data Clusters
description: 了解如何部署高可用性 SQL Server 巨量資料叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 25a6b733eed0611b43fb1f17ad0fe8a0cc1d690a
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75720815"
---
# <a name="deploy-hdfs-name-node-and-shared-spark-services-in-a-highly-available-configuration"></a>在高可用性設定中部署 HDFS 名稱節點和共用 Spark 服務

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

除了使用可用性群組在高可用性設定中部署 SQL Server 主要執行個體以外，您還可以在巨量資料叢集中部署其他任務關鍵性服務，以確保有更高的可靠性。 您可以設定 `HDFS name node` 及為分組到 `sparkhead` 下的共用 Spark 服務設定一個額外複本。 在此情況下，也會在巨量資料叢集中部署 `Zookeeper`，作為下列服務的叢集協調器和中繼資料存放區： 

- HDFS 名稱節點
- Livy 和 Yarn Resource Manager。 

Spark 記錄、作業記錄和 Hive 中繼資料服務都是無狀態服務。 Zookeeper 與確保這些元件的服務健全狀態無關。 

針對這些服務部署多個複本可增強可用複本之間工作負載的延展性、可靠性和負載平衡。

> [!NOTE]
> 下列服務會部署為 `sparkhead` Pod 中的容器： 
> - Livy
> - Yarn Resource Manager
> - Spark 記錄
> - 作業記錄
> - Hive 中繼資料服務  
>

下圖顯示 SQL Server 巨量資料叢集中的 Spark HA 部署：

:::image type="content" source="media/deployment-high-availability-hdfs-spark/spark-ha.png" alt-text="spark-ha-bdc":::

下圖顯示 SQL Server 巨量資料叢集中的 HDFS HA 部署：

:::image type="content" source="media/deployment-high-availability-hdfs-spark/hdfs-ha.png" alt-text="hdfs-ha-bdc":::

## <a name="deploy"></a>部署

如果為名稱節點或 sparkhead 設定兩個複本，則您也必須為 Zookeeper 資源設定三個複本。 在 HDFS 名稱節點的高可用性設定中，會由兩個 Pod 裝載兩個複本。 這兩個 Pod 分別為 `nmnode-0` 和 `nmnode-1`。 此設定為主動-被動。 一次只能有一個主動的名稱節點。 另一個節點會處於待命狀態，並在發生容錯移轉事件之後變成主動。 

您可以使用 `aks-dev-test-ha` 或 `kubeadm-prod` 內建組態設定檔來開始自訂您的巨量資料叢集部署。 這些設定檔包含為資源設定額外高可用性時所需的設定。 例如，以下是 `bdc.json` 設定檔中與部署高可用性 HDFS 名稱節點、Zookeeper 和共用 Spark 資源 (`sparkhead`) 相關的區段。  

```json
{
  ...
    "nmnode-0": {
        "spec": {
            "replicas": 2
        }
    },
    "sparkhead": {
        "spec": {
            "replicas": 2
        }
    },
    "zookeeper": {
        "spec": {
            "replicas": 3
        }
    },
  ...
}
```

基於最佳做法，您也必須在生產環境部署中，將 HDFS 區塊複寫設定為 3。 `aks-dev-test-ha` 和 `kubeadm-prod` 設定檔中已指定此設定。 請參閱 `bdc.json` 設定檔中的以下區段：

```json
{
  ...
  "hdfs": {
      "resources": [
          "nmnode-0",
          "zookeeper",
          "storage-0",
          "sparkhead"
      ],
      "settings": {
          "hdfs-site.dfs.replication": "3"
      }
  },
  ...
}
```

## <a name="known-limitations"></a>已知限制

在 SQL Server 巨量資料叢集中設定 Hadoop 服務高可用性時的已知問題和限制包括：

- 所有設定都必須在巨量資料叢集部署時指定。 在 SQL Server 2019 CU1 版本中，您無法在部署後啟用高可用性設定。

## <a name="next-steps"></a>後續步驟

- 如需在巨量資料叢集部署中使用設定檔的詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md#configfile)。
- 如需巨量資料叢集中 SQL Server 主要高可用性選項的詳細資訊，請參閱[部署高可用性 SQL Server 主要執行個體](deployment-high-availability.md)主題。
