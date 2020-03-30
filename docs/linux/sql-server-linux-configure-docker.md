---
title: Docker 上 SQL Server 的設定選項
description: 探索在 Docker 中使用 SQL Server 2017 和 2019 容器映像並與其互動的不同方式。 這包括保存資料、複製檔案和疑難排解。
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.date: 01/08/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 82737f18-f5d6-4dce-a255-688889fdde69
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e97f535dedd2b6ee25abfc886d1f08272697c549
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287502"
---
# <a name="configure-sql-server-container-images-on-docker"></a>在 Docker 上設定 SQL Server 容器映像

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章說明如何以 Docker 設定和使用 [mssql-server-linux 容器映像](https://hub.docker.com/_/microsoft-mssql-server) \(英文\)。 

如需了解其他部署案例，請參閱：

- [Windows](../database-engine/install-windows/install-sql-server.md)
- [Linux](../linux/sql-server-linux-setup.md)
- [Kubernetes - 巨量資料叢集](../big-data-cluster/deploy-get-started.md)

此映像包含以 Ubuntu 16.04 為基礎，在 Linux 上執行的 SQL Server。 您可於適用於 Mac/Windows 的 Docker 上將其與 Docker 引擎 1.8 以上版本搭配使用。

> [!NOTE]
> 此文章特別著重於 mssql-server-linux 映像的使用。 Windows 映像並未涵蓋其中，但您可以在 [mssql-server-windows Docker Hub 頁面](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/) \(英文\) 上深入了解。

> [!IMPORTANT]
> 為產品使用案例選擇執行 SQL Server 容器之前，請檢閱我們的 [SQL Server 容器支援原則](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) \(部分機器翻譯\) 以確定您是以支援的設定執行。

這段 6 分鐘的影片會介紹如何在容器上執行 SQL Server：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2019-in-Containers/player?WT.mc_id=dataexposed-c9-niner]


## <a name="pull-and-run-the-container-image"></a>提取及執行容器映像

若要提取並執行適用於 SQL Server 2017 和 SQL Server 2019 的 Docker 容器映像，請遵循下列快速入門中的先決條件和步驟：

- [以 Docker 執行 SQL Server 2017 容器映像](quickstart-install-connect-docker.md?view=sql-server-2017)
- [以 Docker 執行 SQL Server 2019 容器映像](quickstart-install-connect-docker.md?view=sql-server-ver15)

本設定文章將在下列各節中提供其他使用案例。

<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="run-rhel-based-container-images"></a><a id="rhel"></a> 執行 RHEL 型容器映像

適用於 SQL Server Linux 容器映像的文件都指向 Ubuntu 型容器。 從 SQL Server 2019 開始，您可以使用 Red Hat Enterprise Linux (RHEL) 型容器。 在所有 Docker 命令中，將容器存放庫從 **mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04** 變更為 **mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8**。

例如，下列命令會為使用 RHEL 8 的 SQL Server 2019 容器提取累積更新 1：

```bash
sudo docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

```PowerShell
docker pull mcr.microsoft.com/mssql/rhel/server:2019-CU1-rhel-8
```

::: moniker-end

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="run-production-container-images"></a><a id="production"></a> 執行生產容器映像

上一節中的快速入門會從 Docker Hub 執行免費的 SQL Server 開發人員版本。 如果您想要執行生產容器映像 (例如 Enterprise、Standard 或 Web 版本)，大部分的資訊仍然適用。 但仍有一些此處概述的差異。

- 如果您具備有效授權，則只能在生產環境中使用 SQL Server。 您可以在[此處](https://go.microsoft.com/fwlink/?linkid=857693)取得免費的 SQL Server Express 生產授權。 SQL Server Standard 和 Enterprise Edition 授權可透過 [Microsoft 大量授權](https://www.microsoft.com/licensing/default.aspx)取得。


- 開發人員容器映像也可以設定為執行生產版本。 使用下列步驟來執行生產版本：

在[快速入門](quickstart-install-connect-docker.md)中檢閱需求和執行程序。 您必須使用 **MSSQL_PID** 環境變數來指定生產版本。 下列範例示範如何針對 Enterprise Edition 執行最新的 SQL Server 2017 容器映像：

```bash
docker run --name sqlenterprise \
      -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
      -e 'MSSQL_PID=Enterprise' -p 1433:1433 \
      -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run --name sqlenterprise `
      -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
      -e "MSSQL_PID=Enterprise" -p 1433:1433 `
      -d "mcr.microsoft.com/mssql/server:2017-latest"
