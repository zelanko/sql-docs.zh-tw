---
title: 使用 pip 安裝 azdata
titleSuffix: ''
description: 了解如何使用 pip 來安裝 azdata 工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ecf4eaaddf9423bb9a3ae88036b5c3cb2090451b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725279"
---
# <a name="install-azdata-with-pip"></a>使用 `pip` 安裝 `azdata`

[!INCLUDE[azdata](../../includes/applies-to-version/azdata.md)]

此文章描述如何使用 `pip` 在 Windows、Linux 或 macOS/OS X 上安裝 `azdata` 工具。

> [!TIP]
> 為了提供更簡單的體驗，`azdata` 可以使用適用於 Windows、Linux (Ubuntu、Debian、RHEL、CentOS、openSUSE 與 SLE 發行版本) 與 macOS 的[套件管理員](./deploy-install-azdata.md)來安裝。

## <a name="prerequisites"></a><a id="prerequisites"></a> 必要條件

`azdata` 是以 Python 撰寫的命令列公用程式，可讓叢集系統管理員透過 REST API 來啟動及管理資料資源。 所需的最低 Python 版本為 3.5。 需要 `pip` 才能下載及安裝 `azdata` 工具。 下面的指示提供適用於 Windows、Linux (Ubuntu) 與 macOS/OS X 的範例。如需在其他平台上安裝 Python 的詳細資訊，請參閱 [Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download) \(英文\)。 此外也請安裝及更新最新版的 `requests` Python 套件：

```bash
pip3 install -U requests
```

## <a name="windows-azdata-installation"></a><a id="windows"></a> Windows `azdata` 安裝

1. 在 Windows 用戶端上，從 [https://www.python.org/downloads/](https://www.python.org/downloads/) 下載所需的 Python 套件。 針對 Python 3.5.3 與更新版本，在您安裝 Python 時也會一併安裝 pip3。

   > [!TIP]
   > 安裝 Python3 時，請選取將 Python 新增至您的 `PATH`。 若安裝時未採取此動作，也可以在之後尋找 pip3 的位置，然後手動將其新增至您的`PATH`。

1. 開啟新的 Windows PowerShell 工作階段，讓其取得最新的路徑，其中包含 Python。

1. 從 SQL Server 2019 CU5 版本開始，azdata 與伺服器之間有獨立的語意版本。 如果您在這之前已安裝任何舊版的 `azdata`，請務必先解除安裝，然後安裝最新版本。

   例如，針對 2019-cu4，請執行下列命令：

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu4/requirements.txt
   ```

  > [!NOTE]
  > 在上面的範例中，請將 `2019-cu6` 取代為 `azdata` 安裝的版本與 CU。 

1. 安裝 `azdata`。

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

1. 升級 pip3。

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 從 SQL Server 2019 CU5 版本開始，azdata 與伺服器之間有獨立的語意版本。 如果您在這之前已安裝任何舊版的 `azdata`，請務必先解除安裝，然後安裝最新版本。

   例如，針對 `2019-cu6`，請執行下列命令：

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-cu6/requirements.txt
   ```

  > [!NOTE]
  > 在上面的範例中，請將 `2019-cu6` 取代為 `azdata` 安裝的版本與 CU。

1. 安裝 `azdata`。

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > `--user` 參數會將 `azdata` 安裝至 Python 使用者安裝目錄。 在 Linux 上通常是 `~/.local/bin`。 請將此目錄新增至您的路徑，或巡覽至使用者安裝目錄，然後從該處執行 `./azdata`。

## <a name="install-azdata-on-macos-or-os-x"></a><a id="macOSX"></a> 在 macOS 或 OS X 上安裝 `azdata`

若要在 macOS 或 OS X 上安裝 `azdata`，請完成下列步驟。 在每個步驟中，於在 [終端機] 中執行範例。

1. 在 macOS 用戶端上，安裝 [Homebrew](https://brew.sh) (若還未安裝)：

   ```bash
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   ```

1. 安裝 Python 及 pip (最低版本 3.0)：

   ```bash
   brew install python3
   ```

1. 安裝相依性：

   ```bash
   pip3 install -U requests
   brew install freetds
   ```

1. 從 SQL Server 2019 CU5 版本開始，azdata 與伺服器之間有獨立的語意版本。 如果您在這之前已安裝任何舊版的 `azdata`，請務必先解除安裝，然後安裝最新版本。 例如，下列命令會移除 `azdata` 的 RC1 版本：

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

1. 安裝 `azdata`。

   ```bash
   pip3 install -r https://aka.ms/azdata
   ```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]？](../../big-data-cluster/big-data-cluster-overview.md)。

使用 azdata 搭配[已啟用 Azure Arc 的資料服務](/azure/azure-arc/data/)
