---
title: 使用 Azure Data Studio 筆記本部署 SQL Server big data 叢集
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用 Azure Data Studio 的筆記本來部署 big Data 叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f12a4f06ceb1c3a48b2b2fc661c59594e6d6cce3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426418"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本部署 SQL Server big data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]提供包含部署筆記本之 Azure Data Studio 的延伸模組。 部署筆記本包含檔和程式碼, 您可以在 Azure Data Studio 中用來建立 SQL Server big Data 叢集。 

[筆記本](notebooks-guidance.md)原本實作為開放原始碼專案, 已實作為[Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)。 您可以在文字資料格中使用 markdown 做為文字, 並在其中一個可用的核心中撰寫程式碼。

您可以使用筆記本來部署的[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]大型資料叢集。

## <a name="prerequisites"></a>先決條件
必須具備下列必要條件, 才能啟動筆記本:

* 已安裝最新版的[Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Azure Data Studio 中安裝的擴充功能

除了以上, 部署 SQL Server 2019 big data 叢集也需要:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>啟動筆記本

1. 安裝並啟動[Azure Data Studio 的內部人員組建](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)。
1.  在 [**連接**] 索引標籤上, 按一下 [ **...** ], 然後選取 [**部署 SQL Server big data cluster**...]。

   ![AI 和 ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. 從**部署目標**的 [**選項**] 底下, 選取 [新增] [ **Azure Kubernetes**叢集] 或 [**現有 Azure Kubernetes Service**叢集]。
1. 選取 [**開啟筆記本**]。

此動作會啟動適當的筆記本。 若要完成部署, 請遵循筆記本中的指示, [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]在現有或新的 Azure Kubernetes Service 叢集上部署 big data cluster。
