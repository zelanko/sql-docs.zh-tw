---
title: 使用安裝程式在 Linux 上安裝 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何使用安裝程式 (Linux) 安裝 azdata 工具，以安裝及管理 SQL Server 巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d8d4a34e89de7c136e1e80b43929531a2d10eba
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532066"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>安裝 `azdata`，以管理 Linux 上的 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在 Linux 上安裝適用於 SQL Server 2019 巨量資料叢集的 `azdata`。 您必須先使用 `pip` 安裝 `azdata`，才能開始使用這些套件管理員。

這些套件管理員專為各種作業系統與發行版本而設計。

- 對於 Windows 與 Linux (Ubuntu 發行版本)，使用[套件管理員](./deploy-install-azdata-installer.md)安裝比較容易。
- 若為 Linux (Ubuntu)，[請使用 `apt` 安裝 `azdata`](#azdata-apt)

目前沒有任何套件管理員能夠在其他作業系統或發行版上安裝 `azdata`。 對於這些平台，請參閱[不使用套件管理員安裝 `azdata`](./deploy-install-azdata.md)。

## <a id="linux"></a>安裝適用於 Linux 的 `azdata`

`azdata` 安裝套件可用於具有 `apt` 的 Ubuntu。

### <a id="azdata-apt"></a>使用 apt (Ubuntu) 安裝 `azdata`

>[!NOTE]
>`azdata` 套件不會使用系統 Python，而會安裝自己的 Python 解譯器。

1. 取得安裝程序所需的套件：

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 下載及安裝簽署金鑰：

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. 新增 `azdata` 存放庫資訊：

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2019.list)"
    ```

4. 更新存放庫資訊並安裝 `azdata`：

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 確認安裝：

    ```bash
    azdata --version
    ```

### <a name="update"></a>更新

僅升級 `azdata`：

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

1. 使用 apt-get remove 解除安裝：

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. 移除 `azdata` 存放庫資訊：

    >[!NOTE]
    >若您計劃在未來安裝 `azdata`，就無須執行此步驟

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 移除簽署金鑰：

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. 移除任何 Azdata CLI 一併安裝但不需要的相依性：

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
