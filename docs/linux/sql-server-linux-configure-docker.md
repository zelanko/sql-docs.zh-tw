---
title: Docker 上 SQL Server 的設定選項
description: 探索在 Docker 中與 SQL Server 2017 和 2019 preview 容器映射搭配使用和互動的不同方式。 這包括保存資料、複製檔案和疑難排解。
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: d24bb3566195c71a3b62d16fab867ab5085404b7
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388376"
---
# <a name="configure-sql-server-container-images-on-docker"></a>在 Docker 上設定 SQL Server 容器映射

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何透過 Docker 設定和使用[mssql-linux 容器映射](https://hub.docker.com/_/microsoft-mssql-server)。 此映像包含以 Ubuntu 16.04 為基礎，在 Linux 上執行的 SQL Server。 您可於適用於 Mac/Windows 的 Docker 上將其與 Docker 引擎 1.8 以上版本搭配使用。

> [!NOTE]
> 本文特別著重于使用 mssql-server-linux 映射。 Windows 映像並未涵蓋在內, 但您可以在 [ [mssql-伺服器-Windows Docker Hub] 頁面](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)上深入瞭解。

## <a name="pull-and-run-the-container-image"></a>提取及執行容器映像

若要提取並執行 SQL Server 2017 和 SQL Server 2019 preview 的 Docker 容器映射, 請遵循下列快速入門中的必要條件和步驟:

- [使用 Docker 執行 SQL Server 2017 容器映射](quickstart-install-connect-docker.md?view=sql-server-2017)
- [使用 Docker 執行 SQL Server 2019 preview 容器映射](quickstart-install-connect-docker.md?view=sql-server-ver15)

這篇設定文章提供下列各節的其他使用案例。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a>執行以 RHEL 為基礎的容器映射

SQL Server Linux 容器映射上的所有檔都指向以 Ubuntu 為基礎的容器。 從 SQL Server 2019 preview 開始, 您可以使用以 Red Hat Enterprise Linux (RHEL) 為基礎的容器。 在您所有的 docker 命令中, 將容器存放庫從**mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu**變更為**mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1** 。

例如, 下列命令會提取使用 RHEL 的最新 SQL Server 2019 preview 容器:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a>執行生產容器映射

上一節中的快速入門會從 Docker Hub 執行免費的開發人員版本 SQL Server。 如果您想要執行生產容器映射, 例如 Enterprise、Standard 或 Web edition, 則大部分的資訊仍然適用。 不過, 這裡有一些差異。

- 如果您有有效的授權, 您只能在生產環境中使用 SQL Server。 您可以在[這裡](https://go.microsoft.com/fwlink/?linkid=857693)取得免費的 SQL Server Express 生產授權。 SQL Server Standard 和 Enterprise Edition 授權可透過[Microsoft 大量授權](https://www.microsoft.com/licensing/default.aspx)取得。


- 開發人員容器映射也可以設定為執行生產環境版本。 使用下列步驟來執行生產版本:

請參閱[快速入門](quickstart-install-connect-docker.md)中的需求和執行程式。 您必須使用**MSSQL_PID**環境變數來指定生產版本。 下列範例顯示如何執行 Enterprise Edition 的最新 SQL Server 2017 容器映射:

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d store/microsoft/mssql-server-linux:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "store/microsoft/mssql-server-linux:2017-latest"
 ```

> [!IMPORTANT]
> 藉由將值**Y**傳遞給環境變數**ACCEPT_EULA** , 並將版本值傳遞至**MSSQL_PID**, 表示您擁有您想要使用之版本和 SQL Server 版本的有效和現有授權。 您也同意使用在 Docker 容器映射中執行的 SQL Server 軟體, 將受 SQL Server 授權的條款所規範。

> [!NOTE]
> 如需**MSSQL_PID**可能值的完整清單, 請參閱[在 Linux 上使用環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

::: moniker-end

## <a name="connect-and-query"></a>連接和查詢

您可以從容器外部或從容器內部, 連接及查詢容器中的 SQL Server。 下列各節將說明這兩種案例。 

### <a name="tools-outside-the-container"></a>容器外的工具

您可以從任何支援 SQL 連線的外部 Linux、Windows 或 macOS 工具, 連接到 Docker 電腦上的 SQL Server 實例。 一些常用的工具組括:

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

下列範例會使用**sqlcmd**來連接到在 Docker 容器中執行的 SQL Server。 連接字串中的 IP 位址是執行容器之主機電腦的 IP 位址。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

如果您對應不是預設的主機連接埠**1433**，將該連接埠新增至連接字串。 例如，如果您指定`-p 1400:1433`中您`docker run`命令，然後明確地連接指定通訊埠 1400。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>容器內的工具

從 SQL Server 2017 preview 開始, [SQL Server 的命令列工具](sql-server-linux-setup-tools.md)會包含在容器映射中。 如果您使用互動式命令提示字元附加至映射, 您可以在本機執行這些工具。

1. 使用 `docker exec -it` 命令在您執行的容器中啟動互動式 Bash 殼層。 在下列範例`e69e056c702d`中, 是容器識別碼。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 您不一定要指定整個容器識別碼。您只需要指定足夠的字元來唯一識別它。 因此在此範例中, 它可能已足夠使用`e6`或`e69` , 而不是完整識別碼。

2. 進入容器後，以 sqlcmd 進行本機連線。 請注意, sqlcmd 預設不在路徑中, 因此您必須指定完整路徑。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 當使用 sqlcmd 完成時, `exit`請輸入。

4. 完成互動式命令提示字元時, 輸入`exit`。 結束互動式 Bash 殼層後，容器會繼續執行。

## <a name="run-multiple-sql-server-containers"></a>執行多個 SQL Server 容器

Docker 提供一種方法, 可在相同的主機電腦上執行多個 SQL Server 容器。 針對需要在相同主機上 SQL Server 多個實例的案例, 這是一種方法。 每個容器都必須在不同的埠上公開本身。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

下列範例會建立兩個 SQL Server 2017 容器, 並將它們對應至主機電腦上的埠**1401**和**1402** 。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

下列範例會建立兩個 SQL Server 2019 preview 容器, 並將它們對應至主機電腦上的埠**1401**和**1402** 。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

現在有兩個 SQL Server 實例會在不同的容器中執行。 用戶端可以使用 Docker 主機的 IP 位址和容器的埠號碼, 連接到每個 SQL Server 實例。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a>建立自訂容器

您可以建立自己的[Dockerfile](https://docs.docker.com/engine/reference/builder/#usage)來建立自訂的 SQL Server 容器。 如需詳細資訊, 請參閱[結合 SQL Server 和 Node 應用程式的示範](https://github.com/twright-msft/mssql-node-docker-demo-app)。 如果您建立自己的 Dockerfile, 請留意前景程式, 因為此程式會控制容器的生命週期。 如果結束, 容器將會關閉。 例如, 如果您想要執行腳本並啟動 SQL Server, 請確定 SQL Server 進程是最右邊的命令。 所有其他命令都會在背景中執行。 這會在 Dockerfile 內的下列命令中說明:

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

如果您反轉上一個範例中的命令, 容器會在 do-my-sql-commands.sh 腳本完成時關閉。

## <a id="persist"></a>保存您的資料

您的 SQL Server 設定變更和資料庫檔案會保存在容器中, 即使您使用`docker stop`和`docker start`重新開機容器也一樣。 不過, 如果您使用`docker rm`移除容器, 則會刪除容器中的所有專案, 包括 SQL Server 和您的資料庫。 下一節將說明如何使用**資料磁片**區來保存您的資料庫檔案, 即使相關聯的容器已刪除也一樣。

> [!IMPORTANT]
> 針對 SQL Server, 請務必瞭解 Docker 中的資料持續性。 除了本節中的討論內容之外, 請參閱 Docker 的檔,[以瞭解如何管理 docker 容器中的資料](https://docs.docker.com/engine/tutorials/dockervolumes/)。

### <a name="mount-a-host-directory-as-data-volume"></a>將主機目錄掛接為數據磁片區

第一個選項是將主機上的目錄掛接為容器中的資料磁片區。 若要這麼做, 請`docker run`使用命令`-v <host directory>:/var/opt/mssql`搭配旗標。 這可讓您在容器執行之間還原資料。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

這項技術也可讓您在 Docker 外部共用和查看主機上的檔案。

> [!IMPORTANT]
> 目前不支援在 Mac 上使用 Linux 上的 SQL Server 映射的 Docker 的主機磁片區對應。 請改用資料磁片區容器。 這是目錄特有的`/var/opt/mssql`限制。 從掛接的目錄讀取可以正常運作。 例如, 您可以在 Mac 上使用-v 掛接主機目錄, 並從位於主機上的 .bak 檔案還原備份。

### <a name="use-data-volume-containers"></a>使用資料磁片區容器

第二個選項是使用資料磁片區容器。 您可以使用`-v`參數指定磁片區名稱, 而不是主機目錄, 來建立資料磁片區容器。 下列範例會建立名為**sqlvolume**的共用資料磁片區。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

> [!NOTE]
> 在 [執行] 命令中以隱含方式建立資料磁片區的這項技術無法與舊版的 Docker 搭配運作。 在此情況下, 請使用 Docker 檔中所述的明確步驟,[建立和裝載資料磁片區容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)。

即使您停止並移除此容器, 資料磁片區仍會保存。 您可以使用`docker volume ls`命令來查看它。

```bash
docker volume ls
```

如果您接著使用相同的磁片區名稱建立另一個容器, 新的容器會使用包含在該磁片區中的相同 SQL Server 資料。

若要移除資料磁片區容器, 請`docker volume rm`使用命令。

> [!WARNING]
> 如果您刪除資料磁片區容器, 則會*永久*刪除容器中的任何 SQL Server 資料。

### <a name="backup-and-restore"></a>備份與還原

除了這些容器技術, 您也可以使用標準 SQL Server 備份和還原技術。 您可以使用備份檔案來保護您的資料, 或將資料移至另一個 SQL Server 實例。 如需詳細資訊, 請參閱[在 Linux 上備份和還原 SQL Server 資料庫](sql-server-linux-backup-and-restore-database.md)。

> [!WARNING]
> 如果您建立備份, 請務必建立或複製容器外部的備份檔案。 否則, 如果移除容器, 也會一併刪除備份檔案。

## <a name="execute-commands-in-a-container"></a>在容器中執行命令

如果您有執行中的容器, 您可以在容器中從主機終端機執行命令。

若要取得容器識別碼, 請執行:

```bash
docker ps
```

若要在容器中啟動 bash 終端機, 請執行:

```bash
docker exec -it <Container ID> /bin/bash
```

現在您可以執行命令, 就像是在容器內的終端機中執行一樣。 完成後，鍵入 `exit`。 這會在互動式命令會話中結束, 但您的容器會繼續執行。

## <a name="copy-files-from-a-container"></a>從容器複製檔案

若要將檔案複製到容器外, 請使用下列命令:

```bash
docker cp <Container ID>:<Container path> <host path>
```

**範例:**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>將檔案複製到容器中

若要將檔案複製到容器中, 請使用下列命令:

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**範例:**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a id="tz"></a>設定時區

若要在具有特定時區的 Linux 容器中執行 SQL Server, 請設定**TZ**環境變數。 若要尋找正確的時區值, 請從 Linux bash 提示字元執行**tzselect**命令:

```bash
tzselect
```

選取時區之後, **tzselect**會顯示類似下列的輸出:

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

您可以使用這項資訊, 在您的 Linux 容器中設定相同的環境變數。 下列範例顯示如何在時區中的`Americas/Los_Angeles`容器中執行 SQL Server:

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2017-latest 
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
sudo docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -p 1433:1433 --name sql1 \
   -e 'TZ=America/Los_Angeles'\
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```
::: moniker-end

## <a id="tags"></a>執行特定 SQL Server 容器映射

在某些情況下, 您可能不會想要使用最新的 SQL Server 容器映射。 若要執行特定 SQL Server 容器映射, 請使用下列步驟:

1. 識別您想要使用之發行的 Docker**標記**。 若要查看可用的標籤, 請參閱[mssql-伺服器-Linux Docker hub 頁面](https://hub.docker.com/_/microsoft-mssql-server)。

2. 使用標記提取 SQL Server 容器映射。 例如, 若要提取 RC1 的映射, 請`<image_tag>`將下列`rc1`命令中的取代為。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 若要使用該映射執行新的容器, 請在`docker run`命令中指定標記名稱。 在下列命令中, 將`<image_tag>`取代為您想要執行的版本。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

這些步驟也可以用來降級現有的容器。 例如, 您可能想要復原或降級執行中的容器, 以進行疑難排解或測試。 若要降級執行中的容器, 您必須使用 data 資料夾的持續性技術。 遵循[升級一節](#upgrade)中所述的相同步驟, 但在執行新容器時, 指定較舊版本的標記名稱。

## <a id="version"></a>檢查容器版本

如果您想要知道執行中 docker 容器的 SQL Server 版本, 請執行下列命令來顯示它。 取代`<Container ID or name>`為目標容器識別碼或名稱。 將`<YourStrong!Passw0rd>`取代為 SA 登入的 SQL Server 密碼。

```bash
sudo docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'SELECT @@VERSION'
```

```PowerShell
docker exec -it <Container ID or name> /opt/mssql-tools/bin/sqlcmd `
   -S localhost -U SA -P "<YourStrong!Passw0rd>" `
   -Q 'SELECT @@VERSION'
```

您也可以識別目標 docker 容器映射的 SQL Server 版本和組建編號。 下列命令會顯示**microsoft/mssql-Server-linux: 2017-最新**映射的 SQL Server 版本和組建資訊。 其執行方式是使用環境變數**PAL_PROGRAM_INFO = 1**來執行新的容器。 產生的容器會立即結束, 而`docker rm`命令會將它移除。

```bash
sudo docker run -e PAL_PROGRAM_INFO=1 --name sqlver \
   -ti mcr.microsoft.com/mssql/server:2017-latest && \
   sudo docker rm sqlver
```

```PowerShell
docker run -e PAL_PROGRAM_INFO=1 --name sqlver `
   -ti mcr.microsoft.com/mssql/server:2017-latest; `
   docker rm sqlver
```

先前的命令會顯示類似下列輸出的版本資訊:

```Text
sqlservr
  Version 14.0.3029.16
  Build ID ee3d3882f1c48a7a7e590a620153012eaedc2f37143d485df945a079b9d4eeea
  Build Type release
  Git Version 65d42c4
  Built at Sat Jun 16 01:20:11 GMT 2018

PAL
  Build ID 60cfcb134bbae96d311f6a4f56aeb5a685b3809de80bcb61ec587a8f58b555eb
  Build Type release
  Git Version 21a4c11
  Built at Sat Jun 16 01:18:53 GMT 2018

Packages
  system.sfp                    6.2.9200.1,21a4c1178,
  system.common.sfp             10.0.15063.540
  system.certificates.sfp       6.2.9200.1,21a4c1178,
  system.netfx.sfp              4.6.1590.0
  secforwarderxplat.sfp         14.0.3029.16
  sqlservr.sfp                  14.0.3029.16
  sqlagent.sfp                  14.0.3029.16
```

## <a id="upgrade"></a>在容器中升級 SQL Server

若要使用 Docker 升級容器映射, 請先找出升級的版本戳記。 使用`docker pull`下列命令, 從登錄中提取此版本:

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

這會更新您所建立之任何新容器的 SQL Server 映射, 但不會更新任何執行中容器中的 SQL Server。 若要這樣做, 您必須使用最新的 SQL Server 容器映射建立新的容器, 並將您的資料移轉至該新容器。

1. 請確定您為現有的 SQL Server 容器使用其中一種[資料持續性技術](#persist)。 這可讓您使用相同的資料來啟動新的容器。

1. 使用`docker stop`命令停止 SQL Server 容器。

1. 使用`docker run`建立新的 SQL Server 容器, 並指定對應的主機目錄或資料磁片區容器。 請務必針對您的 SQL Server 升級使用特定的標記。 新的容器現在會使用新版本的 SQL Server 搭配現有的 SQL Server 資料。

   > [!IMPORTANT]
   > 目前僅支援 RC1、RC2 和 GA 之間的升級。

1. 確認您的資料庫和新容器中的資料。

1. (選擇性) 使用`docker rm`移除舊的容器。

## <a id="troubleshooting"></a> 疑難排解

下列各節提供在容器中執行 SQL Server 的疑難排解建議。

### <a name="docker-command-errors"></a>Docker 命令錯誤

如果您收到任何`docker`命令的錯誤, 請確定 docker 服務正在執行, 並嘗試以較高的許可權執行。

例如, 在 Linux 上, 執行`docker`命令時, 您可能會收到下列錯誤:

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果您在 Linux 上收到此錯誤, 請嘗試執行前面加`sudo`上的相同命令。 如果失敗, 請確認 docker 服務正在執行, 並在必要時啟動它。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 上, 確認您是以系統管理員身分啟動 PowerShell 或命令提示字元。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器啟動錯誤

如果 SQL Server 容器無法執行, 請嘗試下列測試:

- 如果您收到錯誤，例如 **' 無法建立端點 CONTAINER_NAME 上網路橋接器。啟動 proxy 時發生錯誤： 接聽 tcp 0.0.0.0:1433 繫結： 已經在使用中的位址。 '** ，則您嘗試對應到已在使用連接埠的容器連接埠 1433。 如果您在主機電腦，在本機執行 SQL Server，也可能會發生。 它也可會發生，如果您啟動兩個 SQL Server 容器，並嘗試將其同時對應到相同的主機連接埠。 如果發生這種情況，使用`-p`參數對應到不同的主機連接埠的容器連接埠 1433。 例如: 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2017-latest`.
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu`.
```

::: moniker-end

- 如果您收到錯誤, 例如 **「在嘗試連線到 Docker daemon 通訊端時發生許可權遭到拒絕 unix:///var/run/docker.sock:在嘗試啟動容器時, 取得 http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: 撥號 unix/var/run/docker.sock: 連線: 許可權已拒絕, 然後將您的使用者新增至 Ubuntu 中的 docker 群組。** 然後再次登出並登入, 因為這種變更會影響新的會話。 

   ```bash
    usermod -aG docker $USER
    ```
- 查看是否有來自容器的錯誤訊息。

    ```bash
    docker logs e69e056c702d
    ```

- 請確定您符合快速入門文章的[必要條件](quickstart-install-connect-docker.md#requirements)一節中所指定的最小記憶體和磁片需求。

- 如果您使用任何容器管理軟體, 請確定它支援以 root 身分執行的容器進程。 容器中的 sqlservr.exe 進程會以 root 的身分執行。

- 請參閱[SQL Server 設定和錯誤記錄](#errorlogs)檔。

### <a name="enable-dump-captures"></a>啟用傾印捕獲

如果 SQL Server 進程在容器內失敗, 您應該建立已啟用**SYS_PTRACE**的新容器。 這會新增 Linux 功能來追蹤進程, 這是在例外狀況上建立傾印檔案的必要項。 支援人員可以使用傾印檔案來協助疑難排解問題。 下列 docker run 命令會啟用這項功能。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 連接失敗

如果您無法連接到在您的容器中執行的 SQL Server 實例, 請嘗試下列測試:

- 查看`docker ps -a`輸出的 [**狀態**] 資料行, 以確定您的 SQL Server 容器正在執行。 如果不是, `docker start <Container ID>`請使用來啟動它。

- 如果您對應至非預設的主機連接埠 (不是 1433)，請確定您在連接字串中指定的連接埠。 您可以看到您的連接埠對應中**連接埠**資料行`docker ps -a`輸出。 例如，下列命令會連接到 sqlcmd 接聽通訊埠 1401容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果您搭配`docker run`現有的對應資料磁片區或資料磁片區容器使用, SQL Server 會忽略`MSSQL_SA_PASSWORD`的值。 相反地, 預先設定的 SA 使用者密碼會從資料磁片區或資料磁片區容器中的 SQL Server 資料使用。 確認您使用的 SA 密碼與您要附加的資料相關聯。

- 請參閱[SQL Server 設定和錯誤記錄](#errorlogs)檔。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性群組

如果您使用 Docker 搭配 SQL Server 可用性群組, 則有兩個額外的需求。

- 對應用於複本通訊的埠 (預設值為 5022)。 例如, 指定`-p 5022:5022`做為`docker run`命令的一部分。

- 使用`-h YOURHOSTNAME` `docker run`命令的參數明確設定容器主機名稱。 當您設定可用性群組時, 會使用此主機名稱。 如果您未使用`-h`來指定它, 則會預設為容器識別碼。

### <a id="errorlogs"></a>SQL Server 設定和錯誤記錄檔

您可以查看 **/var/opt/mssql/log**中的 SQL Server 設定和錯誤記錄檔。 如果容器不在執行中, 請先啟動容器。 然後使用互動式命令提示字元來檢查記錄。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

從您容器內的 bash 會話, 執行下列命令:

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 如果您在建立容器時將主機目錄掛接至 **/var/opt/mssql** , 您可以改為查看主機上對應路徑上的**記錄**檔子目錄。

## <a name="next-steps"></a>後續步驟

透過[快速入門](quickstart-install-connect-docker.md), 開始使用 Docker 上的 SQL Server 2017 容器映射。

另請參閱[mssql-Docker GitHub 存放庫](https://github.com/Microsoft/mssql-docker), 以取得資源、意見反應和已知問題。

[探索 SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)
