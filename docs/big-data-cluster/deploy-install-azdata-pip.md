---
title: 使用 pip 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 了解如何使用 pip 安裝 azdata 工具，以安裝及管理巨量資料叢集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 01/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5360e7aa9718fef0d17bf73b9064c2d1a61a4577
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75726945"
---
# <a name="install-azdata-with-pip"></a>使用 `azdata` 安裝 `pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文描述如何使用 `azdata` 在 Windows 或 Linux 上 安裝 `pip`。

對於 Windows 與 Linux (Ubuntu 發行版本)，使用[套件管理員](./deploy-install-azdata-installer.md)安裝比較容易。

## <a name="prerequisites"></a><a id="prerequisites"></a> 必要條件

`azdata` 是以 Python 撰寫的命令列公用程式，可讓叢集系統管理員透過 REST API 啟動及管理巨量資料叢集。 所需的最低 Python 版本為 3.5。 您也必須擁有 `pip`，才能下載及安裝 `azdata` 工具。 下列說明提供適用於 Windows 和 Ubuntu 的範例。 如需在其他平台上安裝 Python，請參閱 [Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。
此外也請安裝及更新最新版的 `requests` Python 套件：

```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 若要安裝較新版的巨量資料叢集，必須在升級 `azdata` 及安裝新版之前，先備份您的資料，並刪除舊叢集。 如需詳細資訊，請參閱[升級為新版本](deployment-upgrade.md)。

## <a name="windows-azdata-installation"></a><a id="windows"></a> Windows `azdata` 安裝

1. 在 Windows 用戶端上，從 [https://www.python.org/downloads/](https://www.python.org/downloads/) 下載所需的 Python 套件。 針對 Python 3.5.3 和更新版本，在您安裝 Python 時也會一併安裝 pip3。 

   > [!TIP] 
   > 安裝 Python3 時，請選取將 Python 新增至您的 `PATH`。 若安裝時未採取此動作，也可以在之後尋找 pip3 的位置，然後手動將其新增至您的`PATH`。

1. 開啟新的 Windows PowerShell 工作階段，讓其取得最新的路徑，其中包含 Python。

1. 如果您已安裝任何舊版的 `azdata`，請務必先解除安裝，然後安裝最新版本。

   對於 CTP 3.2 或 RC1，請執行下列命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   或
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 使用下列命令安裝 `azdata`：

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="linux-azdata-installation"></a><a id="linux"></a> Linux `azdata` 安裝

在 Linux 上，您必須安裝 Python 3.5，然後升級 pip。 下列範例顯示適用於 Ubuntu 的命令。 針對其他 Linux 平台，請參閱 [Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安裝必要的 Python 套件：

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip && \
   sudo apt-get install -y libkrb5-dev && \
   sudo apt-get install -y libsqlite3-dev && \
   sudo apt-get install -y unixodbc-dev
   ```

1. 升級 pip3：

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果您已安裝任何舊版的 `azdata`，請務必先解除安裝，然後安裝最新版本。

   對於 CTP 3.2 或 RC1，請執行下列命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```
   或
   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 使用下列命令安裝 `azdata`：

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` 參數會將 `azdata` 安裝至 Python 使用者安裝目錄。 在 Linux 上通常是 `~/.local/bin`。 請將此目錄新增至您的路徑，或巡覽至使用者安裝目錄，然後從該處執行 `./azdata`。

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> 在 macOS 或 OS X 上安裝 `azdata`

若要在 macOS 或 OS X 上安裝 `azdata`，請完成下列步驟。 在每個步驟中，於在 [終端機] 中執行範例。

1. 在 macOS 用戶端上，安裝 [Homebrew](https://brew.sh) (若還未安裝)：

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. 安裝 Python 及 pip (最低版本 3.0)：

   ```
   brew install python3
   ```

1. 安裝相依性：

   ```
   pip3 install -U requests
   brew install freetds
   ```

1. 您先前如有安裝任何舊版工具，請務必先解除安裝，然後再安裝 `azdata` 的最新版本。 下列命令會移除 `azdata` 的版本。

   ```
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 使用下列命令安裝 `azdata`：

   ```
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)。
