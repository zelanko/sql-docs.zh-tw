---
title: 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安裝 azdata 工具，以安裝及管理巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 40338c4083241fedd113bca3a1beb839dbdd3fca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75721692"
---
# <a name="install-azdata"></a>安裝 `azdata`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

`azdata` 是以 Python 撰寫的命令列公用程式，可透過 REST API 啟動及管理巨量資料叢集。 

## <a name="find-latest-version"></a>尋找最新版本

您一律可以在 [https://aka.ms/azdata](https://aka.ms/azdata) 找到最新版本的檔案清單。

若要找出已安裝的版本，並查看是否需要更新，請執行 `azdata --version`。

## <a name="os-specific-instructions"></a>OS 特定指示

* [在 Windows 上安裝](deploy-install-azdata-installer.md)
* [在 macOS 上安裝](deploy-install-azdata-macos.md)
* 在 Linux 或[適用於 Linux 的 Windows 子系統 (WSL)](/windows/wsl/about/) 上安裝
   * [在 Debian 或 Ubuntu 上使用 apt 安裝](deploy-install-azdata-linux-package.md)
   * [在 RHEL 或 CentOS 上使用 yum 安裝](deploy-install-azdata-yum.md)
   * [在 openSUSE 或 SLE 上使用 Zypper 安裝](deploy-install-azdata-zypper.md)
   * [從指令碼安裝](deploy-install-azdata-pip.md)

[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
