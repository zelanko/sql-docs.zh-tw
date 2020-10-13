---
title: 安裝適用於 macOS 的 azdata
titleSuffix: ''
description: 了解如何在 macOS 上安裝 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 19a3542f77708dcf779cf01d5299e7ff6add8273
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725239"
---
# <a name="install-azdata-on-macos"></a>在 macOS 上安裝 `azdata`

針對 macOS 平台，您可以使用 Homebrew 套件管理員來安裝 `azdata-cli`。 CLI 套件已在下列 macOS 版本上測試過：

- 10.13 High Sierra
- 10.14 Mojave
- 10.15 Catalina

## <a name="install-with-homebrew"></a>使用 Homebrew 安裝

```bash
brew tap microsoft/azdata-cli-release
brew update
brew install azdata-cli
```

>[!IMPORTANT]
>`azdata-cli` 相依於 Homebrew `python3`、`freetds`、`unixodbc`、`zeromq` 套件，並會加以安裝。 `azdata-cli` 保證可與這些在 Homebrew 上發佈之相依性的最新版本相容。

## <a name="verify-install"></a>確認安裝

```bash
azdata
azdata --version
```

## <a name="update"></a>更新

請先更新您的本機存放庫資訊，然後更新 `azdata-cli` 套件。

```bash
brew tap microsoft/azdata-cli-release
brew update
brew upgrade azdata-cli
```

## <a name="uninstall"></a>解除安裝

使用 Homebrew 來解除安裝 `azdata-cli` 套件。

```bash
brew uninstall azdata-cli
```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

使用 azdata 搭配[已啟用 Azure Arc 的資料服務](/azure/azure-arc/data/)
