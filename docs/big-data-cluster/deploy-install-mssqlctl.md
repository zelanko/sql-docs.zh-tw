---
title: 安裝 mssqlctl
titleSuffix: SQL Server big data clusters
description: 了解如何安裝以安裝和管理 SQL Server 2019 巨量資料叢集 （預覽） mssqlctl 工具。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e7ca0cec461a7eee36d7bfe22fbdc4e2e0c3cc61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797900"
---
# <a name="install-mssqlctl-to-manage-sql-server-big-data-clusters"></a>安裝 mssqlctl 來管理 SQL Server 的巨量資料叢集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

這篇文章說明如何安裝**mssqlctl**在 Windows 或 Linux 上的工具。

**mssqlctl**是命令列公用程式，可讓叢集系統管理員啟動及管理巨量資料叢集，透過 REST Api 以 Python 所撰寫。 最小所需的 Python 版本為 3.5 版。 您也必須擁有`pip`用來下載並安裝**mssqlctl**工具。 下列指示提供 Windows 和 Ubuntu 的範例。 如需其他平台上安裝 Python，請參閱[Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。

> [!IMPORTANT]
> 如果您要安裝較新版的巨量資料叢集，您必須備份您的資料，並刪除舊的叢集*之前*升級**mssqlctl**並安裝新的版本。 如需詳細資訊，請參閱 <<c0> [ 升級至新版](deployment-upgrade.md)。

## <a id="windows"></a> Windows mssqlctl 安裝

1. Windows 用戶端上下載所需的 Python 套件，從[ https://www.python.org/downloads/ ](https://www.python.org/downloads/)。 Python3.5.3 和更新版本，則當您安裝 Python 時也會安裝 pip3。 

   > [!TIP] 
   > 當安裝 Python3，選取要將 Python 新增至您**路徑**。 如果您不這樣做，您可以稍後找出 pip3 所在的位置，並以手動方式將它新增至您**路徑**。

1. 因此，它會取得在其中使用 Python 的最新路徑，請開啟新的 Windows PowerShell 工作階段。

1. 如果您有任何舊版**mssqlctl**安裝，請務必要解除安裝**mssqlctl**第一次，然後再安裝最新版本。

   如果您要解除安裝**mssqlctl**對應至 CTP 版本 2.2 或更低執行：

   ```powershell
   pip3 uninstall mssqlctl
   ```

   CTP 2.3 或更新版本，請執行下列命令。 取代`ctp-2.5`在命令中使用新版**mssqlctl**您要解除安裝：

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

1. 安裝**mssqlctl**使用下列命令：

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

## <a id="linux"></a> Linux mssqlctl 安裝

在 Linux 上，您必須安裝 Python 3.5，然後再升級 pip。 下列範例會示範適用於 Ubuntu 的命令。 對於其他 Linux 平台，請參閱[Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 安裝所需的 Python 套件：

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. 升級 pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. 如果您有任何舊版**mssqlctl**安裝，請務必要解除安裝**mssqlctl**第一次，然後再安裝最新版本。

   如果您要解除安裝**mssqlctl**對應至 CTP 版本 2.2 或更低執行：

   ```powershell
   pip3 uninstall mssqlctl
   ```

   CTP 2.3 或更新版本，請執行下列命令。 取代`ctp-2.5`在命令中使用新版**mssqlctl**您要解除安裝：

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp-2.5/mssqlctl/requirements.txt
   ```

1. 安裝**mssqlctl**使用下列命令：

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt --user
   ```

   > [!NOTE]
   > `--user`參數會 mssqlctl 安裝的 Python 使用者安裝目錄。 這通常是`~/.local/bin`Linux 上。 請將此目錄新增至您的路徑或瀏覽至使用者的安裝目錄，然後執行`./mssqlctl`從該處。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
