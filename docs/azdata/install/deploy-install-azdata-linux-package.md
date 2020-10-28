---
title: 使用 apt 安裝 Azure Data CLI (azdata)
description: 了解如何使用 apt 來安裝 Azure Data CLI (azdata) 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2f248978e09be4670d702805873a5ae6f4f7c9de
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257461"
---
# <a name="install-azure-data-cli-azdata-with-apt"></a>使用 apt 安裝 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

針對具有 `apt` 的 Linux 發行版本，有一個 `azdata-cli` 的套件。 該 CLI 套件已在使用 `apt` 的 Linux 版本上進行測試：

- Ubuntu 16.04、Ubuntu 18.04

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-apt"></a>使用 apt 安裝

>[!IMPORTANT]
> `azdata-cli` 的 RPM 套件相依於 python3 套件。 在您的系統上，這可能是早於 *Python 3.6.x* 需求的 Python 版本。 如果這對您造成問題，請尋找替代的 python3 套件，或遵循使用 [`pip`](../install/deploy-install-azdata-pip.md) 的手動安裝指示。

1. 安裝所需的相依性以安裝 `azdata-cli`。

   ```bash
   sudo apt-get update
   sudo apt-get install gnupg ca-certificates curl wget software-properties-common apt-transport-https lsb-release -y
   ```

2. 匯入 Microsoft 存放庫金鑰。

   ```bash
   curl -sL https://packages.microsoft.com/keys/microsoft.asc |
   gpg --dearmor |
   sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
   ```

3. 建立本機存放庫資訊。

   針對 Ubuntu 16.04 用戶端，執行：

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
    ```

   針對 Ubuntu 18.04 用戶端，執行：

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/prod.list)"
    ```

   針對 Ubuntu 20.04 用戶端，執行：

    ```bash
    sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/prod.list)
    ```

4. 安裝 `azdata-cli`。

   ```bash
   sudo apt-get update
   sudo apt-get install -y azdata-cli
   ```

## <a name="verify-install"></a>確認安裝

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

使用 `apt-get update` 與 `apt-get install` 命令來更新 `azdata-cli`。

```bash
sudo apt-get update && sudo apt-get install --only-upgrade -y azdata-cli
```

## <a name="uninstall"></a>解除安裝

1. 從系統移除套件。

   ```bash
   sudo apt-get remove -y azdata-cli
   ```

2. 如果您不打算重新安裝 `azdata-cli`，請移除存放庫資訊。

   ```bash
   sudo rm /etc/apt/sources.list.d/azdata-cli.list
   ```

3. 移除存放庫金鑰。

   ```bash
   sudo rm /etc/apt/trusted.gpg.d/dpgswdist.v1.asc.gpg
   ```

4. 移除不再需要的相依性。

   ```bash
   sudo apt autoremove
   ```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

使用 azdata 搭配[已啟用 Azure Arc 的資料服務](/azure/azure-arc/data/)