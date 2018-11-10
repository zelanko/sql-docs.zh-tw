---
title: 監視使用叢集系統管理入口網站的 SQL Server 巨量資料叢集 （預覽） |Microsoft Docs
description: 了解如何使用叢集系統管理入口網站來監視 SQL Server 2019 巨量資料叢集 （預覽）。
author: yualan
ms.author: alayu
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: eaff715d1fe29e1484dec7bde24de6bb16449458
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221464"
---
# <a name="introduction-to-the-cluster-administration-portal"></a>叢集系統管理入口網站簡介

如果您想要監視或疑難排解 SQL Server 2019 巨量資料叢集 （預覽），請使用 叢集系統管理入口網站。

叢集系統管理入口網站可讓您：
- 快速檢視執行的 pod 和任何的問題數目
- 監視部署狀態
- 檢視可用的服務端點
- 檢視控制器，以及 SQL Server 的主要執行個體
- 向下鑽研 pod，包括存取 Grafana 儀表板和 Kibana 的記錄檔的詳細資訊

## <a name="access-the-cluster-administration-portal"></a>存取叢集的系統管理入口網站

請遵循[快速入門，來部署巨量資料叢集](quickstart-big-data-cluster-deploy.md)直到到達**叢集管理網站**一節。 一旦您有使用 mssqlctl 執行巨量資料叢集，請遵循下列指示：

當控制器 pod 執行時，您可以使用叢集系統管理入口網站來監視部署。 您可以存取入口網站中使用的外部 IP 位址和連接埠號碼`service-proxy-lb`(例如： **https://\<ip 位址\>: 30777**)。 認證為存取管理員入口網站的值`CONTROLLER_USERNAME`和`CONTROLLER_PASSWORD`上面提供的環境變數。

> [!NOTE]
> 對於 CTP 2.1 中，沒有安全性警告時存取網頁，因為它使用自動產生的 SSL 憑證。

## <a name="overview"></a>總覽

![概觀](./media/cluster-admin-portal/portal-overview.png)

當您第一次輸入入口網站時，您可以快速檢視執行的 pod 數目：
- 控制器
- 主要執行個體
- 計算集區
- 存放集區
- 資料集區

如果有任何問題，您可以開啟已知問題的連結。 您可以使用左側的導覽窗格中，移至特定集區中，如果發生問題。

## <a name="deployment"></a>部署

![部署](./media/cluster-admin-portal/portal-deployment.png)

若要監視您的部署，請按一下左側的 [部署] 索引標籤。 您所見的樹狀檢視您的部署，以及是否在部署中有任何問題。

## <a name="service-endpoints"></a>服務端點

![端點](./media/cluster-admin-portal/portal-endpoints.png)

您可以在左側的導覽窗格中的 端點 索引標籤上的 檢視可用的服務端點。

這包括 Spark 端點，Grafana 儀表板連結和 Kibana 記錄。

## <a name="controller"></a>控制器

![控制站](./media/cluster-admin-portal/portal-controller.png)

控制器會顯示控制站相關的所有 pod。 您可以深入了解控制器[這裡。](concept-controller.md)

若要了解更多其他有關每個 pod，您可以按一下**計量**檢視 Grafana 儀表板的資料行。

若要深入了解問題的 pod 的記錄檔，您可以按一下**記錄檔**資料行。

## <a name="master-instance"></a>主要執行個體

![端點](./media/cluster-admin-portal/portal-master.png)

主要執行個體顯示與 SQL Server 的主要執行個體相關的所有 pod。 您可以深入了解 SQL Server 的主要執行個體[這裡。](concept-master-instance.md)

若要了解更多其他有關每個 pod，您可以按一下**計量**檢視 Grafana 儀表板的資料行。

若要深入了解問題的 pod 的記錄檔，您可以按一下**記錄檔**資料行。

## <a name="pool-and-pod-pages"></a>集區和 Pod 頁面

![集區](./media/cluster-admin-portal/portal-data-pool.png)

在每個集區] 頁面上 （計算、 儲存和資料），您可以向下鑽研至每個 pod 網頁上的 [**預設**

![Pod](./media/cluster-admin-portal/portal-data-default-pool.png)

這會顯示向下鑽研路徑頂端階層連結列。

若要了解更多其他有關每個 pod，您可以按一下**計量**檢視 Grafana 儀表板的資料行。

若要深入了解問題的 pod 的記錄檔，您可以按一下**記錄檔**資料行。

若要深入了解每個集區：
- [計算集區](concept-compute-pool.md)
- [存放集區](concept-storage-pool.md)
- [資料集區](concept-data-pool.md)

## <a name="about-page"></a>關於頁面

![關於](./media/cluster-admin-portal/portal-about.png)

這裡您可以檢視資訊，例如不同的版本號碼、 容器和連結的叢集，文件的相關。

## <a name="next-steps"></a>後續步驟

除了 「 叢集系統管理入口網站中，您也可以執行數個實用的 Kubernetes 命令探索叢集健康情況與狀態。 如需詳細資訊，請參閱 <<c0> [ 進行監視和疑難排解 SQL Server 的巨量資料叢集的 Kubectl 命令](cluster-troubleshooting-commands.md)。

若要深入了解 SQL Server 2019 巨量資料叢集，請參閱[什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
