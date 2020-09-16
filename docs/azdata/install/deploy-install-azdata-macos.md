---
title: 安裝適用於 macOS 的 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何安裝 azdata 工具，以便安裝及管理適用於 macOS 的巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f6662a5ff7ced4c260e2b1a3fbd1efe5a285cf4a
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733652"
---
# <a name="install-azdata-on-macos"></a>在 macOS 上安裝 `azdata`

針對 macOS 平台，您可以使用 homebrew 套件管理員來安裝 `azdata-cli`。 CLI 套件已在下列 macOS 版本上測試過： 
* 10.13 High Sierra
* 10.14 Mojave
* 10.15 Catalina

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