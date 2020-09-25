---
title: 使用安裝程式在 Linux 上安裝 azdata
titleSuffix: ''
description: 了解如何使用安裝程式來安裝 azdata 工具 (Linux)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2dc1c3d58ee5f7b6ea032a2e41f7c18431229881
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914968"
---
# <a name="install-azdata-with-apt"></a>使用 apt 安裝 `azdata`

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/azdata.md)]

本文描述如何在 Linux 上安裝 `azdata`。 您必須先使用 `pip` 安裝 `azdata`，才能開始使用這些套件管理員。

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-azdata-for-linux"></a><a id="linux"></a>安裝適用於 Linux 的 `azdata`

`azdata` 安裝套件可用於具有 `apt` 的 Ubuntu。

### <a name="install-azdata-with-apt-ubuntu"></a><a id="azdata-apt"></a>使用 apt (Ubuntu) 安裝 `azdata`

>[!NOTE]
>`azdata` 套件不會使用系統 Python，而會安裝自己的 Python 解譯器。

1. 取得安裝程序所需的套件：

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
    ```

2. 下載及安裝簽署金鑰：

    ```bash
    curl -sL https://packages.microsoft.com/keys/microsoft.asc |
    gpg --dearmor |
    sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
    ```

3. 新增 `azdata` 存放庫資訊。

   針對 Ubuntu 16.04 用戶端，執行：
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   針對 Ubuntu 18.04 用戶端，執行：
    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
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

### <a name="uninstall"></a>解除安裝

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

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

使用 azdata 搭配[已啟用 Azure Arc 的資料服務](/azure/azure-arc/data/)