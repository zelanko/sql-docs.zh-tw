---
title: 設定 Linux 上 SQL Server 的使用狀況與診斷資料收集
description: 描述如何收集和設定 Linux 上的 SQL Server 客戶使用狀況和診斷資料。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d7fc5a14a9da000b69db804a5439fb62985f59b8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558533"
---
# <a name="configure-usage--diagnostic-data-collection-for-sql-server-on-linux"></a>設定 Linux 上 SQL Server 的使用狀況與診斷資料收集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

根據預設，Microsoft SQL Server 會收集客戶如何使用應用程式的相關資訊。 具體來說，SQL Server 會收集有關安裝體驗、使用情況和效能的相關資訊。 這些資訊可協助 Microsoft 改善產品，以進一步滿足客戶需求。 例如，Microsoft 會收集客戶所遇到之錯誤代碼的相關資訊，以便修正相關錯誤、改善如何使用 SQL Server 的相關文件，以及判斷是否應將功能加入到產品中以滿足客戶。

本文件提供關於所收集的資訊種類、如何設定 Linux 上的 Microsoft SQL Server，以將所收集資訊傳送給 Microsoft 的詳細資料。 SQL Server 2017 包含隱私權聲明，其中說明我們會 (與不會) 向使用者收集的資訊。 如需詳細資訊，請參閱[隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)。

具體來說，Microsoft 不會透過此機制傳送下列類型的資訊：

- 使用者資料表內的任何值
- 任何登入認證或其他驗證資訊
- 個人識別資訊 (PII)

SQL Server 2017 一律會收集並傳送與安裝程序中安裝體驗相關的資訊，以便我們能夠快速找出並修正客戶所遇到的任何安裝問題。 SQL Server 2017 可以透過 **mssql-conf** 設定為不傳送資訊 (針對每個伺服器執行個體) 給 Microsoft。 mssql-conf 是一個設定指令碼，會使用適用於 Red Hat Enterprise Linux、SUSE Linux Enterprise Server 和 Ubuntu 的 SQL Server 2017 進行安裝。

> [!NOTE]
> 您僅可在付費版本的 SQL Server 中停用將資訊傳送給 Microsoft 的功能。

## <a name="disable-usage-and-diagnostic-data-collection"></a>停用使用方式和診斷資料收集

此選項可讓您變更 SQL Server 是否要將使用方式和診斷資料收集傳送給 Microsoft。 根據預設，此值設為 True。 若要變更此值，請執行下列命令：

> [!IMPORTANT]
> 您不能針對免費的 SQL Server 版本 (Express 和 Developer) 關閉使用方式和診斷資料收集。

### <a name="on-red-hat-suse-and-ubuntu"></a>在 Red Hat、SUSE 和 Ubuntu 上

1. 使用 **telemetry.customerfeedback** 的 **set** 命令，以 root 身分執行 mssql-conf 指令碼。 下列範例會藉由指定 **False** 來關閉使用方式和診斷資料收集。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>在 Docker 上
若要停用 Docker 上的使用方式和診斷資料收集，您必須讓 Docker [保存您的資料](sql-server-linux-configure-docker.md)。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 在主機目錄中新增具有 `mssql.conf` 和 `[telemetry]` 這二行的 `customerfeedback = false` 檔案：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 執行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 在主機目錄中新增具有 `mssql.conf` 和 `[telemetry]` 這二行的 `customerfeedback = false` 檔案：

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 執行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>Linux 上 SQL Server 使用方式和診斷資料收集的本機稽核

Microsoft SQL Server 2017 包含一些啟用網際網路的功能，而這些功能可能會收集您電腦或裝置的相關資訊 (「標準電腦資訊」) 並將此資訊傳送至 Microsoft。 SQL Server 使用方式和診斷資料收集的本機稽核元件，會將服務收集的資料寫入指定資料夾，代表將傳送給 Microsoft 的資料 (記錄)。 本機稽核的目的是要讓客戶看到 Microsoft 以此功能收集的所有資料，以用於相容性、法規或隱私權驗證的理由。

在 Linux 上的 SQL Server 中，本機稽核可以在 SQL Server Database Engine 和 Analysis Services (SSAS) 的執行個體層級設定。 其他 SQL Server 元件和 SQL Server 工具沒有使用方式和診斷資料收集的本機稽核功能。

### <a name="enable-local-audit"></a>啟用本機稽核

此選項可啟用本機稽核，並可讓您設定要建立本機稽核記錄的目錄。

1. 為新的本機稽核記錄建立目標目錄。 下列範例會建立新的 **/tmp/audit** 目錄：

   ```bash
   sudo mkdir /tmp/audit
   ```

2. 將目錄的擁有者和群組變更為 **mssql** 使用者：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. 使用 **telemetry.userrequestedlocalauditdirectory** 的 **set** 命令，以 root 身分執行 mssql-conf 指令碼：

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>在 Docker 上
若要在 Docker 上啟用本機稽核，您必須讓 Docker [保存您的資料](sql-server-linux-configure-docker.md)。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 新本機稽核記錄的目標目錄會位於容器中。 在您電腦上的主機目錄中，為新的本機稽核記錄建立目標目錄。 下列範例會建立新的 **/audit** 目錄：

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 在主機目錄中新增具有 `mssql.conf` 和 `[telemetry]` 這二行的 `userrequestedlocalauditdirectory = <host directory>/audit` 檔案：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 執行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. 新本機稽核記錄的目標目錄會位於容器中。 在您電腦上的主機目錄中，為新的本機稽核記錄建立目標目錄。 下列範例會建立新的 **/audit** 目錄：

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 在主機目錄中新增具有 `mssql.conf` 和 `[telemetry]` 這二行的 `userrequestedlocalauditdirectory = <host directory>/audit` 檔案：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 執行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-GA-ubuntu-16.04
   ```

::: moniker-end

## <a name="next-steps"></a>後續步驟

如需 Linux 上的 SQL Server 詳細資訊，請參閱 [Linux 上的 SQL Server 概觀](sql-server-linux-overview.md)。
