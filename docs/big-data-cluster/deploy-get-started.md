---
title: 開始使用
titleSuffix: SQL Server 2019 big data clusters
description: 了解的步驟和部署 SQL Server 2019 巨量資料叢集 （預覽） 的資源。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 05ba81fd45bc44db9c23530fb594c5d2e291e05d
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2019
ms.locfileid: "58567644"
---
# <a name="get-started-with-sql-server-2019-big-data-clusters"></a>開始使用 SQL Server 2019 巨量資料叢集

這篇文章提供如何部署概觀[SQL Server 2019 巨量資料叢集 （預覽）](big-data-cluster-overview.md)。 它是要您熟悉的概念，並了解其他部署文件這一節中提供的架構。 在用戶端和伺服器平台選擇特定的部署步驟有所不同。

## <a id="tools"></a> 用戶端工具

巨量資料叢集需要一組特定的用戶端工具。 在 kubernetes 中部署巨量資料叢集之前，您應該安裝下列工具：

| 工具 | 描述 |
|---|---|
| **mssqlctl** | 部署和管理巨量資料叢集。 |
| **kubectl** | 建立及管理基礎的 Kubernetes 叢集。 |
| **Azure Data Studio** | 使用巨量資料叢集的圖形化介面。 |
| **SQL Server 2019 延伸模組** | Azure Data Studio 擴充功能可讓巨量資料叢集功能。 |

針對不同的案例需要其他工具。 每個發行項應該說明必要的工具，來執行特定工作。 如需工具和安裝連結的完整清單，請參閱 <<c0> [ 安裝 SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

為一系列的相互關聯的容器中管理部署巨量資料叢集[Kubernetes](https://kubernetes.io/docs/home)。 您可以裝載 Kubernetes 的各種不同的方式。 即使您已經有現有的 Kubernetes 環境，您應該檢閱巨量資料叢集的相關的需求。

- **Azure Kubernetes Service (AKS)**:AKS 可讓您部署在 Azure 中受管理的 Kubernetes 叢集。 您只能管理和維護代理程式節點。 有了 AKS，您不需要佈建您自己的硬體叢集。 它也很容易使用巨量資料叢集[部署指令碼](quickstart-big-data-cluster-deploy.md)建立 AKS 叢集，並部署在一個步驟中的巨量資料叢集。 如需使用 AKS 使用巨量資料叢集的詳細資訊，請參閱[適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署中設定 Azure Kubernetes Service](deploy-on-aks.md)。

- **多部機器**:您也可以部署到多部 Linux 電腦，這可能是實體伺服器或虛擬機器的 Kubernetes。 [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)工具可用來建立 Kubernetes 叢集。 這個方法適用於您已經有您想要用於您的巨量資料叢集的現有基礎結構。 如需使用詳細資訊**kubeadm**部署巨量資料叢集，請參閱[適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署的多部電腦上設定的 Kubernetes](deploy-with-kubeadm.md)。

- **Minikube**:Minikube 可讓您在單一伺服器上本機執行 Kubernetes。 如果您正在嘗試巨量資料叢集，或需要使用在測試或開發的案例中，它就會是不錯的選項。 如需使用 Minikube 的詳細資訊，請參閱 < [Minikube 文件](https://kubernetes.io/docs/setup/minikube/)。 巨量資料叢集搭配使用 Minikube 的特定需求，請參閱 <<c0> [ 設定適用於 SQL Server 2019 巨量資料叢集部署的 minikube](deploy-on-minikube.md)。

## <a name="deployment-scripts"></a>部署指令碼

部署指令碼可協助部署 Kubernetes 和巨量資料叢集以單一步驟。 它們也經常會提供必要的環境變數的預設值。 如需的巨量資料叢集在 Azure Kubernetes Service (AKS) 的部署指令碼範例，請參閱 <<c0> [ 部署與部署指令碼 (AKS) 叢集的巨量資料的 SQL Server 2019](quickstart-big-data-cluster-deploy.md)。

您可以自訂任何部署指令碼，藉由建立您自己的版本，以不同的方式設定巨量資料叢集環境變數。

## <a name="deploy-a-big-data-cluster"></a>部署巨量資料叢集

若要使用單一指令碼將 Kubernetes 和巨量資料叢集部署到 AKS，請參閱下列範例：

- [部署與部署指令碼 (AKS) 的 SQL Server 2019 巨量資料叢集](quickstart-big-data-cluster-deploy.md)

如需部署使用 AKS，kubeadm，MiniKube 的巨量資料叢集的詳細的部署指導方針，請參閱下列文章：

- [如何部署 SQL Server 在 Kubernetes 上的巨量資料叢集](deployment-guidance.md)

## <a name="next-steps"></a>後續步驟

您已成功部署巨量資料叢集之後,[連線到叢集](connect-to-big-data-cluster.md)，並考慮[載入範例資料](tutorial-load-sample-data.md)搭配幾個逐步解說。