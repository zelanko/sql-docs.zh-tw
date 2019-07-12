---
title: 執行 SQL Server Machine Learning 在容器中的服務 |Microsoft Docs
description: 本教學課程會示範如何使用 SQL Server Machine Learning 服務在 Docker 上執行的 Linux 容器。
author: uc-msft
ms.author: umajay
manager: craigg
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 3e654e29d6c49d3bf68cdfe7c4e3b479b47a973c
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67840467"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>執行 SQL Server Machine Learning 在容器中的服務

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程會示範如何建置 SQL Server Machine Learning 服務的 Docker 容器，並從 TRANSACT-SQL 中執行機器學習服務指令碼。

> [!div class="checklist"]
> * Mssql docker 存放庫複製。
> * 建置使用機器學習服務的 SQL Server Linux 容器映像。
> * 使用機器學習服務中執行 SQL Server Linux 容器映像。
> * 執行 R 或 Python 指令碼使用 TRANSACT-SQL 陳述式。
> * 停止並移除 SQL Server Linux 容器。 

## <a name="prerequisites"></a>先決條件

* Git 命令列介面。
* 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
* 至少 2 GB 的磁碟空間。
* 至少 2 GB 的 RAM。
* [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>Mssql docker 存放庫複製

1. 開啟 bash 終端機，在 Windows 上的 Linux/Mac 或 WSL 終端機上。

1. 建立要在本機保留一份 mssql docker 存放庫的本機目錄。
1. 執行 git clone 命令來複製 mssql docker 存放庫。

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>建置使用機器學習服務的 SQL Server Linux 容器映像

1. 將目錄變更為 mssql mlservices 目錄。

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. 執行 build.sh 指令碼。

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > 建置 docker 映像時，需要安裝幾個 Gb 大小的封裝。 指令碼可能需要 20 分鐘的時間才能完成，視網路頻寬而定。

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>使用機器學習服務中執行 SQL Server Linux 容器映像

1. 執行容器之前先設定環境變數。 將 PATH_TO_MSSQL 環境變數設定主應用程式目錄。

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. 執行 run.sh 指令碼。

   ```bash
   ./run.sh
   ```

   此命令會建立使用機器學習服務的 SQL Server 容器與開發人員版本 （預設值）。 SQL Server 連接埠**1433年**在連接埠與主機上公開**1401年**。

   > [!NOTE]
   > 在容器中執行生產 SQL Server 版本的程序會稍有不同。 如需詳細資訊，請參閱[執行生產容器映像](sql-server-linux-configure-docker.md#production)。 如果您使用相同的容器名稱和連接埠，本逐步解說的其餘部分仍適用於實際執行的容器。

1. 若要檢視 Docker 容器，請使用 `docker ps` 命令。

   ```bash
   sudo docker ps -a
   ```

1. 如果**狀態**資料行會顯示狀態為**向上**、 然後 SQL Server 正在執行中容器和接聽的通訊埠中指定**連接埠**資料行。 如果**狀態**資料行的 SQL Server 容器節目**Exited**，請參閱[疑難排解 > 一節的設定指南](sql-server-linux-configure-docker.md#troubleshooting)。

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>執行 R / Python 指令碼從 TRANSACT-SQL

1. 連接到容器中的 SQL Server，並執行下列 T-SQL 陳述式啟用外部指令碼組態選項。

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. 請確認機器學習服務正在執行下列的簡單 R/Python sp_execute_external_script。

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

在本教學課程中，您了解如何執行下列作業：

> [!div class="checklist"]
> * Mssql docker 存放庫複製。
> * 建置使用機器學習服務的 SQL Server Linux 容器映像。
> * 使用機器學習服務中執行 SQL Server Linux 容器映像。
> * 執行 R 或 Python 指令碼使用 TRANSACT-SQL 陳述式。
> * 停止並移除 SQL Server Linux 容器。

接下來，請檢閱其他的 Docker 設定及疑難排解案例：

> [!div class="nextstepaction"]
>[在 Docker 上的 SQL Server 的設定指南](sql-server-linux-configure-docker.md)
