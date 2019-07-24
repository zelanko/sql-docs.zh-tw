---
title: 安裝 azdata
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝 azdata 工具, 以便安裝和管理 SQL Server 2019 big data 叢集 (預覽)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9444842081456563f411ad618f32b8dbd59f7513
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426438"
---
# <a name="install-azdata-to-manage-sql-server-big-data-clusters"></a>安裝 azdata 以管理 SQL Server big data 叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何在 Windows 或 Linux 上安裝適用于 CTP 3.2 的**azdata**工具。

## <a id="prerequisites"></a> 必要條件

**azdata**是以 Python 撰寫的命令列公用程式, 可讓叢集系統管理員透過 REST api 來啟動和管理大型資料叢集。 所需的最小 Python 版本為3.5 版。 您也`pip`必須使用此來下載並安裝**azdata**工具。 下列指示提供適用于 Windows 和 Ubuntu 的範例。 如需在其他平臺上安裝 Python, 請參閱[Python 檔](https://wiki.python.org/moin/BeginnersGuide/Download)。
此外, 您也必須安裝並更新最新版本的*要求*Python 套件:
```bash
pip3 install -U requests
```

> [!IMPORTANT]
> 如果您要安裝較新版本的 big data 叢集, 則必須在升級**azdata**並安裝新版本*之前, 先*備份您的資料並刪除舊的叢集。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

## <a id="windows"></a>Windows azdata 安裝

1. 在 Windows 用戶端上, 從[https://www.python.org/downloads/](https://www.python.org/downloads/)下載所需的 Python 套件。 針對 python 3.5.3 和更新版本, 當您安裝 Python 時, 也會一併安裝 pip3。 

   > [!TIP] 
   > 安裝 Python3 時, 請選取將 Python 新增至您的**路徑**。 如果沒有這麼做, 您可以在稍後尋找 pip3 所在位置, 並手動將它新增至您的**路徑**。

1. 開啟新的 Windows PowerShell 會話, 讓它取得最新的 Python 路徑。

1. 如果您已安裝任何舊版的工具 (名為**mssqlctl**的 previosly), 請務必先將它卸載, 再安裝最新版本的**azdata**。

   針對 CTP 3.1 或更低版本, 請執行下列命令。 在`ctp3.1`命令中, 將取代為您要卸載的**mssqlctl**版本。 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果您已安裝任何舊版的**azdata** , 請務必先將其卸載, 再安裝最新版本。

   針對 CTP 3.2 或更高版本, 請執行下列命令。 在`ctp3.2`命令中, 將取代為您要卸載的**azdata**版本。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 使用下列命令安裝**azdata** :

   ```powershell
   pip3 install -r https://aka.ms/azdata
   ```

## <a id="linux"></a>Linux azdata 安裝

在 Linux 上, 您必須安裝 Python 3.5, 然後升級 pip。 下列範例顯示適用于 Ubuntu 的命令。 如需其他 Linux 平臺, 請參閱[Python 檔](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安裝必要的 Python 套件:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. 升級 pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果您已安裝任何舊版的工具 (先前名為**mssqlctl**), 請務必先將它卸載, 再安裝最新版本的**azdata**。

   針對 CTP 3.1 或更低版本, 請執行下列命令。 在`ctp3.1`命令中, 將取代為您要卸載的**mssqlctl**版本。 

   ```powershell
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

1. 如果您已安裝任何舊版的**azdata** , 請務必先將其卸載, 再安裝最新版本。

   針對 CTP 3.2 或更高版本, 請執行下列命令。 在`ctp3.2`命令中, 將取代為您要卸載的**azdata**版本。

   ```powershell
   pip3 uninstall -r https://aka.ms/azdata
   ```

1. 使用下列命令安裝**azdata** :

   ```bash
   pip3 install -r https://aka.ms/azdata --user
   ```

   > [!NOTE]
   > 此`--user`參數會將 azdata 安裝至 Python 使用者安裝目錄。 這通常`~/.local/bin`是在 Linux 上。 請將此目錄新增至您的路徑, 或流覽至使用者安裝目錄`./azdata` , 然後從該處執行。

## <a name="next-steps"></a>後續步驟

如需 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
