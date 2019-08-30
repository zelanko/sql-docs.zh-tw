---
title: 使用 pip 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝 azdata 工具以使用 pip 安裝和管理[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a72e2ab39a17adef6c330f1ae17dcdc8a5dd8ddf
ms.sourcegitcommit: 71fac5fee00e0eca57e555f44274dd7e08d47e1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70160727"
---
# <a name="install-azdata-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-pip"></a>安裝`azdata`以[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]使用`pip`

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何使用`azdata` `pip`, 在 Windows 或 Linux 上安裝候選版的工具。

## <a id="prerequisites"></a> 必要條件

`azdata`是以 Python 撰寫的命令列公用程式, 可讓叢集系統管理員透過 REST Api 來啟動和管理大型資料叢集。 所需的最低 Python 版本為 3.5。 您也必須擁有`pip`該用來下載及安裝`azdata`工具。 下列說明提供適用於 Windows 和 Ubuntu 的範例。 如需在其他平台上安裝 Python，請參閱 [Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。
此外，您也必須安裝並更新「要求」的最新版本 Python 套件：
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 如果您要安裝較新版本的 big data 叢集, 則必須*先*備份您的資料, 並刪除舊的`azdata`叢集, 然後再升級並安裝新的版本。 如需詳細資訊，請參閱[升級為新版本](deployment-upgrade.md)。

## <a id="windows"></a>Windows `azdata`安裝

1. 在 Windows 用戶端上，從 [https://www.python.org/downloads/](https://www.python.org/downloads/) 下載所需的 Python 套件。 針對 Python 3.5.3 和更新版本，在您安裝 Python 時也會一併安裝 pip3。 

   > [!TIP] 
   > 安裝 Python3 時，請選取將 Python 新增至您的**路徑**。 如果您未這麼做，您也可以在稍後尋找 pip3 所在位置，並手動將其新增至您的**路徑**。

1. 開啟新的 Windows PowerShell 工作階段，讓其取得最新的路徑，其中包含 Python。

1. 如果您已安裝任何舊版的工具 (在 CTP 3.2 之前), 就必須先將它卸載, 再安裝最新版本的`azdata`。 下列命令會移除**mssqlctl**的 CTP 3.1 版本。

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果您已`azdata`安裝任何舊版, 請務必先將其卸載, 再安裝最新版本。

   針對 CTP 3.2, 請執行下列命令。

   ```powershell
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. 使用`azdata`下列命令安裝:

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Linux `azdata`安裝

在 Linux 上，您必須安裝 Python 3.5，然後升級 pip。 下列範例顯示適用於 Ubuntu 的命令。 針對其他 Linux 平台，請參閱 [Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安裝必要的 Python 套件：

   ```bash
   sudo apt-get update && \
   sudo apt-get install -y python3 && \
   sudo apt-get install -y python3-pip
   ```

1. 升級 pip3：

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果您已安裝任何舊版的工具 (在 CTP 3.2 之前), 就必須先將它卸載, 再安裝最新版本的`azdata`。 下列命令會移除**mssqlctl**的 CTP 3.1 版本。

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果您已`azdata`安裝任何舊版, 請務必先將其卸載, 再安裝最新版本。

   針對 CTP 3.2, 請執行下列命令。

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

1. 使用`azdata`下列命令安裝:

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > 參數會安裝`azdata`到 Python 使用者安裝目錄。 `--user` 在 Linux 上通常是 `~/.local/bin`。 請將此目錄新增至您的路徑，或巡覽至使用者安裝目錄，然後從該處執行 `./azdata`。

## <a name="next-steps"></a>後續步驟

如需有關 big data 叢集的詳細資訊, 請參閱[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]什麼是？](big-data-cluster-overview.md)。
