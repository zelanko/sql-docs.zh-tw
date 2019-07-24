---
title: 開始使用
titleSuffix: SQL Server big data clusters
description: 瞭解部署 SQL Server 2019 big data 叢集 (預覽) 的步驟和資源。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 41dd39c7aa613083f8ff47824ed6238b6f3c61b9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419431"
---
# <a name="get-started-with-sql-server-big-data-clusters"></a>開始使用 SQL Server big data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文概述如何部署[SQL Server 2019 big data cluster (預覽)](big-data-cluster-overview.md)。 它的目的是要引導您瞭解這些概念, 並提供可讓您瞭解本節中其他部署文章的架構。 您的特定部署步驟會根據您的用戶端和伺服器平臺選擇而有所不同。

## <a id="tools"></a>用戶端工具

Big data 叢集需要一組特定的用戶端工具。 將大型資料叢集部署至 Kubernetes 之前, 您應該安裝下列工具:

| 工具 | 描述 |
|---|---|
| **azdata** | 部署和管理大型資料叢集。 |
| **kubectl** | 建立和管理基礎 Kubernetes 叢集。 |
| **Azure Data Studio** | 用於使用 big data cluster 的圖形化介面。 |
| **SQL Server 2019 延伸模組** | 啟用 big Data cluster 功能的 Azure Data Studio 延伸模組。 |

不同的案例需要其他工具。 每篇文章都應該說明執行特定工作的必要工具。 如需工具和安裝連結的完整清單, 請參閱[安裝 SQL Server 2019 big data tools](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

Big data 叢集會部署為一系列的相互關聯容器, 並在[Kubernetes](https://kubernetes.io/docs/home)中進行管理。 您可以用各種方式裝載 Kubernetes。 即使您已經有現有的 Kubernetes 環境, 您還是應該查看 big data 叢集的相關需求。

- **Azure Kubernetes Service (AKS)** :AKS 可讓您在 Azure 中部署受控 Kubernetes 叢集。 您只會管理和維護代理程式節點。 有了 AKS, 您就不需要為叢集布建自己的硬體。 您也可以輕鬆地使用 big data cluster[部署腳本](quickstart-big-data-cluster-deploy.md)來建立 AKS 叢集, 並在一個步驟中部署 big data cluster。 如需有關使用 AKS 搭配 big data 叢集的詳細資訊, 請參閱[設定 SQL Server 2019 big data cluster (預覽) 部署的 Azure Kubernetes Service](deploy-on-aks.md)。

- **多部電腦**:您也可以將 Kubernetes 部署到多部 Linux 電腦, 也就是實體伺服器或虛擬機器。 [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)工具可以用來建立 Kubernetes 叢集。 如果您已經有想要用於 big data 叢集的現有基礎結構, 這個方法會很有作用。 如需有關使用**kubeadm**部署與大型資料叢集的詳細資訊, 請參閱[在多部電腦上設定 Kubernetes, 以進行 SQL Server 2019 big data cluster (預覽) 部署](deploy-with-kubeadm.md)。

- **Minikube**:Minikube 可讓您在單一伺服器上本機執行 Kubernetes。 如果您想要嘗試海量資料叢集, 或需要在測試或開發案例中使用它, 這是個不錯的選項。 如需有關使用 Minikube 的詳細資訊, 請參閱[Minikube 檔](https://kubernetes.io/docs/setup/minikube/)。 如需使用 Minikube 搭配 big data 叢集的特定需求, 請參閱[Configure Minikube for SQL Server 2019 big data cluster 部署](deploy-on-minikube.md)。

## <a name="deploy-a-big-data-cluster"></a>部署巨量資料叢集

設定 Kubernetes 之後, 您可以使用`azdata bdc create`命令來部署 big data cluster。 部署時, 您可以採用數種不同的方法。

- 如果您要部署至開發/測試環境, 您可以選擇使用**azdata**所提供的其中一個[預設](deployment-guidance.md#deploy)設定。

- 若要自訂您的部署, 您可以建立並使用您自己的[部署設定檔](deployment-guidance.md#configfile)。

- 如需完全自動安裝, 您可以在環境變數中傳遞所有其他設定。 如需詳細資訊, 請參閱自動[部署](deployment-guidance.md#unattended)。

## <a name="deployment-scripts"></a>部署指令碼

部署腳本可協助您在單一步驟中部署 Kubernetes 和 big data 叢集。 它們通常也會提供 big data cluster 設定的預設值。 如需 Azure Kubernetes Service (AKS) 上的大型資料叢集部署腳本範例, 請參閱下列文章:

[使用部署腳本部署 SQL Server 2019 big data 叢集 (AKS)](quickstart-big-data-cluster-deploy.md)。

您可以建立自己的版本, 以不同方式設定 big data 叢集環境變數, 以自訂任何部署腳本。

[使用 Azure Data Studio 筆記本部署 SQL Server 2019 big data](deploy-notebooks.md)叢集。

## <a name="next-steps"></a>後續步驟

在您成功部署 big data 叢集之後, 請[連接到](connect-to-big-data-cluster.md)叢集, 並考慮[載入範例資料](tutorial-load-sample-data.md)以用於數個逐步解說。