```

> [!IMPORTANT]
> 透過將值 **Y** 傳遞至環境變數 **ACCEPT_EULA** 並將版本值傳遞至 **MSSQL_PID**，來表示您目前具備您想要使用之 SQL Server 版本的有效授權。 您也同意使用在 Docker 容器映像中執行的 SQL Server 軟體將受到 SQL Server 授權的條款所規範。

> [!NOTE]
> 如需 **MSSQL_PID** 的完整可能值清單，請參閱[在 Linux 上使用環境變數設定 SQL Server 設定](sql-server-linux-configure-environment-variables.md)。

::: moniker-end

## <a name="connect-and-query"></a>連線和查詢

您可以從容器外部或從容器內部，連線和查詢容器中的 SQL Server。 下列各節將說明這兩種案例。 

### <a name="tools-outside-the-container"></a>容器外部的工具

您可以從支援 SQL 連線的任何外部 Linux、Windows 或 macOS 工具連線到 Docker 機器上的 SQL Server 執行個體。 一些常用工具包括：

- [sqlcmd](sql-server-linux-setup-tools.md)
- [Visual Studio Code](sql-server-linux-develop-use-vscode.md)
- [Windows 上的 SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)

下列範例會使用 **sqlcmd** 來連線到在 Docker 容器中執行的 SQL Server。 連接字串中的 IP 位址是執行容器之主機電腦的 IP 位址。

```bash
sqlcmd -S 10.3.2.4 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4 -U SA -P "<YourPassword>"
```

如果您對應的主機連接埠不是預設的 **1433**，將該連接埠新增至連接字串。 例如，如果您在 `docker run` 命令中指定了 `-p 1400:1433`，則要明確地指定連接埠 1400 來連線。

```bash
sqlcmd -S 10.3.2.4,1400 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1400 -U SA -P "<YourPassword>"
```

### <a name="tools-inside-the-container"></a>容器內部的工具

從 SQL Server 2017 開始，容器映像會包含 [SQL Server 命令列工具](sql-server-linux-setup-tools.md)。 如果您使用互動式命令提示字元來附加至映像，則可在本機執行這些工具。

1. 使用 `docker exec -it` 命令在您執行的容器中啟動互動式 Bash 殼層。 在下列範例中，`e69e056c702d` 是容器識別碼。

    ```bash
    docker exec -it e69e056c702d "bash"
    ```

    > [!TIP]
    > 您不一定要指定整個容器識別碼。您只需指定足夠的字元來唯一識別它。 因此，在此範例中，使用 `e6` 或 `e69` 可能就已足夠，而不需使用完整識別碼。

2. 進入容器後，以 sqlcmd 進行本機連線。 請注意，sqlcmd 預設不在路徑中，因此您必須指定完整路徑。

    ```bash
    /opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P '<YourPassword>'
    ```

3. 完成使用 sqlcmd 時，輸入 `exit`。

4. 完成使用互動式命令提示字元時，輸入 `exit`。 結束互動式 Bash 殼層後，容器會繼續執行。

## <a name="run-multiple-sql-server-containers"></a>執行多個 SQL Server 容器

Docker 提供一種方法，可在相同的主機電腦上執行多個 SQL Server 容器。 請針對相同主機上需要多個 SQL Server 執行個體的案例使用此方法。 每個容器都必須在不同的連接埠上公開其本身。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

下列範例會建立兩個 SQL Server 2017 容器，並將它們對應至主機電腦上的連接埠 **1401** 和 **1402**。

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

下列範例會建立兩個 SQL Server 2019 容器，並將容器對應至主機電腦上的連接埠 **1401** 和 **1402**。

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1402:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

現在，有兩個在不同容器中執行的 SQL Server 執行個體。 用戶端可以使用 Docker 主機的 IP 位址和容器的連接埠號碼，來連線到每個 SQL Server 執行個體。

```bash
sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
sqlcmd -S 10.3.2.4,1402 -U SA -P '<YourPassword>'
```

```PowerShell
sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
sqlcmd -S 10.3.2.4,1402 -U SA -P "<YourPassword>"
```

## <a name="create-a-customized-container"></a><a id="customcontainer"></a> 建立自訂容器

您能夠建立自己的 [Dockerfile](https://docs.docker.com/engine/reference/builder/#usage) \(英文\)，來建立自訂的 SQL Server 容器。 如需詳細資訊，請參閱[結合 SQL Server 和 Node 應用程式的示範](https://github.com/twright-msft/mssql-node-docker-demo-app) \(英文\)。 如果您建立自己的 Dockerfile，請留意前景程序，因為此程序會控制容器的生命週期。 如果結束，容器將會關閉。 例如，如果您想要執行指令碼並啟動 SQL Server，請確定 SQL Server 程序是最右邊的命令。 所有其他命令都會在背景執行。 下列命令會在 Dockerfile 的內部進行示範：

```bash
/usr/src/app/do-my-sql-commands.sh & /opt/mssql/bin/sqlservr
```

如果您反轉上一個範例中的命令，容器就會在 do-my-sql-commands.sh 指令碼完成時關閉。

## <a name="persist-your-data"></a><a id="persist"></a> 保存您的資料

您的 SQL Server 設定變更和資料庫檔案都會保存於容器中，即使您使用 `docker stop` 和 `docker start` 來將容器重新啟動也一樣。 不過，如果您使用 `docker rm` 來移除容器，則會刪除容器中的所有項目，包括 SQL Server 和您的資料庫。 下一節將說明如何使用**資料磁碟區**來保存您的資料庫檔案，即使已刪除相關聯的容器也一樣。

> [!IMPORTANT]
> 針對 SQL Server，請務必瞭解 Docker 中的資料持續性。 除了本節的討論，另請參閱 Docker 文件，以了解[如何管理 Docker 容器中的資料](https://docs.docker.com/engine/tutorials/dockervolumes/) \(英文\)。

### <a name="mount-a-host-directory-as-data-volume"></a>裝載主機目錄作為資料磁碟區

第一個選項是在主機上裝載目錄作為容器中的資料磁碟區。 若要執行此動作，請使用 `docker run` 命令搭配 `-v <host directory>:/var/opt/mssql` 旗標。 這可讓您在容器執行之間還原資料。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>/data:/var/opt/mssql/data -v <host directory>/log:/var/opt/mssql/log -v <host directory>/secrets:/var/opt/mssql/secrets -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

此技術也可讓您在 Docker 外部共用和檢視主機上的檔案。

> [!IMPORTANT]
> **Windows 上的 Docker** 的主機磁碟區對應，目前不支援對應完整 `/var/opt/mssql` 目錄。 不過，您可以將子目錄 (例如 `/var/opt/mssql/data`) 對應到您的主機電腦。

> [!IMPORTANT]
> 目前不支援使用 Linux 上的 SQL Server 映像，針對 **Mac 上的 Docker** 進行主機磁碟區對應。 請改用資料磁碟區容器。 此限制是 `/var/opt/mssql` 目錄特有的。 從裝載的目錄讀取可以正常運作。 例如，您可以在 Mac 上使用 -v 來裝載主機目錄，並從位於主機的 .bak 檔案還原備份。

### <a name="use-data-volume-containers"></a>使用資料磁碟區容器

第二個選項是使用資料磁碟區容器。 您可以使用 `-v` 參數來指定磁碟區名稱而非主機目錄，藉以建立資料磁碟區容器。 下列範例會建立名為 **sqlvolume** 的共用資料磁碟區。

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v sqlvolume:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

> [!NOTE]
> 這項在執行命令中隱含建立資料磁碟區的技術無法與舊版 Docker 搭配運作。 在此情況下，請使用 Docker 文件中概述的明確步驟，[建立和裝載資料磁碟區容器](https://docs.docker.com/engine/tutorials/dockervolumes/#creating-and-mounting-a-data-volume-container) \(英文\)。

即使您停止並移除此容器，資料磁碟區仍會保存。 您可以使用 `docker volume ls` 命令來檢視它。

```bash
docker volume ls
```

如果您接著使用相同磁碟區名稱來建立另一個容器，新容器就會使用該磁碟區中所含的相同 SQL Server 資料。

若要移除資料磁碟區容器，請使用 `docker volume rm` 命令。

> [!WARNING]
> 如果您刪除資料磁碟區容器，則會「永久」  刪除容器中的所有 SQL Server 資料。

### <a name="backup-and-restore"></a>備份與還原

除了這些容器技術，您也可以使用標準的 SQL Server 備份和還原技術。 您可以使用備份檔案來保護資料，或將資料移至另一個 SQL Server 執行個體。 如需詳細資訊，請參閱[備份與還原 Linux 上的 SQL Server 資料庫](sql-server-linux-backup-and-restore-database.md)。

> [!WARNING]
> 如果您建立備份，請務必在容器外部建立或複製備份檔案。 否則，如果移除容器，也會一併刪除備份檔案。

## <a name="execute-commands-in-a-container"></a>在容器中執行命令

如果您有執行中的容器，就可以在該容器內，從主機終端機執行命令。

若要取得容器識別碼，請執行：

```bash
docker ps
```

若要在容器中啟動 Bash 終端機，請執行：

```bash
docker exec -it <Container ID> /bin/bash
```

現在您可以執行命令，就像是在容器內部的終端機中執行它們一樣。 完成後，鍵入 `exit`。 這會在互動式命令工作階段中結束，但您的容器會繼續執行。

## <a name="copy-files-from-a-container"></a>從容器複製檔案

若要將檔案複製到容器外部，請使用下列命令：

```bash
docker cp <Container ID>:<Container path> <host path>
```

**範例︰**

```bash
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog /tmp/errorlog
```

```PowerShell
docker cp d6b75213ef80:/var/opt/mssql/log/errorlog C:\Temp\errorlog
```

## <a name="copy-files-into-a-container"></a>將檔案複製到容器

若要將檔案複製到容器內部，請使用下列命令：

```bash
docker cp <Host path> <Container ID>:<Container path>
```

**範例︰**

```bash
docker cp /tmp/mydb.mdf d6b75213ef80:/var/opt/mssql/data
```

```PowerShell
docker cp C:\Temp\mydb.mdf d6b75213ef80:/var/opt/mssql/data
```
## <a name="configure-the-timezone"></a><a id="tz"></a> 設定時區

若要在具有特定時區的 Linux 容器中執行 SQL Server，請設定 `TZ` 環境變數。 若要尋找正確的時區值，請從 Linux Bash 提示執行 `tzselect` 命令：

```bash
tzselect
```

選取時區之後，`tzselect` 會顯示類似下列的輸出：

```bash
The following information has been given:

        United States
        Pacific

