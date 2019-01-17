---
title: 安裝 mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何安裝以安裝和管理 SQL Server 2019 巨量資料叢集 （預覽） mssqlctl 工具。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/15/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aec8f030a996e5dd86c44a5a655e98d4926988ed
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361408"
---
# <a name="install-mssqlctl-to-manage-sql-server-2019-big-data-clusters"></a>安裝 mssqlctl 來管理 SQL Server 2019 巨量資料叢集

這篇文章說明如何安裝**mssqlctl**在 Windows 或 Linux 上的工具。

**mssqlctl**是命令列公用程式，可讓叢集系統管理員啟動及管理巨量資料叢集，透過 REST Api 以 Python 所撰寫。 最小所需的 Python 版本為 3.5 版。 您也必須擁有`pip`用來下載並安裝**mssqlctl**工具。 下列指示提供 Windows 和 Ubuntu 的範例。 如需其他平台上安裝 Python，請參閱[Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。

> [!IMPORTANT]
> 如果您已安裝舊版**mssqlctl**，您必須刪除叢集*之前*升級**mssqlctl**並安裝新的版本。 如需詳細資訊，請參閱 <<c0> [ 升級至新版](deployment-guidance.md#upgrade)。

## <a id="windows"></a> Windows mssqlctl 安裝

1. Windows 用戶端上下載所需的 Python 套件，從[ https://www.python.org/downloads/ ](https://www.python.org/downloads/)。 Python3.5.3 和更新版本，則當您安裝 Python 時也會安裝 pip3。 

   > [!TIP] 
   > 當安裝 Python3，選取要將 Python 新增至您**路徑**。 如果您不這樣做，您可以稍後找出 pip3 所在的位置，並以手動方式將它新增至您**路徑**。

1. 因此，它會取得在其中使用 Python 的最新路徑，請開啟新的 Windows PowerShell 工作階段。

2. 安裝**mssqlctl**使用下列命令：

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl
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
   
1. 安裝**mssqlctl**使用下列命令：

   ```bash
   pip3 install --extra-index-url https://private-repo.microsoft.com/python/ctp-2.2 mssqlctl --user
   ```
   
   > [!NOTE]
   > `--user`參數會 mssqlctl 安裝的 Python 使用者安裝目錄。 這通常是`~/.local/bin`Linux 上。 請將此目錄新增至您的路徑或瀏覽至使用者的安裝目錄，然後執行`./mssqlctl`從該處。
   
## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
