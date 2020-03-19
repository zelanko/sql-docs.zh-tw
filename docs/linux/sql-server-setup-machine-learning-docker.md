---
title: 在 Docker 上安裝
titleSuffix: SQL Server Machine Learning Services
description: 了解如何在 Docker 上安裝 SQL Server 機器學習服務 (Python 與 R)。
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 02/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 767df0ec19f0749eab78a757db5bc92eb66cab49
ms.sourcegitcommit: 39d8d2d504d0ab70bac5ae3e981657e15dfb7bee
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/10/2020
ms.locfileid: "78964516"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>在 Docker 上安裝 SQL Server 機器學習服務 (Python 與 R)

本文說明如何在 Docker 上安裝 SQL Server 機器學習服務。 您可以使用機器學習服務來在資料庫中執行 Python 和 R 指令碼。 我們不會提供具有機器學習服務的預先建立容器， 但可使用 [GitHub 上提供的範例範本](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)，從 SQL Server 容器建立。

## <a name="prerequisites"></a>Prerequisites

- Git 命令列介面。
- 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/install/)。
- [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>複製 mssql-docker 存放庫

1. 在 Linux 或 Mac 上開啟 Bash 終端機，或在 Windows 上開啟 Windows 子系統 Linux 版終端機。

2. 建立本機目錄，以保存 mssql-docker 存放庫的本機複本。

3. 執行 git clone 命令以複製 mssql-docker 存放庫：

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>建置 SQL Server Linux 容器映像

1. 將目錄變更為 mssql-mlservices 目錄：

2. 在相同目錄中，執行下列命令：

    ```bash
       docker builds -t mssql-server-mlservices
    ```

3. 執行命令：

    ```bash
       docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=  -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    修改以新增 SA_PASSWORD 與 -v 路徑。 

4. 執行下列命令以確認：

    ```bash
       docker ps -a
    ```

   > [!NOTE]
   > 若要建置 Docker 映像，您必須安裝大小為數 GB 的套件。 視網路頻寬而定，指令碼最多可能需要 20 分鐘才能完成執行。

## <a name="run-the-sql-server-linux-container-image"></a>執行 SQL Server Linux 容器映像

1. 執行容器之前，請先設定您的環境變數。 將 PATH_TO_MSSQL 環境變數設定為主機目錄：

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

2. 執行 run.sh 指令碼：

   ```bash
   ./run.sh
   ```

   此命令會使用 Developer 版本 (預設值) 建立具有機器學習服務的 SQL Server 容器。 SQL Server 連接埠 **1433** 在主機上會公開為連接埠 **1401**。

   > [!NOTE]
   > 在容器中執行生產環境 SQL Server 版本的程序會稍有不同。 如需詳細資訊，請參閱[在 Docker 上設定 SQL Server 容器映像](sql-server-linux-configure-docker.md)。 如果您使用相同的容器名稱和連接埠，則本逐步解說的其餘部分仍適用於生產環境容器。

3. 若要檢視 Docker 容器，請執行 `docker ps` 命令：

   ```bash
   sudo docker ps -a
   ```

4. 若 **STATUS** 欄位顯示的狀態含 **Up**，表示 SQL Server 正在容器中執行且接聽於 **PORTS** 欄位中指定的連接埠。 若 SQL Server 容器的 **STATUS** 欄位顯示 **Exited**，請參閱[設定指南的＜疑難排解＞一節](sql-server-linux-configure-docker.md#troubleshooting)。

   ```bash
   $ sudo docker ps -a
   ```
    輸出：

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="run-in-a-container"></a>在容器中執行

[使用 Docker 執行 SQL Server 容器映像](quickstart-install-connect-docker.md)。

## <a name="connect-to-linux-sql-server-in-the-container"></a>連線至容器中的 Linux SQL Server

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>後續步驟

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [教學課程：在 T-SQL 中執行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視以真實世界案例為基礎的機器學習範例，請參閱[機器學習服務教學課程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)
