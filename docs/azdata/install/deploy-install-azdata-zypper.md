---
title: 使用 zypper 安裝 Azure Data CLI (azdata)
titleSuffix: ''
description: 了解如何使用 zypper 來安裝 Azure Data CLI (azdata) 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d43a1f9c65aa17fae3d262a51f45105b5f583cdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257506"
---
# <a name="install-azure-data-cli-azdata-with-zypper"></a>使用 zypper 安裝 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

針對具有 `zypper` 的 Linux 發行版本，有一個 `azdata-cli` 的套件。 該 CLI 套件已在使用 `zypper` 的 Linux 版本上進行測試：

- openSUSE 42.2 (leap) +
- SLES 12 SP 2 +

[!INCLUDE [azdata-package-installation-remove-pip-install](../../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-zypper"></a>使用 zypper 安裝

>[!IMPORTANT]
>`azdata-cli` 的 RPM 套件相依於 python3 套件。 在您的系統上，這可能是早於 *Python 3.6.x* 需求的 Python 版本。 如果這對您造成問題，請尋找替代的 python3 套件，或遵循使用 [`pip`](../install/deploy-install-azdata-pip.md) 的手動安裝指示。

1. 安裝所需的相依性以安裝 `azdata-cli`。

   ```bash
   sudo zypper install -y curl
   ```

1. 匯入 Microsoft 存放庫金鑰。

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. 建立本機存放庫資訊。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
   ```

1. 安裝 `azdata-cli`。

   ```bash
   sudo zypper install --from packages-microsoft-com-mssql-server-2019 -y azdata-cli
   ```

## <a name="verify-install"></a>確認安裝

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

使用 `zypper update` 命令更新 `azdata-cli`。

```bash
sudo zypper refresh
sudo zypper update azdata-cli
```

## <a name="uninstall"></a>解除安裝

從系統移除套件。

```bash
sudo zypper removerepo azdata-cli
```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

使用 azdata 搭配[已啟用 Azure Arc 的資料服務](/azure/azure-arc/data/)