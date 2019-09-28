---
title: 在 Linux 上使用安裝程式安裝 azdata
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝 azdata 工具，以安裝和管理使用安裝程式（Linux）的 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] （預覽）。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2795178cb975ecb620528c4a5dc8715b70d447fd
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342012"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>安裝 `azdata` 以管理 Linux 上的 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在 Linux 上安裝適用于 SQL Server 2019 Big Data 叢集發行候選版本的 `azdata`。 在這些套件管理員可供使用之前，必須先安裝 `azdata`，`pip`。

封裝管理員是針對各種作業系統和散發而設計的。

- 若為 Linux （Ubuntu），請[使用 `apt` 安裝 `azdata`](#azdata-apt)

目前，沒有任何套件管理員可在其他作業系統或發行版本上安裝 `azdata`。 針對這些平臺，請參閱[安裝不含套件管理員的 `azdata`](./deploy-install-azdata.md)。

## <a id="linux"></a>安裝適用于 Linux 的 `azdata`

`azdata` 安裝套件適用于具有 `apt` 的 Ubuntu。

### <a id="azdata-apt"></a>使用 apt 安裝 `azdata` （Ubuntu）

>[!NOTE]
>@No__t-0 套件不會使用系統 Python，而是會安裝它自己的 Python 解譯器。

1. 取得安裝程式所需的套件：

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 下載並安裝簽署金鑰：

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

3. 新增 @no__t 0 存放庫資訊：

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. 更新存放庫資訊，並安裝 `azdata`：

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 確認安裝：

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

升級 @no__t-僅限0：

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

1. 使用 apt 卸載-get remove：

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. 移除 `azdata` 存放庫資訊：

    >[!NOTE]
    >如果您計畫在未來安裝 `azdata`，則不需要執行此步驟

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 移除簽署金鑰：

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. 移除與 Azdata CLI 一起安裝的任何不必要相依性：

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>後續步驟

如需有關 big data 叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
