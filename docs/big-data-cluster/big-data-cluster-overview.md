---
title: 什麼是 Big Data 叢集？
titleSuffix: SQL Server Big Data Clusters
description: 瞭解在 Kubernetes 上執行的(預覽),並提供關聯式和HDFS資料的相應放大選項。[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c75005c35e743a87ff742352946c4fdde5fcf0b8
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153655"
---
# <a name="what-are-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>什麼是[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

從開始[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] , 可讓您部署在 Kubernetes 上執行之 SQL Server、Spark 和 HDFS 容器的可擴充叢集。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 這些元件會並存執行，可供您讀取、寫入和處理來自 Transact-SQL 或 Spark 的巨量資料，讓您輕鬆地結合與分析具有大量巨量資料的高價值關聯式資料。

如需最新版本新功能和已知問題的詳細資訊，請參閱[版本資訊](release-notes-big-data-cluster.md)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>案例

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]提供與您的 big 資料互動的彈性。 您可以查詢外部資料源、在 SQL Server 管理的 HDFS 中儲存巨量資料，或透過叢集查詢來自多個外部資料源的資料。 接著您可以使用 AI、機器學習服務和其他分析工作的資料。 下列各節提供這些案例的詳細資訊。

### <a name="data-virtualization"></a>資料虛擬化

利用[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md), 可以[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]查詢外部資料源, 而不需要移動或複製資料。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 為資料源引進新的連接器。

![資料虛擬化](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

SQL Server 巨量資料叢集包含可調整的 HDFS「存放集區」。 這可以用來儲存可能內嵌自多個外部來源的巨量資料。 當巨量資料儲存在巨量資料叢集中的 HDFS 之後，您就可以分析及查詢資料，並將其與關聯式資料結合。

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>向外延展資料超市

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]提供相應放大計算和儲存體, 以改善分析任何資料的效能。 來自各種來源的資料可以作為快取以在「資料集區」節點之間內嵌並散發來供進一步分析。

![資料超市](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>整合的 AI 與機器學習

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]在儲存于 HDFS 儲存集區和資料集區中的資料上啟用 AI 和機器學習工作。 您可以利用 R、Python、Scala 或 JAVA，在 SQL Server 中使用 Spark 和內建 AI 工具。

![AI 和 ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>管理與監控

管理和監視是透過命令列工具、API、入口網站和動態管理檢視的組合來提供。

您可以使用 Azure Data Studio 在巨量資料叢集上執行各種工作。 這是由新的 **SQL Server 2019 延伸模組 (預覽)** 所提供。 此延伸模組提供：

- 常見管理工作的內建程式碼片段。
- 能夠瀏覽 HDFS、上傳檔案、預覽檔案及建立目錄。
- 能夠建立、開啟並執行與 Jupyter 相容的筆記本。
- 資料虛擬化精靈可簡化外部資料源的建立。

## <a id="architecture"></a> 架構

SQL Server 巨量資料叢集是由 [Kubernetes](https://kubernetes.io/docs/concepts/) 協調的 Linux 容器叢集。

### <a name="kubernetes-concepts"></a>Kubernetes 概念

Kubernetes 是開放原始碼容器協調器，可根據需求調整容器部署。 下表定義一些重要的 Kubernetes 術語：

|||
|:--|:--|
| **Cluster** | Kubernetes 叢集是稱為節點的一組電腦。 其中一個節點會控制叢集，並受指定為主要節點，而其餘節點為背景工作節點。 Kubernetes 主要節點負責在背景工作節點間散發工作，並監視叢集的健康狀態。 |
| **節點** | 節點會執行容器化應用程式。 節點可以是實體電腦或虛擬機器。 Kubernetes 叢集可包含實體機器和虛擬機器節點的混合。 |
| **Pod** | Pod 是 Kubernetes 的不可部分完成部署單位。 Pod 是執行應用程式所需一或多個容器以及相關聯資源的邏輯群組。 每個 Pod 都會在一個節點上執行，每個節點可以執行一或多個 Pod。 Kubernetes 主機會自動將 Pod 指派給叢集中的節點。 |
| &nbsp; ||

在[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]中, Kubernetes 會負責的狀態[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)];Kubernetes 會建立和設定叢集節點、將 pod 指派給節點, 以及監視叢集的健全狀況。

### <a name="big-data-clusters-architecture"></a>巨量資料叢集架構

下圖顯示 SQL Server 的巨量資料叢集元件。

![架構概觀](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> 控制器

控制器會提供叢集的管理和安全性。 其中包含 cntrol 服務、設定存放區以及其他叢集層級的服務 (例如 Kibana、Grafana 和彈性搜尋)。

### <a id="computeplane"></a> 計算集區

計算集區會將計算資源提供給叢集。 其中包含在 Linux Pod 上執行 SQL Server 的節點。 計算集區中的 Pod 會分割成 *SQL 計算執行個體*，以進行特定的處理工作。 

### <a id="dataplane"></a> 資料集區

資料集區用於資料持續性和快取。 資料集區由在 Linux 上執行 SQL Server 的一或多個 Pod 所組成。 用於從 SQL 查詢或 Spark 作業中內嵌資料。 SQL Server 巨量資料叢集資料超市會保存在資料集區中。 

### <a name="storage-pool"></a>存放集區

存放集區包含由 Linux 上的 SQL Server、Spark 和 HDFS 組成的存放集區 Pod。 SQL Server 巨量資料叢集中的所有存放裝置節點都是 HDFS 叢集成員。

> [!TIP]
> 如需深入了解叢集架構和安裝，請參閱[工作坊：Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)。

## <a name="next-steps"></a>後續步驟

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]第一次是透過 SQL Server 2019 早期採用方案, 以有限的公開預覽形式提供。 若要要求存取權，請在[這裡](https://aka.ms/eapsignup)註冊，並指出您希望試用巨量資料叢集的原因。 Microsoft 會將所有要求分級並盡快回應。
