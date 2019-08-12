---
title: 使用 Azure Data Studio 筆記本部署 SQL Server 巨量資料叢集
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用來自 Azure Data Studio 的筆記本來部署巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fb1da50fb84cbfd44aeab50a00be1c8433b3041e
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892451"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本部署 SQL Server 巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供包含部署筆記本的 Azure Data Studio 擴充功能。 部署筆記本所包含的文件和程式碼，可供您用來在 Azure Data Studio 中建立 SQL Server 巨量資料叢集。

[筆記本](notebooks-guidance.md)原本是實作為開放原始碼專案，而現已實作至 [Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download) \(部分機器翻譯\)。 您現在可以將 Markdown 用於文字儲存格中的文字，也可以使用其中一個可用的核心，在程式碼儲存格中撰寫程式碼。

您可以使用筆記本來部署 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的巨量資料叢集。

## <a name="prerequisites"></a>先決條件

必須滿足下列先決條件才能啟動筆記本：

* 已安裝最新版本的[Azure Data Studio 內部人員組建](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* 在 Azure Data Studio 中安裝 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 延伸模組

除了上述，部署 SQL Server 2019 巨量資料叢集也需要：

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>啟動筆記本

1. 啟動 Azure Data Studio 內部人員。

1. 在 [Connections] \(連線\) 索引標籤上，按一下 [...] 並選取 [Deploy SQL Server big data cluster] \(部署 SQL Server 巨量資料叢集\)。

   ![AI 和 ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. 在 [Options] \(選項\) 下的 [Deployment Target] \(部署目標\) 中，選取 [New Azure Kubernetes Cluster] \(新增 Azure Kubernetes 叢集\) 或 [Existing Azure Kubernetes Service cluster] \(現有的 Azure Kubernetes Service 叢集\)。

1. 按一下 [**選取**] 按鈕。

1. 此動作會啟動一個對話方塊來收集使用者輸入、提供必要的資訊, 以及檢查預設值。

1. 按一下 [**開啟筆記本**] 按鈕。
此動作會啟動適當的筆記本。 若要完成部署，請遵循筆記本中的指示在現有的或新的 Azure Kubernetes Service 叢集上部署 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 巨量資料叢集。

## <a name="next-steps"></a>後續步驟

如需部署的詳細資訊，請參閱 [SQL Server 巨量資料叢集的部署指導方針](deployment-guidance.md)。