Therefore TZ='America/Los_Angeles' will be used.
```

您可以使用此資訊，在 Linux 容器中設定相同的環境變數。 下列範例示範如何在 `Americas/Los_Angeles` 時區的容器中執行 SQL Server：

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
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

```PowerShell
sudo docker run -e 'ACCEPT_EULA=Y' -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" `
   -p 1433:1433 --name sql1 `
   -e "TZ=America/Los_Angeles" `
   -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```
::: moniker-end

## <a name="run-a-specific-sql-server-container-image"></a><a id="tags"></a> 執行特定的 SQL Server 容器映像

在某些情況下，您可能不想使用最新的 SQL Server 容器映像。 若要執行特定的 SQL Server 容器映像，請使用下列步驟：

1. 識別您想要使用之版本的 Docker **標記**。 若要檢視所有可用的標記，請參閱 [mssql-server-linux Docker Hub 頁面](https://hub.docker.com/_/microsoft-mssql-server) \(英文\)。

2. 使用標記來提取 SQL Server 容器映像。 例如，若要提取 RC1 映像，請以 `rc1` 取代下列命令中的 `<image_tag>`。

   ```bash
   docker pull mcr.microsoft.com/mssql/server:<image_tag>
   ```

3. 若要使用該映像來執行新容器，則在 `docker run` 命令中指定標記名稱。 在下列命令中，以您想要執行的版本取代 `<image_tag>`。

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d mcr.microsoft.com/mssql/server:<image_tag>
   ```

