---
title: 在 Docker 上的 SQL Server 組態選項
description: 探索不同的方式使用，並與其互動 SQL Server 2017 和 2019年預覽容器映像，在 Docker 中。 這包括複製檔案，並進行疑難排解的保存資料。
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
manager: jroth
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 34320ca5f0e969443ecd60eae64ca80a6aeaec63
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834069"
---
# <a name="configure-sql-server-container-images-on-docker"></a>在 Docker 上設定 SQL Server 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何設定和使用[mssql server linux 容器映像](https://hub.docker.com/_/microsoft-mssql-server)使用 Docker。 此映像包含以 Ubuntu 16.04 為基礎，在 Linux 上執行的 SQL Server。 您可於適用於 Mac/Windows 的 Docker 上將其與 Docker 引擎 1.8 以上版本搭配使用。

> [!NOTE]
> 本文特別著重於使用 mssql server linux 映像。 未涵蓋的 Windows 映像，但您可以深入了解上[mssql server windows Docker Hub 頁面](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)。

## <a name="pull-and-run-the-container-image"></a>提取及執行容器映像

提取及執行 Docker 容器映像，以使用 SQL Server 2017 和 SQL Server 2019 的預覽，請依照下列的必要條件和下列快速入門中的步驟：

- [以 Docker 執行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md?view=sql-server-2017)
- [以 Docker 執行 SQL Server 2019 預覽容器映像](quickstart-install-connect-docker.md?view=sql-server-ver15)

設定本文下列各節中的其他使用案例。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a id="rhel"></a> 執行 RHEL 為基礎的容器映像

所有 SQL Server Linux 容器映像上的文件會指向以 Ubuntu 為基礎的容器。 從 SQL Server 2019 preview 開始，您可以使用基礎上 Red Hat Enterprise Linux (RHEL) 的容器。 變更的容器存放庫**mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu**要**mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1**中所有的 docker 命令。

例如，下列命令會提取最新的 SQL Server 2019 預覽容器，使用 RHEL:

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CTP3.1
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a id="production"></a> 執行生產容器映像

快速入門中的上一節中會執行免費的 SQL Server 的開發人員版本，從 Docker Hub。 如果您想要執行生產容器映像，例如 Enterprise、 Standard 或 Web 版本，仍然適用於大部分的資訊。 不過，有幾個此處概述的差異。

