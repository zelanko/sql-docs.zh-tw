---
title: 在容器中執行 SQL Server 機器學習服務 | Microsoft Docs
description: 此教學課程示範如何在 Docker 上執行的 Linux 容器中使用 SQL Server 機器學習服務。
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 4fa470ce5b35cf8e78f919080988b5091af6e04e
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890920"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>在容器中執行 SQL Server 機器學習服務

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此教學課程示範如何使用 SQL Server 機器學習服務來建置 Docker 容器，以及如何從 Transact-SQL 執行機器學習指令碼。 涵蓋範圍包括下列工作：

> [!div class="checklist"]
> * 複製 mssql-docker 存放庫。
> * 建置具有機器學習服務的 SQL Server Linux 容器映像。
> * 執行具有機器學習服務的 SQL Server Linux 容器映像。
> * 使用 Transact-SQL 陳述式執行 R 或 Python 指令碼。
> * 停止並移除 SQL Server Linux 容器。

## <a name="prerequisites"></a>先決條件

* Git 命令列介面。
* 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
* 至少 2 GB 的磁碟空間。
* 至少 2 GB 的 RAM。
* [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>複製 mssql-docker 存放庫

1. 開啟 Linux 或 Mac 上的 Bash 終端機或 Windows 上的 WSL 終端機。

1. 建立本機目錄，以保存 mssql-docker 存放庫的本機複本。
1. 執行 git clone 命令以複製 mssql-docker 存放庫：

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image-with-machine-learning-services"></a>建置具有機器學習服務的 SQL Server Linux 容器映像

1. 將目錄變更為 mssql-mlservices 目錄：

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. 執行 build.sh 指令碼：

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > 若要建置 Docker 映像，您必須安裝大小為數 GB 的套件。 視網路頻寬而定，指令碼最多可能需要 20 分鐘才能完成執行。

## <a name="run-the-sql-server-linux-container-image-with-machine-learning-services"></a>執行具有機器學習服務的 SQL Server Linux 容器映像

1. 執行容器之前，請先設定您的環境變數。 將 PATH_TO_MSSQL 環境變數設定為主機目錄：

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. 執行 run.sh 指令碼：

   ```bash
   ./run.sh
   ```

   此命令會使用 Developer 版本 (預設值) 建立具有機器學習服務的 SQL Server 容器。 SQL Server 連接埠 **1433** 在主機上會公開為連接埠 **1401**。

   > [!NOTE]
   > 在容器中執行生產 SQL Server 版本的程序將有些微差異。 如需詳細資訊，請參閱[在 Docker 上設定 SQL Server 容器映像](sql-server-linux-configure-docker.md)。 如果您使用相同的容器名稱和連接埠，本逐步解說的其餘部分仍然可與生產容器搭配運作。

1. 若要檢視 Docker 容器，請執行 `docker ps` 命令：

   ```bash
   sudo docker ps -a
   ```

1. 若 **STATUS** 欄位顯示的狀態含 **Up**，表示 SQL Server 正在容器中執行且接聽於 **PORTS** 欄位中指定的連接埠。 若 SQL Server 容器的 **STATUS** 欄位顯示 **Exited**，請參閱[設定指南的＜疑難排解＞一節](sql-server-linux-configure-docker.md#troubleshooting)。

   ```bash
   $ sudo docker ps -a
   ```

    輸出： 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="change-the-sa-password"></a>變更 SA 密碼

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="execute-r--python-scripts-from-transact-sql"></a>從 Transact-SQL 執行 R / Python 指令碼

1. 連線到容器中的 SQL Server，然後執行下列 T-SQL 陳述式來啟用外部指令碼設定選項：

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. 執行下列簡單的 R/Python sp_execute_external_script，來確認機器學習服務正在運作：

    ```sql
    execute sp_execute_external_script 
    @language = N'R',
    @script = N'
    print("Hello World!")
    print(R.version)
    print(Revo.version)
    OutputDataSet <- InputDataSet', 
    @input_data_1 = N'select 1'
    with result sets((i int));
    go
    ```

    ```sql
    execute sp_execute_external_script 
    @language = N'Python',
    @script = N'
    import sys
    print(sys.version)
    print("Hello World!")
    OutputDataSet = InputDataSet',
    @input_data_1 = N'select 1'
    with result sets((i int));
    go 
    ```

## <a name="next-steps"></a>後續步驟

在此教學課程中，您已了解如何執行下列動作：

> [!div class="checklist"]
> * 複製 mssql-docker 存放庫
> * 使用機器學習服務建置 SQL Server Linux 容器映像
> * 使用機器學習服務執行 SQL Server Linux 容器映像
> * 使用 Transact-SQL 陳述式執行 R 或 Python 指令碼
> * 停止並移除 SQL Server Linux 容器

接下來，請檢閱其他 Docker 設定和疑難排解案例：

> [!div class="nextstepaction"]
>[Docker 上 SQL Server 的設定指南](sql-server-linux-configure-docker.md)
