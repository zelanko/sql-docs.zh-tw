---
title: 使用 yum 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何使用 yum 安裝 azdata 工具，以安裝及管理巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cf6e061b0ca4fca7c843575a87038a801ab8f758
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75728549"
---
# <a name="install-azdata-with-yum"></a>使用 yum 安裝 `azdata`

針對具有 `yum` 的 Linux 發行版本，有一個 `azdata-cli` 的套件。 該 CLI 套件已在使用 `yum` 的 Linux 版本上進行測試：

- RHEL 7、RHEL 8


[!INCLUDE [azdata-package-installation-remove-pip-install](../includes/azdata-package-installation-remove-pip-install.md)]

## <a name="install-with-yum"></a>使用 yum 安裝

>[!IMPORTANT]
> `azdata-cli` 的 RPM 套件相依於 python3 套件。 在您的系統上，這可能是早於 *Python 3.6.x* 需求的 Python 版本。 如果這對您造成問題，請尋找替代的 python3 套件，或遵循使用 [`pip`](deploy-install-azdata-pip.md) 的手動安裝指示。

1. 匯入 Microsoft 存放庫金鑰

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

1. 建立本機存放庫資訊

   針對 RHEL 7 用戶端，請執行：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2019.repo
   ```
  
   針對 RHEL 8 用戶端，請執行：

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   ```

1. 使用 `yum install` 命令安裝

   ```bash
   sudo yum install azdata-cli
   ```

## <a name="verify-install"></a>確認安裝

```
azdata
azdata --version
```

## <a name="update"></a>更新

使用 `yum update` 命令更新 `azdata-cli`。

```bash
sudo yum update azdata-cli
```

## <a name="uninstall"></a>解除安裝

1. 從系統移除套件。

   ```bash
   sudo yum remove azdata-cli
   ```

1. 如果您不打算重新安裝 `azdata-cli`，請移除存放庫資訊

   ```bash
   sudo rm /etc/yum.repos.d/azdata-cli.repo
   ```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
