---
title: 在 Docker 上安裝
titleSuffix: SQL Server Machine Learning Services
description: 了解如何在 Docker 上安裝 SQL Server 機器學習服務 (Python 與 R)。
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/11/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e53acfa9e0fdfb7f7ee9b1ab6b7de5cd43ba8a9d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870036"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>在 Docker 上安裝 SQL Server 機器學習服務 (Python 與 R)

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

本文說明如何在 Docker 上安裝 SQL Server 機器學習服務。 您可以使用機器學習服務來在資料庫中執行 Python 和 R 指令碼。 我們不會提供具有機器學習服務的預先建立容器， 但可使用 [GitHub 上提供的範例範本](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)，從 SQL Server 容器建立。

## <a name="prerequisites"></a>必要條件

- Git 命令列介面。

- 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[取得 Docker](https://docs.docker.com/get-docker/) (英文)。

- 另請參閱 [Linux 上的 SQL Server 系統需求](sql-server-linux-setup.md#system)。

## <a name="clone-the-mssql-docker-repository"></a>複製 mssql-docker 存放庫

下列命令會將 `mssql-docker` Git 存放庫複製到本機目錄。

1. 開啟 Linux 或 Mac 上的 Bash 終端機。

2. 建立目錄，以保存 mssql-docker 存放庫的本機複本。

3. 執行 git clone 命令以複製 mssql-docker 存放庫：

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>建置 SQL Server Linux 容器映像

完成下列步驟以建置 Docker 映像：

1. 將目錄變更為 mssql-mlservices 目錄：
    
    ```bash
    /mssql-docker/linux/preview/examples/mssql-mlservices
    ```

2. 在相同目錄中，執行下列命令：

    ```bash
    docker build -t mssql-server-mlservices .
    ```

3. 執行命令：

    ```bash
    docker run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=<password> -v <directory on the host OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```
  
    > [!NOTE]
    > 您可針對 MSSQL_PID 使用下列任何值：Developer (free)、Express (free)、Enteprise (paid)、Standard (paid)。 如果使用付費版本，請確定已購買授權。 將 (password) 取代成實際密碼。 使用 -v 進行磁碟區掛接為選擇性。 將 (directory on the host OS) 取代成希望掛接資料庫資料和記錄檔的實際目錄。
    

4. 執行下列命令以確認：

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > 若要建置 Docker 映像，您必須安裝大小為數 GB 的套件。 視網路頻寬而定，指令碼可能需要一些時間才能完成執行。

## <a name="run-the-sql-server-linux-container-image"></a>執行 SQL Server Linux 容器映像

1. 執行容器之前，請先設定您的環境變數。 將 PATH_TO_MSSQL 環境變數設定為主機目錄：

   ```bash
   export MSSQL_PID='Developer'
   export ACCEPT_EULA='Y'
   export ACCEPT_EULA_ML='Y'
   export PATH_TO_MSSQL='/home/mssql/'
   ```
  
   > [!NOTE]
   > 在容器中執行生產環境 SQL Server 版本的程序會稍有不同。 如需詳細資訊，請參閱[在 Docker 上設定 SQL Server 容器映像](./sql-server-linux-docker-container-deployment.md)。 如果您使用相同的容器名稱和連接埠，則本逐步解說的其餘部分仍適用於生產環境容器。

2. 若要檢視 Docker 容器，請執行 `docker ps` 命令：

   ```bash
   sudo docker ps -a
   ```

3. 若 **STATUS** 資料行顯示的狀態含 **Up**，表示 SQL Server 正在容器中執行且接聽於 **PORTS** 資料行中指定的連接埠。 若 SQL Server 容器的 **STATUS** 欄位顯示 **Exited**，請參閱 [設定指南的＜疑難排解＞一節](./sql-server-linux-docker-container-troubleshooting.md)。

 
    輸出：

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>啟用機器學習服務

若要啟用機器學習服務，請連線至 SQL Server 執行個體並執行下列 T-SQL 陳述式：

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>後續步驟

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [Python 教學課程：在 SQL Server 機器學習服務中使用線性迴歸來預測滑雪工具租用](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python 教學課程：將 K-Means 叢集搭配 SQL Server 機器學習服務使用來分類客戶](../machine-learning/tutorials/python-clustering-model.md)

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [快速入門：在 T-SQL 中執行 R](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../machine-learning/tutorials/r-taxi-classification-introduction.md)