- 如果您有有效的授權，可以只在生產環境中使用 SQL Server。 您可以取得免費的 SQL Server Express 生產授權[此處](https://go.microsoft.com/fwlink/?linkid=857693)。 SQL Server Standard 和 Enterprise Edition 授權都是透過[Microsoft 大量授權](https://www.microsoft.com/licensing/default.aspx)。


- 若要執行的生產版本，可以設定開發人員的容器映像。 您可以使用下列步驟來執行生產版本：

檢閱需求，並執行程序[快速入門](quickstart-install-connect-docker.md)。 您必須指定您的生產版本，具有**MSSQL_PID**環境變數。 下列範例示範如何執行 Enterprise edition 的最新的 SQL Server 2017 容器映像：

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
> 傳遞的值，藉以**Y**環境變數**ACCEPT_EULA**和版本值以**MSSQL_PID**，您要表達您有有效的和現有的授權，版本和您想要使用的 SQL Server 版本。 您也同意在 Docker 容器映像中執行的 SQL Server 軟體的使用會受到您的 SQL Server 授權條款。

> [!NOTE]
> 如需完整的可能值清單**MSSQL_PID**，請參閱[環境變數，在 Linux 上設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

::: moniker-end

## <a name="connect-and-query"></a>連線及查詢

您可以連接並查詢從外部容器，或從容器中的 SQL Server 容器。 下列各節會說明這兩種案例。 

### <a name="tools-outside-the-container"></a>對容器外部的工具

您可以從連線到 SQL Server 執行個體 Docker 機器上支援 SQL 連線的任何外部 Linux、 Windows 或 macOS 工具。 一些常見的工具包括：

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

下列範例會使用**sqlcmd**連線到 Docker 容器中執行的 SQL Server。 連接字串中的 IP 位址是正在執行容器主機電腦的 IP 位址。

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

### <a name="tools-inside-the-container"></a>在容器內的工具

開始使用 SQL Server 2017 preview [SQL Server 命令列工具](sql-server-linux-setup-tools.md)包括在容器映像。 如果您附加至互動式命令提示字元使用映像，您可以在本機執行的工具。

1. 使用 `docker exec -it` 命令在您執行的容器中啟動互動式 Bash 殼層。 在下列範例中`e69e056c702d`是容器識別碼。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 您不一定要指定整個容器的識別碼。您只需要指定字元足以唯一識別它。 因此在此範例中，它可能會不足以使用`e6`或`e69`而不是完整的識別碼。

2. 進入容器後，以 sqlcmd 進行本機連線。 請注意該 sqlcmd 不在路徑中，根據預設，因此您必須指定完整路徑。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 完成後使用 sqlcmd，鍵入`exit`。

4. 完成後的互動式命令提示字元，鍵入`exit`。 結束互動式 Bash 殼層後，容器會繼續執行。

## <a name="run-multiple-sql-server-containers"></a>執行多個 SQL Server 容器

Docker 提供相同的主機電腦上執行多個 SQL Server 容器的方式。 這是針對需要多個相同的主機上的 SQL Server 執行個體的案例的方法。 每個容器必須公開本身不同的連接埠。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

下列範例會建立兩個 SQL Server 2017 容器，並將它們對應至連接埠**1401年**並**1402年**主機電腦上。

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

下列範例會建立兩個 SQL Server 2019 預覽容器，並將它們對應至連接埠**1401年**並**1402年**主機電腦上。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

現在有兩個不同的容器中執行的 SQL Server 執行個體。 使用容器的 Docker 主機和連接埠號碼的 IP 位址，用戶端可以連線到每個 SQL Server 執行個體。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a id="customcontainer"></a> 建立自訂的容器

您可建立您自己[Dockerfile](https://docs.docker.com/engine/reference/builder/#usage)來建立自訂的 SQL Server 容器。 如需詳細資訊，請參閱 <<c0> [ 結合了 SQL Server 和 Node 應用程式的示範](https://github.com/twright-msft/mssql-node-docker-demo-app)。 如果您建立自己的 Dockerfile，請注意前景處理序，因為此程序可控制容器的生命週期。 如果結束，則容器也會關閉。 比方說，如果您想要執行指令碼，並啟動 SQL Server，請確定 SQL Server 處理序是最右邊的命令。 所有其他命令會在背景中執行。 下列命令在 Dockerfile 所示：

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

如果您反轉先前的範例中的命令，容器執行-我-sql-commands.sh 指令碼完成時，會關機。

## <a id="persist"></a> 保存您的資料

您的 SQL Server 組態變更和資料庫檔案會保存在容器即使您重新啟動的容器`docker stop`和`docker start`。 不過，如果您移除的容器`docker rm`，容器中的所有項目會遭到刪除，包括 SQL Server 和資料庫。 下列章節將說明如何使用**的資料磁碟區**保存您的資料庫檔案，即使刪除相關聯的容器。

> [!IMPORTANT]
> 針對 SQL Server，務必了解在 Docker 中的資料持續性。 除了本章節中討論，請參閱 Docker 文件上[如何管理在 Docker 容器中的資料](https://docs.docker.com/engine/tutorials/dockervolumes/)。

### <a name="mount-a-host-directory-as-data-volume"></a>作為資料磁碟區掛接主機目錄

第一個選項是您在主機上掛接目錄，為資料磁碟區容器中。 若要這樣做，請使用`docker run`命令搭配`-v <host directory>:/var/opt/mssql`旗標。 這可讓還原容器執行之間的資料。

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

這項技術也可讓您共用，並檢視外部 Docker 主機上的檔案。

> [!IMPORTANT]
> 在此階段不支援在 Mac 上與 SQL Server Linux 映像上的 docker 主機磁碟區對應。 請改用資料磁碟區容器。 這項限制是特有`/var/opt/mssql`目錄。 讀取從掛接的目錄運作正常。 例如，您可以掛接主機目錄，在 Mac 上使用 hyper-v，並位於主機的.bak 檔案中的備份還原。

### <a name="use-data-volume-containers"></a>使用資料磁碟區容器

第二個選項是使用資料磁碟區容器。 您可以藉由指定磁碟區名稱，而不是與主應用程式目錄中建立資料磁碟區容器`-v`參數。 下列範例會建立名為共用的資料量**sqlvolume**。

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
> 這項技術，以隱含方式執行的命令中建立的資料磁碟區無法搭配舊版的 Docker。 在此情況下，使用明確的步驟中的 Docker 文件，概述[建立和掛接資料磁碟區容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container)。

即使您停止並移除此容器時，會保存的資料量。 您可以檢視它與`docker volume ls`命令。

```bash
docker volume ls
```

如果您隨後會建立具有相同的磁碟區名稱的另一個容器，新的容器會使用包含磁碟區中的相同 SQL Server 資料。

若要移除資料磁碟區容器，請使用`docker volume rm`命令。

> [!WARNING]
> 如果您刪除資料磁碟區容器，容器中的任何 SQL Server 資料會*永久*刪除。

### <a name="backup-and-restore"></a>備份與還原

除了這些容器技術，您也可以使用標準的 SQL Server 備份和還原技術。 您可以使用備份檔案，來保護您的資料，或將資料移到另一個 SQL Server 執行個體。 如需詳細資訊，請參閱 < [Linux 上的資料庫備份和還原 SQL Server](sql-server-linux-backup-and-restore-database.md)。

> [!WARNING]
> 如果您建立備份，請務必要建立或複製容器之外的備份檔案。 否則，如果容器已移除，會一併刪除備份檔案。

## <a name="execute-commands-in-a-container"></a>在容器中執行命令

如果您有執行中的容器，您可以從主應用程式終端機中執行容器內的命令。

若要取得執行的容器識別碼：

```bash
docker ps
```

若要啟動終端機執行容器中的 bash:

```bash
docker exec -it <Container ID> /bin/bash
```

現在您可以執行命令，就好像您以在容器內的終端機中執行它們。 完成後，鍵入 `exit`。 這會結束互動式命令工作階段中，但您的容器會繼續執行。

## <a name="copy-files-from-a-container"></a>將檔案從一個容器

若要複製出容器的檔案，請使用下列命令：

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

## <a name="copy-files-into-a-container"></a>將檔案複製到容器

若要將檔案複製到容器，使用下列命令：

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
## <a id="tz"></a> 設定時區

若要在具有特定時區中的 Linux 容器中執行 SQL Server，設定**TZ**環境變數。 若要尋找正確的時區值，請執行**tzselect** Linux bash 提示字元命令：

```bash
tzselect
```

選取時區之後, **tzselect**會顯示類似下面的輸出：

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

您可以使用這項資訊來設定 Linux 容器中的同一個環境變數。 下列範例示範如何在容器中執行 SQL Server`Americas/Los_Angeles`時區：

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

## <a id="tags"></a> 執行特定的 SQL Server 容器映像

有的情況下您可能不想使用最新的 SQL Server 容器映像。 若要執行特定的 SQL Server 容器映像，請使用下列步驟：

1. 識別 Docker**標記**您想要使用的版本。 若要檢視可用的標籤，請參閱[mssql server linux Docker hub 頁面](https://hub.docker.com/_/microsoft-mssql-server)。

2. 提取 SQL Server 容器映像與標記。 例如，若要提取的 RC1 映像，取代`<image_tag>`在下列命令中使用`rc1`。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 若要執行該映像新的容器，指定的標記名稱`docker run`命令。 在下列命令中，取代`<image_tag>`與您想要執行的版本。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

這些步驟也可用來降級現有容器。 比方說，您可能想要復原，或降級用於疑難排解或測試執行中的容器。 若要降級執行中的容器，您必須使用持續性技術資料的資料夾。 遵循相同的步驟中所述[升級區段](#upgrade)，但是當您執行新的容器指定較舊版本的標記名稱。

## <a id="version"></a> 檢查容器版本

如果您想要知道在執行的 docker 容器中的 SQL Server 的版本，請執行下列命令來顯示它。 取代`<Container ID or name>`的目標容器識別碼或名稱。 取代`<YourStrong!Passw0rd>`SA 登入的 SQL Server 密碼。

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

您也可以識別 SQL Server 版本，並建置目標 docker 容器映像的數字。 下列命令會顯示 SQL Server 版本和組建資訊**microsoft/mssql 伺服器-linux:2017-最新**映像。 其做法是使用環境變數執行新的容器**PAL_PROGRAM_INFO = 1**。 產生的容器立即結束，而`docker rm`命令會移除它。

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

上述命令會顯示類似下列輸出的版本資訊：

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

## <a id="upgrade"></a> 在容器中的 SQL Server 升級

若要升級使用 Docker 容器映像，您必須先找出升級版本的標記。 從登錄提取本版`docker pull`命令：

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

這會更新任何新的容器，您建立時，SQL Server 映像，但它不會更新任何執行中的容器中的 SQL Server。 若要這樣做，您必須使用最新的 SQL Server 容器映像建立新的容器，並將資料移轉至該新的容器。

1. 請確定您使用其中一個[的資料持續性技術](#persist)您現有的 SQL Server 容器。 這可讓您使用相同的資料開始新的容器。

1. 停止 SQL Server 容器與`docker stop`命令。

1. 建立新的 SQL Server 容器與`docker run`並指定對應的主應用程式目錄或資料磁碟區容器。 請確定您的 SQL Server 升級為使用特定的標記。 新的容器現在會使用與您現有的 SQL Server 資料的新版本的 SQL Server。

   > [!IMPORTANT]
   > RC1 des、desx、rc2 和 GA 之間目前只支援升級。

1. 請確認您的資料庫和新的容器中的資料。

1. （選擇性） 移除的舊容器`docker rm`。

## <a id="troubleshooting"></a> 疑難排解

下列各節提供在容器中執行 SQL Server 的疑難排解建議。

### <a name="docker-command-errors"></a>Docker 命令發生錯誤

如果遇到任何錯誤`docker`命令，請確定 docker 服務正在執行，並嘗試以更高權限執行。

例如，在 Linux 上，您可能會收到下列錯誤時執行`docker`命令：

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果您在 Linux 上收到這個錯誤，請嘗試執行相同的命令前面加上`sudo`。 如果失敗，請確認 docker 服務正在執行，而且必要時加以啟動。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 中，確認您啟動 PowerShell 或以系統管理員身分您命令提示字元。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器啟動錯誤

如果 SQL Server 容器無法執行，請嘗試下列測試：

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

- 請檢查是否有任何錯誤訊息，從容器。

    ```bash
    docker logs e69e056c702d
    ```

- 請確定您符合指定的最小記憶體和磁碟需求[必要條件](quickstart-install-connect-docker.md#requirements)快速入門文章一節。

- 如果您使用任何容器管理軟體，請確定它支援以 root 身分執行的容器處理序。 以 root 身分執行，例如出現 sqlservr 程序，容器中的執行。

- 檢閱[SQL Server 安裝程式和錯誤記錄檔](#errorlogs)。

### <a name="enable-dump-captures"></a>啟用傾印擷取

如果 SQL Server 處理序無法在容器內，您應該建立新的容器，使用**SYS_PTRACE**啟用。 這會將追蹤處理序，也就是建立在例外狀況的傾印檔案所需的 Linux 功能。 傾印檔案可供支援，以協助疑難排解問題。 下列 docker run 命令可讓這項功能。

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

### <a name="sql-server-connection-failures"></a>SQL Server 連線失敗

如果您無法連線到容器中執行的 SQL Server 執行個體，請嘗試下列測試：

- 請確定您的 SQL Server 容器正在執行來看看**狀態**資料行`docker ps -a`輸出。 如果沒有，請使用`docker start <Container ID>`啟動它。

- 如果您對應至非預設的主機連接埠 (不是 1433)，請確定您在連接字串中指定的連接埠。 您可以看到您的連接埠對應中**連接埠**資料行`docker ps -a`輸出。 例如，下列命令會連接到 sqlcmd 接聽通訊埠 1401容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果您使用`docker run`的現有對應的資料磁碟區或資料磁碟區容器，使用 SQL Server 會忽略值`MSSQL_SA_PASSWORD`。 相反地，都可以從 SQL Server 中的資料的資料量或資料磁碟區容器中使用預先設定的 SA 使用者密碼。 確認您要使用的資料，您會將附加至相關聯的 SA 密碼。

- 檢閱[SQL Server 安裝程式和錯誤記錄檔](#errorlogs)。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性群組

如果您使用 Docker 與 SQL Server 可用性群組，有兩個額外的需求。

- 將對應的連接埠，可用於複本通訊 （預設值 5022）。 例如，指定`-p 5022:5022`一部分您`docker run`命令。

- 明確地設定在容器主機名稱`-h YOURHOSTNAME`參數`docker run`命令。 設定您的可用性群組時，會使用此主機名稱。 如果您未指定它與`-h`，它會預設為容器識別碼。

### <a id="errorlogs"></a> SQL Server 安裝程式和錯誤記錄檔

您可以查看 SQL Server 安裝程式和錯誤記錄檔 **/var/opt/mssql/log**。 如果容器不在執行中，第一次啟動容器。 若要檢查記錄檔，然後使用互動式命令提示字元。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

從您容器內的 bash 工作階段，請執行下列命令：

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 如果掛接主機目錄來 **/var/opt/mssql**當您建立您的容器，您可以改為查看**記錄**主機上的對應路徑的子目錄。

## <a name="next-steps"></a>後續步驟

開始使用 Docker 上的 SQL Server 2017 容器映像經過[快速入門](quickstart-install-connect-docker.md)。

此外，請參閱[mssql-docker GitHub 存放庫](https://github.com/Microsoft/mssql-docker)的資源、 意見反應和已知的問題。

[探索 SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)
