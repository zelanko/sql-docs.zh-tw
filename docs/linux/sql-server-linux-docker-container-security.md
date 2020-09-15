---
title: 安全的 SQL Server Docker 容器
description: 了解保護 SQL Server Docker 容器的不同方式，以及如何在主機上以不同的非根使用者執行容器
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.custom: contperfq1
ms.date: 09/07/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 10d2eb061a4ee6d9ff9c8d0594561667dd882dc9
ms.sourcegitcommit: 678f513b0c4846797ba82a3f921ac95f7a5ac863
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2020
ms.locfileid: "89511568"
---
# <a name="secure-sql-server-docker-containers"></a>安全的 SQL Server Docker 容器

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

SQL Server 2017 容器根據預設會以根使用者的身分啟動。 這可能會造成一些安全性疑慮。 本文會討論在執行 SQL Server Docker 容器時可使用的安全性選項，以及如何以非根使用者的身分建置 SQL Server 容器。

## <a name="build-and-run-non-root-sql-server-2017-containers"></a><a id="buildnonrootcontainer"></a> 建置並執行非根 SQL Server 2017 容器

請遵循下列步驟來建置以 `mssql` (非根) 使用者身分啟動的 SQL Server 2017 容器。

> [!NOTE]
> SQL Server 2019 容器會自動以非根身分啟動，因此下列步驟僅適用於預設以 root 身分啟動的 SQL Server 2017 容器。

1. 下載[適用於非根 SQL Server 容器的範例 dockerfile](https://raw.githubusercontent.com/microsoft/mssql-docker/master/linux/preview/examples/mssql-server-linux-non-root/Dockerfile)，並將它儲存為 `dockerfile`。

2. 在 dockerfile 目錄的內容中執行下列命令，建置非根 SQL Server 容器：

    ```bash
    cd <path to dockerfile>
    docker build -t 2017-latest-non-root .
    ```

3. 啟動容器。

    ```bash
    docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword@" --cap-add SYS_PTRACE --name sql1 -p 1433:1433 -d 2017-latest-non-root
    ```

    > [!NOTE]
    > `--cap-add SYS_PTRACE` 旗標是非根 SQL Server 容器產生傾印以用於疑難排解用途的必要項目。

4. 檢查容器是否正以非根使用者執行：

    ```bash
    docker exec -it sql1 bash
    ```

    執行 `whoami`，這將會傳回正在容器內執行的使用者。
    
    ```bash
    whoami
    ```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> 以主機上不同的非根使用者身分執行容器

若要以不同的非根使用者執行 SQL Server 容器，請將 -u 旗標新增至 docker run 命令。 非根容器包含限制，除非磁碟區是掛接到非根使用者可存取的 `/var/opt/mssql`，否則必須作為根群組的一部分執行。 根群組不會授與任何額外的根權限給非根使用者。

#### <a name="run-as-a-user-with-a-uid-4000"></a>以 UID 4000 的使用者執行

您可以使用自訂 UID 來啟動 SQL Server。 例如，以下命令會以 UID 4000 來啟動 SQL Server：

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> 請確定 SQL Server 容器具有像是 'mssql' 或 'root' 等具名使用者，否則 SQLCMD 將無法在容器內執行。 您可以在容器內執行 `whoami` 來檢查 SQL Server 容器是否正以具名使用者的身分執行。

#### <a name="run-the-non-root-container-as-the-root-user"></a>以根使用者身分執行非根容器

若需要，則可以根使用者的身分來執行非根容器。 這也會自動授與完整的檔案權限給容器，因為這是較高的權限。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-user-on-your-host-machine"></a>以您主機電腦上的使用者身分執行

您可以透過下列命令，使用主機電腦上現有的使用者來啟動 SQL Server：
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

#### <a name="run-as-a-different-user-and-group"></a>以不同的使用者和群組執行

您可以使用自訂使用者和群組來啟動 SQL Server。 在此範例中，已掛接磁碟區具備針對主機電腦上使用者或群組設定的權限。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> 為非根容器設定永續性儲存體權限

若要允許非根使用者存取已掛接磁碟區上的資料庫檔案，請確認執行容器的使用者或群組可讀取/寫入永續性檔案儲存體。  

您可以使用此命令來取得資料庫檔案目前的擁有權。

```bash
ls -ll <database file dir>
```

若 SQL Server 無法存取保存的資料庫檔案，請執行下列其中一個命令。

#### <a name="grant-the-root-group-rw-access-to-the-db-files"></a>授與根群組對 DB 檔案的讀寫存取權

授與根群組存取下列目錄的權限，讓非根 SQL Server 容器能夠存取資料庫檔案。

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

#### <a name="set-the-non-root-user-as-the-owner-of-the-files"></a>將非根使用者設為檔案的擁有者

這可以是預設的非根使用者，或是任何其他您想要指定的非根使用者。 在此範例中，我們會將 UID 10001 設為非根使用者。

```bash
chown -R 10001:0 <database file dir>
```

## <a name="next-steps"></a>後續步驟

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

- 透過此[快速入門](quickstart-install-connect-docker.md?view=sql-server-2017)，開始使用 Docker 上的 SQL Server 2017 容器映像

::: moniker-end

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

- 透過此[快速入門](quickstart-install-connect-docker.md?view=sql-server-ver15)，開始使用 Docker 上的 SQL Server 2019 容器映像

::: moniker-end

- [部署及連線到 SQL Server Docker 容器](sql-server-linux-docker-container-deployment.md)

- [參考 Docker 容器的其他組態及自訂](sql-server-linux-docker-container-configure.md)

- [針對 SQL Server Docker 容器進行疑難排解](sql-server-linux-docker-container-troubleshooting.md)