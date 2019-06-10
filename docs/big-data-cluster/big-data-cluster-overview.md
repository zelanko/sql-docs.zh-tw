---
title: 什麼是巨量資料叢集？
titleSuffix: SQL Server big data clusters
description: 深入了解 SQL Server 2019 巨量資料叢集 （預覽），以在 Kubernetes 上執行，並提供關聯式的向外延展選項和 HDFS 的資料。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/07/2018
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: fed82f9bda8f72d92157de726eb6ae3c6ed1c0c0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801887"
---
# <a name="what-are-sql-server-big-data-clusters"></a>什麼是 SQL Server 巨量資料叢集？

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

從開始[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]，SQL Server 的巨量資料叢集可讓您部署的 SQL Server、 Spark 和 HDFS 的容器，在 Kubernetes 上執行的可調整叢集。 這些元件會並存執行，可讓您讀取、 寫入，並處理從 TRANSACT-SQL 或 Spark 的巨量資料、 讓您輕鬆地結合和分析龐大的巨量資料與您寶貴的關聯式資料。

如需有關新功能和最新版本的已知的問題的詳細資訊，請參閱 <<c0> [ 版本資訊](release-notes-big-data-cluster.md)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="scenarios"></a>案例

SQL Server 巨量資料叢集提供您與您的巨量資料的互動的彈性。 您可以查詢外部資料來源、 巨量資料儲存在 HDFS 受 SQL Server 或從叢集內的多個外部資料來源的查詢資料。 然後您可以使用資料 AI、 機器學習服務，以及其他分析工作。 下列各節提供這些案例的詳細資訊。

### <a name="data-virtualization"></a>資料虛擬化

利用[SQL Server PolyBase](../relational-databases/polybase/polybase-guide.md)，SQL Server 的巨量資料叢集可以查詢外部資料來源，而不需要移動或複製資料。 [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] 資料來源中介紹新的連接器。

![資料虛擬化](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data lake

SQL Server 的巨量資料叢集包含可調整的 HDFS*存放集區*。 這可以用來儲存可能內嵌多個外部來源的巨量資料。 一旦巨量資料儲存在 HDFS 中，在巨量資料叢集，您可以分析和查詢資料並將它與您的關聯式資料結合。

![Data lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>向外延展資料超市

SQL Server 巨量資料叢集提供向外延展計算和儲存體，以改善的效能分析的任何資料。 從各種來源的資料可以擷取，並分散*資料集區*節點做為快取，供進一步分析。

![資料超市](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>整合的 AI 和機器學習服務

SQL Server 的巨量資料叢集啟用人工智慧和機器學習服務工作儲存在 HDFS 儲存體集區和資料集區中的資料。 您可以使用 R、 Python、 Scala 或 Java 的 SQL Server 中使用 Spark，以及內建的 AI 工具。

![AI 和 ML](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>管理與監控

透過命令列工具、 Api、 系統管理員入口網站和動態管理檢視的組合提供管理和監視。

[叢集系統管理員入口網站](cluster-admin-portal.md)是顯示在叢集中的 pod 的健全狀況與狀態的 web 介面。 它也會提供 log analytics 和監視儀表板的其他儀表板的連結。

您可以使用 Azure Data Studio 巨量資料叢集上執行的各種工作。 這會啟用新**SQL Server 2019 擴充功能 （預覽）** 。 此延伸模組提供：

- 適合一般管理工作的內建程式碼片段。
- 能夠瀏覽 HDFS 中，將檔案上傳、 預覽檔案，然後建立目錄。
- 若要建立，開啟，並執行相容性的 Jupyter notebook 的能力。
- 簡化的外部資料來源建立的虛擬化資料精靈。

## <a id="architecture"></a> 架構

SQL Server 的巨量資料叢集是由協調的 Linux 容器的叢集[Kubernetes](https://kubernetes.io/docs/concepts/)。

### <a name="kubernetes-concepts"></a>Kubernetes 概念

Kubernetes 是開放原始碼容器協調者，可以調整容器部署根據的需求。 下表定義了一些重要的 Kubernetes 術語：

|||
|:--|:--|
| **Cluster** | Kubernetes 叢集是一組機器，又稱為節點。 控制叢集一個節點，並指定在主要節點剩餘的節點是背景工作節點。 Kubernetes 主機負責散發工作的背景工作角色，以及監視叢集的健康情況。 |
| **節點** | 節點會執行容器化應用程式。 它可以是實體機器或虛擬機器。 Kubernetes 叢集可以包含實體機器和虛擬機器節點的混合。 |
| **Pod** | 在 pod 已 Kubernetes 的不可部分完成的部署單位。 在 pod 已一或多個容器的邏輯群組-和相關聯的資源所需執行的應用程式。 每個 pod 節點上執行;節點可以執行一或多個 pod。 Kubernetes 主機會將 pod 自動指派給叢集中的節點。 |
| &nbsp; ||

在 SQL Server 的巨量資料叢集，Kubernetes 會負責使用 SQL Server 的巨量資料叢集; 的狀態Kubernetes 會建置和設定叢集節點、 將 pod 指派給節點，和監視叢集的健全狀況。

### <a name="big-data-clusters-architecture"></a>巨量資料叢集架構

叢集中的節點可分為三個邏輯平面： 控制層、 計算平面和資料平面。 每個平面叢集中有不同的責任。 在 SQL Server 的巨量資料叢集中的每個 Kubernetes 節點的主機元件至少一個平面的 pod。

![架構概觀](media/big-data-cluster-overview/architecture-diagram-planes.png)

### <a id="controlplane"></a> 控制平面

控制平面會提供管理和安全性的叢集。 它包含 Kubernetes 母片*SQL Server 的主要執行個體*，和其他叢集層級服務，例如 Hive 中繼存放區和 Spark 驅動程式。

### <a id="computeplane"></a> 計算平面

計算平面會提供在叢集中的運算資源。 它包含在 Linux pod 上執行 SQL Server 的節點。 計算平面中的 pod 分為*計算集區*特定處理工作。 計算集區可做為[PolyBase](../relational-databases/polybase/polybase-guide.md)分散式查詢，透過不同的資料來源這類作為 HDFS、 Oracle、 MongoDB 或 Teradata 的向外延展群組。

### <a id="dataplane"></a> 資料平面

資料平面用於資料持續性和快取。 它包含 SQL 資料集區，以及儲存體集區。  SQL 資料集區是由一或多個 pod，在 Linux 上執行 SQL Server 所組成。 它用來擷取從 SQL 查詢或 Spark 作業的資料。 SQL Server 的巨量資料叢集的資料超市會保存在資料集區。 存放集區包含 Linux、 Spark 和 HDFS 上的 SQL Server 所組成的儲存體集區 pod。 在 SQL Server 的巨量資料叢集中的所有存放裝置節點是 HDFS 叢集的成員。

> [!TIP]
> 深入了解巨量資料叢集架構和安裝，請參閱[研討會：Microsoft SQL Server 的巨量資料叢集架構](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)。

## <a name="next-steps"></a>後續步驟

SQL Server 的巨量資料叢集可先透過 SQL Server 2019 Early Adoption Program 的有限公開預覽。 若要要求存取權，註冊[此處](https://aka.ms/eapsignup)，並指定您感興趣試用巨量資料叢集。 Microsoft 將分級所有要求，並儘速回應。
