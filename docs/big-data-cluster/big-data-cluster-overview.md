---
title: 什麼是 big data 叢集？
titleSuffix: SQL Server big data clusters
description: 瞭解在 Kubernetes 上執行的 SQL Server 2019 big data 叢集 (預覽), 並提供關聯式和 HDFS 資料的相應放大選項。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0beb4ea57ba6c2591e5b2c06a7775fc2d7e8b26c
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419502"
---
# <a name="what-are-sql-server-big-data-clusters"></a>什麼是 SQL Server 巨量資料叢集？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

從開始[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)], SQL Server big data 叢集可讓您部署在 Kubernetes 上執行之 SQL Server、Spark 和 HDFS 容器的可擴充叢集。 這些元件會並存執行, 讓您可以讀取、寫入和處理來自 Transact-sql 或 Spark 的大型資料, 讓您輕鬆地結合和分析具有大量海量資料的高價值關聯式資料。

如需最新版本的新功能和已知問題的詳細資訊, 請參閱[版本](release-notes-big-data-cluster.md)資訊。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>案例

SQL Server big data 叢集可讓您彈性地與您的 big 資料互動。 您可以查詢外部資料源、在 SQL Server 管理的 HDFS 中儲存海量資料, 或透過叢集查詢來自多個外部資料源的資料。 然後, 您可以使用 AI、機器學習和其他分析工作的資料。 下列各節提供有關這些案例的詳細資訊。

### <a name="data-virtualization"></a>資料虛擬化

藉由利用[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), SQL Server big data 叢集可以查詢外部資料源, 而不需要移動或複製資料。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]為數據源引進新的連接器。

![資料虛擬化](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data lake

SQL Server big data 叢集包含可擴充的 HDFS*存放集區*。 這可以用來儲存海量資料, 可能會從多個外部來源內嵌。 一旦海量資料儲存在 big data 叢集中的 HDFS 之後, 您就可以分析並查詢資料, 並將其與關聯式資料結合。

![Data lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>向外延展資料超市

SQL Server big data 叢集提供向外延展計算和儲存體, 以改善分析任何資料的效能。 來自各種來源的資料可以內嵌並散佈于*資料集*區節點, 做為進一步分析的快取。

![資料超市](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>整合式 AI 和 Machine Learning

SQL Server big data 叢集會針對儲存在 HDFS 存放集區和資料集區中的資料, 啟用 AI 和機器學習工作。 您可以在 SQL Server 中使用 Spark 和內建 AI 工具, 使用 R、Python、Scala 或 JAVA。

![AI 和 ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>管理與監控

管理和監視是透過命令列工具、Api、入口網站和動態管理檢視的組合來提供。

您可以使用 Azure Data Studio 在 big Data 叢集上執行各種工作。 這是由新的**SQL Server 2019 延伸模組 (預覽)** 啟用。 此延伸模組提供:

- 常見管理工作的內建程式碼片段。
- 能夠流覽 HDFS、上傳檔案、預覽檔案, 以及建立目錄。
- 能夠建立、開啟及執行與 Jupyter 相容的筆記本。
- [資料虛擬化] [wizard] 可簡化外部資料源的建立。

## <a id="architecture"></a>結構

SQL Server big data 叢集是由[Kubernetes](https://kubernetes.io/docs/concepts/)協調的 Linux 容器叢集。

### <a name="kubernetes-concepts"></a>Kubernetes 概念

Kubernetes 是一個開放原始碼容器協調器, 可以根據需求調整容器部署。 下表定義一些重要的 Kubernetes 術語:

|||
|:--|:--|
| **Cluster** | Kubernetes 叢集是一組電腦, 稱為節點。 一個節點控制叢集, 並指定主要節點;其餘節點是背景工作節點。 Kubernetes master 負責在背景工作角色和監視叢集的健康情況間散發工作。 |
| **節點** | 節點會執行容器化應用程式。 它可以是實體電腦或虛擬機器。 Kubernetes 叢集可包含混合的實體機器和虛擬機器節點。 |
| **Pod** | Pod 是 Kubernetes 的不可部分完成部署單位。 Pod 是執行應用程式所需的一或多個容器 (和相關聯的資源) 的邏輯群組。 每個 pod 都會在一個節點上執行;節點可以執行一或多個 pod。 Kubernetes 主機會自動將 pod 指派給叢集中的節點。 |
| &nbsp; ||

在 SQL Server big data 叢集中, Kubernetes 會負責 SQL Server big data 叢集的狀態;Kubernetes 會建立和設定叢集節點、將 pod 指派給節點, 以及監視叢集的健全狀況。

### <a name="big-data-clusters-architecture"></a>Big data 叢集架構

下圖顯示 SQL Server 的 big data 叢集元件。

![架構概觀](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a>控制器

控制器會提供叢集的管理和安全性。 其中包含 cntrol 服務、設定存放區, 以及其他叢集層級的服務, 例如 Kibana、Grafana 和彈性搜尋。

### <a id="computeplane"></a>計算集區

計算集區會提供計算資源給叢集。 其中包含執行 Linux 上的 SQL Server pod 的節點。 計算集區中的 pod 會分割成*SQL 計算實例*, 以進行特定的處理工作。 

### <a id="dataplane"></a>資料集區

資料集區用於資料持續性和快取。 資料集區是由執行 Linux 上的 SQL Server 的一或多個 pod 所組成。 它是用來內嵌 SQL 查詢或 Spark 作業的資料。 SQL Server big data cluster 資料超市會保存在資料集區中。 

### <a name="storage-pool"></a>存放集區

存放集區包含由 Linux 上的 SQL Server、Spark 和 HDFS 組成的存放集區 pod。 SQL Server big data 叢集中的所有存放裝置節點都是 HDFS 叢集的成員。

> [!TIP]
> 如需深入瞭解 big data 叢集架構和安裝, 請參閱[研討會:Microsoft SQL Server big data 叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)。

## <a name="next-steps"></a>後續步驟

SQL Server big data 叢集第一次是以有限的公開預覽版本, 透過 SQL Server 2019 早期採用計畫取得。 若要要求存取權, 請[在這裡](https://aka.ms/eapsignup)註冊, 並指定您想要試用 big data 叢集的相關資訊。 Microsoft 會將所有要求分級, 並儘快回應。
