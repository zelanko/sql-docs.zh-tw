---
title: 在容器中執行 SQL Server Machine Learning 服務 |Microsoft Docs
description: 本教學課程說明如何在 Docker 上執行的 Linux 容器中, 使用 SQL Server Machine Learning 服務。
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f3d3774adf4bee07269b25c3359b031ca24eb99e
ms.sourcegitcommit: ef7834ed0f38c1712f45737018a0bfe892e894ee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300430"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>在容器中執行 SQL Server Machine Learning 服務

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本教學課程示範如何使用 SQL Server Machine Learning 服務建立 Docker 容器, 並從 Transact-sql 執行 Machine Learning 腳本。

> [!div class="checklist"]
> * 複製 mssql-docker 存放庫。
> * 使用 Machine Learning 服務組建 SQL Server Linux 容器映射。
> * 使用 Machine Learning 服務執行 SQL Server Linux 容器映射。
> * 使用 Transact-sql 語句執行 R 或 Python 腳本。
> * 停止並移除 SQL Server Linux 容器。 

## <a name="prerequisites"></a>先決條件

* Git 命令列介面。
* 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。
* 至少 2 GB 的磁碟空間。
* 最少 2 GB 的 RAM。
* [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>複製 mssql-docker 存放庫

1. 開啟 Linux/Mac 上的 bash 終端機或 Windows 上的 WSL 終端機。

1. 建立本機目錄, 以在本機保存 mssql-docker 存放庫的複本。
1. 執行 git clone 命令以複製 mssql docker 存放庫。

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>使用 Machine Learning 服務組建 SQL Server Linux 容器映射

1. 將目錄變更為 mssql-mlservices 目錄。

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. 執行 build.sh 腳本。

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > 建立 docker 映射需要安裝大小為數 Gb 的套件。 視網路頻寬而定, 腳本可能需要最多20分鐘的時間才能完成。

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>使用 Machine Learning 服務執行 SQL Server Linux 容器映射

1. 在執行容器之前, 請先設定環境變數。 將 PATH_TO_MSSQL 環境變數設定為主機目錄。

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. 執行 run.sh 腳本。

   ```bash
   ./run.sh
   ```

   此命令會建立具有 Developer edition (預設值) Machine Learning 服務的 SQL Server 容器。 SQL Server 埠**1433**會在主機上公開為埠**1401**。

   > [!NOTE]
   > 在容器中執行生產 SQL Server 版本的程式稍有不同。 如需詳細資訊, 請參閱[在 Docker 上設定 SQL Server 容器映射](sql-server-linux-configure-docker.md)。 如果您使用相同的容器名稱和埠, 本逐步解說的其餘部分仍然可與生產環境容器搭配運作。

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>從 Transact-sql 執行 R/Python 腳本

1. 連接到容器中的 SQL Server, 然後執行下列 T-sql 語句來啟用 [外部腳本設定] 選項。

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. 執行下列簡單的 R/Python sp_execute_external_script, 確認 Machine Learning 服務正在運作。

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

在本教學課程中, 您已瞭解如何執行下列動作:

> [!div class="checklist"]
> * 複製 mssql-docker 存放庫。
> * 使用 Machine Learning 服務組建 SQL Server Linux 容器映射。
> * 使用 Machine Learning 服務執行 SQL Server Linux 容器映射。
> * 使用 Transact-sql 語句執行 R 或 Python 腳本。
> * 停止並移除 SQL Server Linux 容器。

接下來, 請參閱其他 Docker 設定和疑難排解案例:

> [!div class="nextstepaction"]
>[Docker 上的 SQL Server 設定指南](sql-server-linux-configure-docker.md)
