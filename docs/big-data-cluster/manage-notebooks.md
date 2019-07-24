---
title: 使用 Azure Data Studio 筆記本管理 SQL Server big data 叢集
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用 Azure Data Studio 的筆記本來管理大型資料叢集, 並對其進行疑難排解。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8d87b09878539cccd40191d870bf97487579dca2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426398"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>使用 Azure Data Studio 筆記本來管理 SQL Server 的海量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]提供包含部署筆記本之 Azure Data Studio 的延伸模組。 部署筆記本包含檔和程式碼, 您可以在 Azure Data Studio 中用來管理 SQL Server 的海量資料叢集。

[筆記本](notebooks-guidance.md)原本實作為開放原始碼專案, 已實作為[Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)。 您可以在文字資料格中使用 markdown 做為文字, 並在其中一個可用的核心中撰寫程式碼。

您可以使用筆記本來部署的[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]大型資料叢集。

## <a name="prerequisites"></a>必要條件

必須具備下列必要條件, 才能啟動筆記本:

* 最新版的[Azure Data Studio 內部人員組建](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Azure Data Studio 中安裝的擴充功能

除了以上, 部署 SQL Server 2019 big data 叢集也需要:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)
