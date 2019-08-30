---
title: 在 Linux 上使用安裝程式安裝 azdata
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝 azdata 工具, 以便使用安裝程式 ( [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Linux) 安裝和管理 (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e11e4851294ac8ffd8efa66e2156dcd47bce3aa0
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160678"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-on-linux"></a>安裝`azdata`以在[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] Linux 上管理

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在 Linux 上`azdata`安裝適用于 SQL Server 2019 Big Data 叢集候選版。 在這些套件管理員可供使用之前, `azdata`需要`pip`安裝。

封裝管理員是針對各種作業系統和散發而設計的。

- 若為 Linux (Ubuntu), 請[使用安裝`azdata` `apt` ](#azdata-apt)

目前, 在其他作業系統或散發套件上, 沒有`azdata`要安裝的封裝管理員。 針對這些平臺, 請[參閱`azdata`不安裝套件管理員](./deploy-install-azdata.md)。

## <a id="linux"></a>針對`azdata` Linux 安裝

`azdata`安裝套件適用于具有`apt`的 Ubuntu。

### <a id="azdata-apt"></a>使用`azdata` apt 安裝 (Ubuntu)

>[!NOTE]
>`azdata`套件不會使用系統 Python, 而是會安裝它自己的 python 解譯器。

1. 取得安裝程式所需的套件:

    ```bash
    sudo apt-get update
    sudo apt-get install gnupg ca-certificates curl apt-transport-https lsb-release -y
    ```

2. 下載並安裝簽署金鑰:

    ```bash
    wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```

3. 新增存放`azdata`庫資訊:

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"
    ```

4. 更新存放庫資訊並`azdata`安裝:

    ```bash
    sudo apt-get update
    sudo apt-get install -y azdata-cli
    ```

5. 確認安裝:

    ```bash
    azdata --version
    ```

### <a name="update"></a>Update

僅`azdata`限升級:

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

### <a name="uninstall"></a>Uninstall

1. 使用 apt 卸載-get remove:

    ```bash
    sudo apt-get remove -y azdata-cli
    ```

2. 移除存放`azdata`庫資訊:

    >[!NOTE]
    >如果您計畫在未來安裝`azdata` , 則不需要執行此步驟

    ```bash
    sudo rm /etc/apt/sources.list.d/azdata-cli.list
    ```

3. 移除簽署金鑰:

    ```bash
    sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
    ```

4. 移除與 Azdata CLI 一起安裝的任何不必要相依性:

    ```bash
    sudo apt autoremove
    ```

## <a name="next-steps"></a>後續步驟

如需有關 big data 叢集的詳細資訊, 請參閱[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]什麼是？](big-data-cluster-overview.md)。
