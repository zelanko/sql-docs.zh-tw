---
title: 開始使用
titleSuffix: SQL Server Big Data Clusters
description: 了解部署 SQL Server 巨量資料叢集的步驟和資源。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4caaacd2d71d00d874a793129eef2f4144f03190
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784294"
---
# <a name="get-started-with-big-data-clusters-2019-deployment"></a>開始使用 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 部署

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文提供如何部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的概觀。 本文將說明概念，並提供可供了解部署案例的架構。 您特定的部署步驟會依您針對用戶端和伺服器所選擇的平台而有所不同。 如需 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的簡介，請參閱 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)

如需了解其他 SQL Server 部署案例，請參閱：

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Docker 容器](../linux/sql-server-linux-configure-docker.md)

## <a name="quick-introduction"></a>快速簡介 

觀看這段 9 分鐘的影片，以取得如何部署巨量資料叢集的概觀：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Big-Data-Clusters-deployment-overview/player?WT.mc_id=dataexposed-c9-niner]


> [!TIP]
> 若要快速部署 Kubernetes 與巨量資料叢集環境，以協助您提升其功能，請使用[指令碼區段](#scripts)中指出的任一項範例指令碼。 在部署之後若要管理叢集，可使用下一區段中的[用戶端工具](#tools)。


## <a name="client-tools"></a><a id="tools"></a> 用戶端工具

巨量資料叢集需要一組特定的用戶端工具。 將巨量資料叢集部署至 Kubernetes 之前，您應該先安裝部署所需的工具。 針對不同案例，還會需要特定工具。 每篇文章都應該會說明執行某個特定工作的必要工具。 如需工具和安裝連結的完整清單，請參閱[安裝 SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)。

## <a name="kubernetes"></a>Kubernetes

巨量資料叢集會被部署為一系列相互關聯的容器，這些容器是在 [Kubernetes](https://kubernetes.io/docs/home) \(英文\) 中加以管理。 您可以透過數種不同方式裝載 Kubernetes。 即使您已經具有現有的 Kubernetes 環境，您還是應該檢閱適用於巨量資料叢集的相關需求。

- **Azure Kubernetes Service (AKS)** ：AKS 可讓您在 Azure 中部署受控 Kubernetes 叢集。 您只需要管理及維護代理程式節點。 透過 AKS，您不需要自行為叢集佈建硬體。 它也可讓您輕鬆使用 [python 指令碼](quickstart-big-data-cluster-deploy.md)或[部署筆記本](notebooks-deploy.md)，以單一步驟建立 AKS 叢集並部署巨量資料叢集。 如需如何為巨量資料叢集部署設定 AKS 的詳細資訊，請參閱[設定適用於 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 部署的 Azure Kubernetes Service](deploy-on-aks.md)。

- **Azure Red Hat OpenShift (ARO)** ：ARO 允許您在 Azure 中部署受控的 Red Hat OpenShift 叢集。 您只需要管理及維護代理程式節點。 透過 ARO，您不需要為叢集佈建自己的硬體。 您也可以輕鬆使用 [Python 指令碼](quickstart-big-data-cluster-deploy-aro.md)，一個步驟即可建立 ARO 叢集並部署巨量資料叢集。 SQL Server 2019 CU5 中引入此部署模型。 

- **多部電腦**：您也可以將 Kubernetes 部署至多部 Linux 電腦，其可為實體伺服器或虛擬機器。 [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) \(英文\) 工具可以用來建立 Kubernetes 叢集。 您可以使用 [bash 指令碼](deployment-script-single-node-kubeadm.md)來將此類型的部署自動化。 此方法很適合用於您已經具有要用於巨量資料叢集之現有基礎結構的情況。 如需如何在巨量資料叢集中使用 **kubeadm**部署的詳細資訊，請參閱[為 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 部署在多部電腦上設定 Kubernetes](deploy-with-kubeadm.md)。

- **Red Hat OpenShift**：部署至自己的 Red Hat OpenShift 叢集。 如需相關資訊，請參閱[在 OpenShift 內部部署與 Azure Red Hat OpenShift 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-openshift.md)。 SQL Server 2019 CU5 中引入此部署模型。

## <a name="deploy-a-big-data-cluster"></a>部署巨量資料叢集

在設定 Kubernetes 之後，您會使用 `azdata bdc create` 命令來部署巨量資料叢集。 部署時，您可以採取數種不同的方式。

- 如果您是要部署至開發-測試環境，您可以選擇使用由 **azdata** 所提供的其中一個[預設設定](deployment-guidance.md#deploy)。

- 若要自訂部署，您可以建立並使用自己的[部署設定檔](deployment-guidance.md#configfile)。

- 若要進行完全自動安裝，您可以透過環境變數傳遞所有其他設定。 如需詳細資訊，請參閱[自動部署](deployment-guidance.md#unattended)。


## <a name="deployment-scripts"></a><a id="scripts"></a> 部署指令碼

部署指令碼可以協助以單一步驟同時部署 Kubernetes 和巨量資料叢集。 它們通常也會提供適用於巨量資料叢集設定的預設值。 您可以透過自行建立會以不同方式設定巨量資料叢集部署的版本，來自訂任何部署指令碼。

目前提供下列部署指令碼：

- [Python 指令碼 -- 在 Azure Kubernetes Service (AKS) 上部署巨量資料叢集](quickstart-big-data-cluster-deploy.md)
- [Bash 指令碼 -- 將巨量資料叢集部署至單一節點 kubeadm 叢集](deployment-script-single-node-kubeadm.md)

## <a name="deployment-notebooks"></a>部署筆記本

您也可以透過執行 Azure Data Studio 筆記本來部署巨量資料叢集。 如需如何在 AKS 上使用筆記本進行部署的詳細資訊，請參閱下列文章：

- [使用 Azure Data Studio 筆記本部署 SQL Server 巨量資料叢集](notebooks-deploy.md)。

## <a name="next-steps"></a>後續步驟

在您成功部署巨量資料叢集之後，請[連線至叢集](connect-to-big-data-cluster.md)並考慮[載入範例資料](tutorial-load-sample-data.md)來搭配數個逐步解說使用。
