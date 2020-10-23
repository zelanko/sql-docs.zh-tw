---
title: 使用 azdata 與 Grafana 儀表板監視應用程式
titleSuffix: SQL Server Big Data Clusters
description: 在 SQL Server 2019 巨量資料叢集上使用 azdata 與 Grafana 監視應用程式。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 08/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1391b88f2762293aa4eebf255682605bf5b6b1e0
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257278"
---
# <a name="monitor-applications-with-azdata-and-grafana-dashboard"></a>使用 azdata 與 Grafana 儀表板監視應用程式

Grafana 是最佳雲端原生虛擬化工具之一，可用來為 Kubernetes 中執行的應用程式提供各種監視計量。  

此文章描述如何監視 SQL Server 巨量資料叢集內的應用程式。

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 巨量資料叢集](deployment-guidance.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]](../azdata/install/deploy-install-azdata.md)

## <a name="capabilities"></a>功能

在 SQL Server 2019 中，您可以建立、刪除、描述、初始化、列出執行及更新您的應用程式。 下表描述您可以搭配 **azdata** 使用的應用程式部署命令。

|Command |描述 |
|:---|:---|
|`azdata bdc endpoint list` | 列出巨量資料叢集的端點。 |


您可以使用下列範例列出 **Grafana 儀表板**的端點：

```bash
azdata bdc endpoint list --endpoint-name metricsui 
```

輸出將會為您提供端點，您可以使用您的叢集使用者名稱與密碼登入。 

![Grafana 儀表板](media/big-data-cluster-monitor-apps/grafana-dashboard-endpoint.png)


當您開啟儀表板時，請移至 [主機應用程式計量] **** ，您可以在其中取得有關應用程式的其他見解並繼續進行追蹤。  

![主機應用程式計量](media/big-data-cluster-monitor-apps/host-apps-metrics.png)


若要深入了解應用程式的單一 Pod (在部分情況下，您的應用程式有多個複本)，請移至 [主機 Pod 計量] ****  ，並選擇 Pod，您會看到下列計量：  

![主機 Pod 計量](media/big-data-cluster-monitor-apps/host-pods-metrics.png) 


## <a name="next-steps"></a>後續步驟

您可以在[應用程式部署範例](https://aka.ms/sql-app-deploy)中查看其他範例。

如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。