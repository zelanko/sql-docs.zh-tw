---
title: 開始使用
titleSuffix: SQL Server big data clusters
description: 瞭解部署[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]的步驟和資源 (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 323394f9590551528ce9e9dfdf1fb97c7d1c2225
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653396"
---
# <a name="get-started-with-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>開始使用[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供如何部署[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)的總覽。 它的目的是要引導您理解其概念，並提供架構以了解本節中的其他部署文章。 您特定的部署步驟會依您針對用戶端和伺服器所選擇的平台而有所不同。

> [!TIP]
> 若要快速取得已部署 Kubernetes 和 big data 叢集的環境, 以協助您提升其功能, 請使用[腳本一節](#scripts)中所指的其中一個範例腳本。 部署之後, 若要管理叢集, 請使用下一節中的[用戶端工具](#tools)。

## <a id="tools"></a> 用戶端工具

巨量資料叢集需要一組特定的用戶端工具。 在您將巨量資料叢集部署至 Kubernetes 之前，應該先安裝下列工具：

| 工具 | 描述 |
|---|---|
| **azdata** | 部署及管理巨量資料叢集。 |
| **kubectl** | 建立及管理基礎 Kubernetes 叢集。 |
| **Azure Data Studio** | 用來使用巨量資料叢集的圖形化介面。 |
| **SQL Server 2019 擴充** | 能提供巨量資料叢集功能的 Azure Data Studio 擴充。 |

針對不同的案例，還會需要其他工具。 每篇文章都應該會說明執行某個特定工作的必要工具。 如需工具和安裝連結的完整清單，請參閱[安裝 SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

巨量資料叢集會被部署為一系列相互關聯的容器，這些容器是在 [Kubernetes](https://kubernetes.io/docs/home) \(英文\) 中加以管理。 您可以透過數種不同方式裝載 Kubernetes。 即使您已經具有現有的 Kubernetes 環境，您還是應該檢閱適用於巨量資料叢集的相關需求。

- **Azure Kubernetes Service (AKS)** ：AKS 可讓您在 Azure 中部署受控 Kubernetes 叢集。 您只需要管理及維護代理程式節點。 透過 AKS，您不需要自行為叢集佈建硬體。 它也可讓您輕鬆使用 [python 指令碼](quickstart-big-data-cluster-deploy.md)或[部署筆記本](deploy-notebooks.md)，以單一步驟建立 AKS 叢集並部署巨量資料叢集。 如需設定 AKS 以進行 big data 叢集部署的詳細資訊, 請參閱[設定[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]部署的 Azure Kubernetes Service](deploy-on-aks.md)。

- **多部電腦**：您也可以將 Kubernetes 部署至多部 Linux 電腦，其可為實體伺服器或虛擬機器。 [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) \(英文\) 工具可以用來建立 Kubernetes 叢集。 您可以使用 [bash 指令碼](deployment-script-single-node-kubeadm.md)來將此類型的部署自動化。 此方法很適合用於您已經具有要用於巨量資料叢集之現有基礎結構的情況。 如需有關搭配 big data 叢集使用**kubeadm**部署的詳細資訊, 請參閱[在多部[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]電腦上設定 Kubernetes 以進行部署](deploy-with-kubeadm.md)。

- **Minikube**：Minikube 可讓您在單一伺服器上於本機執行 Kubernetes。 它很適合在您只是要試用巨量資料叢集，或是需要將它用於測試或部署案例時使用。 如需使用 Minikube 的詳細資訊，請參閱 [Minikube 文件](https://kubernetes.io/docs/setup/minikube/) \(英文\)。 如需搭配巨量資料叢集使用 Minikube 的特定需求，請參閱[針對 SQL Server 2019 巨量資料叢集部署設定 Minikube](deploy-on-minikube.md)。

## <a name="deploy-a-big-data-cluster"></a>部署巨量資料叢集

在設定 Kubernetes 之後，您會使用 `azdata bdc create` 命令來部署巨量資料叢集。 部署時，您可以採取數種不同的方式。

- 如果您是要部署至開發-測試環境，您可以選擇使用由 **azdata** 所提供的其中一個[預設設定](deployment-guidance.md#deploy)。

- 若要自訂部署，您可以建立並使用自己的[部署設定檔](deployment-guidance.md#configfile)。

- 若要進行完全自動安裝，您可以透過環境變數傳遞所有其他設定。 如需詳細資訊，請參閱[自動部署](deployment-guidance.md#unattended)。


## <a id="scripts"></a>部署腳本

部署指令碼可以協助以單一步驟同時部署 Kubernetes 和巨量資料叢集。 它們通常也會提供適用於巨量資料叢集設定的預設值。 您可以透過自行建立會以不同方式設定巨量資料叢集部署的版本，來自訂任何部署指令碼。

目前提供下列部署指令碼：

- [Python 指令碼 -- 在 Azure Kubernetes Service (AKS) 上部署巨量資料叢集](quickstart-big-data-cluster-deploy.md)
- [Bash 指令碼 -- 將巨量資料叢集部署至單一節點 kubeadm 叢集](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>部署筆記本

您也可以透過執行 Azure Data Studio 筆記本來部署巨量資料叢集。 如需如何在 AKS 上使用筆記本進行部署的詳細資訊，請參閱下列文章：

- [使用 Azure Data Studio 筆記本部署 SQL Server 巨量資料叢集](deploy-notebooks.md)。

## <a name="next-steps"></a>後續步驟

在您成功部署巨量資料叢集之後，請[連線至叢集](connect-to-big-data-cluster.md)並考慮[載入範例資料](tutorial-load-sample-data.md)來搭配數個逐步解說使用。