這些步驟也可以用來將現有的容器降級。 例如，您可能想要復原或降級執行中的容器，以進行疑難排解或測試。 若要將執行中的容器降級，您必須使用適用於資料資料夾的持續性技術。 遵循[升級小節](#upgrade)中概述的相同步驟，但在執行新容器時指定較舊版本的標記名稱。

## <a name="check-the-container-version"></a><a id="version"></a> 檢查容器版本

如果您想要知道執行中 Docker 容器內的 SQL Server 版本，請執行下列命令來顯示它。 以目標容器識別碼或名稱取代 `<Container ID or name>`。 以用來進行 SA 登入的 SQL Server 密碼取代 `<YourStrong!Passw0rd>`。

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

您也可以識別目標 Docker 容器映像的 SQL Server 版本和組建編號。 下列命令會顯示 **mcr.microsoft.com/mssql/server:2017-latest** 映像的 SQL Server 版本和組建資訊。 其執行方式是使用環境變數 **PAL_PROGRAM_INFO=1** 來執行新容器。 產生的容器會立即結束，而且 `docker rm` 命令會移除它。

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

先前的命令會顯示類似下列輸出的版本資訊：

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

## <a name="upgrade-sql-server-in-containers"></a><a id="upgrade"></a> 在容器中升級 SQL Server

若要使用 Docker 來升級容器映像，請先識別適用於您升級之版本的標記。 使用 `docker pull` 命令，從登錄中提取此版本：

```bash
docker pull mcr.microsoft.com/mssql/server:<image_tag>
```

這會更新您所建立之任何新容器的 SQL Server 映像，但不會更新任何執行中容器內的 SQL Server。 若要執行此動作，您必須使用最新的 SQL Server 容器映像來建立新容器，並將您的資料移轉至該新容器。

1. 請確定您會針對現有的 SQL Server 容器使用其中一種[資料持續性技術](#persist)。 這可讓您使用相同的資料來啟動新容器。

1. 使用 `docker stop` 命令來停止 SQL Server 容器。

1. 使用 `docker run` 來建立新的 SQL Server 容器，並指定對應的主機目錄或資料磁碟區容器。 請務必針對您的 SQL Server 升級使用特定的標記。 新容器現在會使用新的 SQL Server 版本搭配您現有的 SQL Server 資料。

   > [!IMPORTANT]
   > 目前僅支援 RC1、RC2 和 GA 之間的升級。

1. 在新容器中確認您的資料庫和資料。

1. (選擇性) 使用 `docker rm` 來移除舊容器。

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

docker exec 進入容器。
```bash
docker exec -it sql1 bash
```

執行 `whoami`，傳回正在容器內執行的使用者。

```bash
whoami
```

## <a name="run-container-as-a-different-non-root-user-on-the-host"></a><a id="nonrootuser"></a> 以主機上不同的非根使用者身分執行容器

若要以不同的非根使用者執行 SQL Server 容器，請將 -u 旗標新增至 docker run 命令。 非根容器包含限制，除非磁碟區是掛接到非根使用者可存取的 '/var/opt/mssql'，否則必須作為根群組的一部分執行。 根群組不會授與任何額外的根權限給非根使用者。

**以 UID 4000 的使用者執行**

您可以使用自訂 UID 來啟動 SQL Server。 例如，以下命令會以 UID 4000 來啟動 SQL Server：
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u 4000:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

> [!Warning]
> 請確定 SQL Server 容器具有像是 'mssql' 或 'root' 等具名使用者，否則 SQLCMD 將無法在容器內執行。 您可以在容器內執行 `whoami` 來檢查 SQL Server 容器是否正以具名使用者的身分執行。

**以根使用者身分執行非根容器**

若需要，您可以根使用者的身分執行非根容器。 這也會自動授與完整的檔案權限給容器，因為這是較高的權限。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -u 0:0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**以您主機電腦上的使用者身分執行**

您可以透過下列命令，使用主機電腦上現有的使用者來啟動 SQL Server：
```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u $(id -u myusername):0 -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

**以不同的使用者和群組執行**

您可以使用自訂使用者和群組來啟動 SQL Server。 在此範例中，已掛接磁碟區具備針對主機電腦上使用者或群組設定的權限。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" --cap-add SYS_PTRACE -u (id -u myusername):(id -g myusername) -v /path/to/mssql:/var/opt/mssql -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="configure-persistent-storage-permissions-for-non-root-containers"></a><a id="storagepermissions"></a> 為非根容器設定永續性儲存體權限

若要允許非根使用者存取已掛接磁碟區上的 DB 檔案，請確認您執行容器的使用者/群組可接觸永續性檔案儲存體。  

您可以使用此命令來取得資料庫檔案目前的擁有權。

```bash
ls -ll <database file dir>
```

若 SQL Server 無法存取保存的資料庫檔案，請執行下列其中一個命令。

**授與根群組對 DB 檔案的讀寫存取權**

授與根群組存取下列目錄的權限，讓非根 SQL Server 容器能夠存取資料庫檔案。

```bash
chgrp -R 0 <database file dir>
chmod -R g=u <database file dir>
```

**將非根使用者設為檔案的擁有者。**

這可以是預設的非根使用者，或是任何其他您想要指定的非根使用者。 在此範例中，我們會將 UID 10001 設為非根使用者。

```bash
chown -R 10001:0 <database file dir>
```

## <a name="change-the-default-file-location"></a><a id="changefilelocation"></a> 變更預設檔案位置

新增 `MSSQL_DATA_DIR` 變數來在您 `docker run` 命令中變更您的資料目錄，然後將磁碟區掛接到您容器使用者可存取的該位置。

```bash
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=MyStrongPassword" -e "MSSQL_DATA_DIR=/my/file/path" -v /my/host/path:/my/file/path -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest
```

## <a name="troubleshooting"></a><a id="troubleshooting"></a> 疑難排解

下列各節提供在容器中執行 SQL Server 的疑難排解建議。

### <a name="docker-command-errors"></a>Docker 命令錯誤

如果您收到有關任何 `docker` 命令的錯誤，請確定 Docker 服務正在執行，並嘗試以提升的權限執行。

例如，在 Linux 上，您可能會在執行 `docker` 命令時收到下列錯誤：

```
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
```

如果您在 Linux 上收到此錯誤，請嘗試執行前面已加上 `sudo` 的相同命令。 如果該動作失敗，確認 Docker 服務正在執行，並視需要啟動它。

```bash
sudo systemctl status docker
sudo systemctl start docker
```

在 Windows 上，確認您是以系統管理員身分啟動 PowerShell 或命令提示字元。

### <a name="sql-server-container-startup-errors"></a>SQL Server 容器啟動錯誤

如果 SQL Server 容器無法執行，請嘗試下列測試：

- 如果您收到如下的錯誤： **「無法在網路橋接器上建立端點 CONTAINER_NAME。啟動 Proxy 時發生錯誤: listen tcp 0.0.0.0:1433 bind: 位址已在使用中。」** ，則您正嘗試將容器連接埠 1433 對應到已在使用中的連接埠。 如果您在主機電腦上本機執行 SQL Server，就會發生這種情況。 如果您啟動兩個 SQL Server 容器，並嘗試將它們都對應到相同的主機連接埠，也可能發生此問題。 如果發生這種情況，請使用 `-p` 參數，將容器連接埠 1433 對應到不同的主機連接埠。 例如： 

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
docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

```PowerShell
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1400:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04`.
```

::: moniker-end

- 如果在嘗試啟動容器時，收到如下的錯誤： **「嘗試在 unix:///var/run/docker.sock 上連線到 Docker daemon 通訊端時發生權限遭拒:取得 http://%2Fvar%2Frun%2Fdocker.sock/v1.30tdout=1&tail=all: dial unix /var/run/docker.sock: connect: 權限遭拒」** ，然後將您的使用者新增至 Ubuntu 中的 Docker 群組。 接著登出並重新登入，因為此變更將影響新的工作階段。 

   ```bash
    usermod -aG docker $USER
   ```
- 檢查以查看是否有任何來自容器的錯誤訊息。

    ```bash
    docker logs e69e056c702d
    ```

- 確定您符合快速入門文章之[先決條件](quickstart-install-connect-docker.md#requirements)一節中所指定的最小記憶體和磁碟需求。

- 如果您使用任何容器管理軟體，請確定它支援以 root 身分執行容器程序。 容器中的 sqlservr 程序會以 root 身分執行。

- 檢閱 [SQL Server 設定和錯誤記錄檔](#errorlogs)。

### <a name="enable-dump-captures"></a>啟用傾印擷取

如果 SQL Server 程序在容器內部失敗，則您應該建立已啟用 **SYS_PTRACE** 的新容器。 這會新增 Linux 功能來追蹤程序，其在例外狀況上建立傾印檔案時是必要的。 支援人員可以使用傾印檔案來協助進行問題的疑難排解。 下列 docker run 命令會啟用此功能。

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2017-latest
```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

```bash
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -e "MSSQL_PID=Developer" --cap-add SYS_PTRACE -p 1401:1433 -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
```

::: moniker-end

### <a name="sql-server-connection-failures"></a>SQL Server 連線失敗

如果您無法連線到在容器中執行的 SQL Server 執行個體，請嘗試下列測試：

- 查看 `docker ps -a` 輸出的 [狀態]  欄，以確定您的 SQL Server 容器正在執行。 如果沒有，則使用 `docker start <Container ID>` 來啟動它。

- 如果您已對應到非預設的主機連接埠 (不是 1433)，請確定您會在連接字串中指定該連接埠。 您可以在 `docker ps -a` 輸出的 [連接埠]  欄中看到連接埠對應。 例如，下列命令會將 sqlcmd 連線到在連接埠 1401 上接聽的容器：

    ```bash
    sqlcmd -S 10.3.2.4,1401 -U SA -P '<YourPassword>'
    ```

    ```PowerShell
    sqlcmd -S 10.3.2.4,1401 -U SA -P "<YourPassword>"
    ```

- 如果您搭配現有的對應資料磁碟區或資料磁碟區容器使用 `docker run`，SQL Server 就會忽略 `MSSQL_SA_PASSWORD` 的值。 相反地，會從資料磁碟區或資料磁碟區容器中的 SQL Server 資料使用預先設定的 SA 使用者密碼。 確認您使用的 SA 密碼會與您要附加的資料相關聯。

- 檢閱 [SQL Server 設定和錯誤記錄檔](#errorlogs)。

### <a name="sql-server-availability-groups"></a>SQL Server 可用性群組

如果您使用 Docker 搭配 SQL Server 可用性群組，則有兩個額外的需求。

- 對應用於複本通訊的連接埠 (預設值為 5022)。 例如，指定 `-p 5022:5022` 作為 `docker run` 命令的一部分。

- 使用 `docker run` 命令的 `-h YOURHOSTNAME` 參數，明確設定容器主機名稱。 當您設定可用性群組時，會使用此主機名稱。 如果您未使用 `-h` 來指定它，則會預設為容器識別碼。

### <a name="sql-server-setup-and-error-logs"></a><a id="errorlogs"></a> SQL Server 設定和錯誤記錄檔

您可以在 **/var/opt/mssql/log** 中查看 SQL Server 設定和錯誤記錄檔。 如果容器並未執行，請先啟動容器。 接著，使用互動式命令提示字元來檢查記錄。

```bash
docker start e69e056c702d
docker exec -it e69e056c702d "bash"
```

從您容器內部的 Bash 工作階段，執行下列命令：

```bash
cd /var/opt/mssql/log
cat setup*.log
cat errorlog
```

> [!TIP]
> 如果您已在建立容器時將主機目錄裝載至 **/var/opt/mssql**，則可改為查看主機中對應路徑上的**記錄**子目錄。

## <a name="next-steps"></a>後續步驟

透過此[快速入門](quickstart-install-connect-docker.md)，開始使用 Docker 上的 SQL Server 2017 容器映像。

另請參閱 [mssql-docker GitHub 存放庫](https://github.com/Microsoft/mssql-docker) \(英文\)，以取得資源、意見反應和已知問題。

[探索 SQL Server 容器的高可用性](sql-server-linux-container-ha-overview.md)
