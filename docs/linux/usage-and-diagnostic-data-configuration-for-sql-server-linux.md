---
title: 在 Linux 上設定使用量和適用於 SQL Server 的診斷資料收集
description: 描述如何 SQL Server 客戶的使用量和診斷資料收集與 Linux 上設定。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ab0b00013c09c5328ad711307558e67adc784d05
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834544"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-on-linux"></a>在 Linux 上設定使用量和適用於 SQL Server 的診斷資料收集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

根據預設，Microsoft SQL Server 會收集客戶如何使用應用程式的相關資訊。 具體來說，SQL Server 會收集有關安裝體驗、使用情況和效能的相關資訊。 這些資訊可協助 Microsoft 改善產品，以進一步滿足客戶需求。 例如，Microsoft 會收集客戶所遇到之錯誤代碼的相關資訊，以便修正相關錯誤、改善如何使用 SQL Server 的相關文件，以及判斷是否應將功能加入到產品中以滿足客戶。

本文件提供有關收集何種資訊，以及有關如何設定傳送也收集 Linux 上的 Microsoft SQL Server 詳細資料給 Microsoft 的資訊。 SQL Server 2017 包含隱私權聲明，說明我們執行，並不會從使用者收集哪些資訊。 如需詳細資訊，請參閱 <<c0> [ 隱私權聲明](https://go.microsoft.com/fwlink/?LinkID=868444)。

具體來說，Microsoft 不會透過此機制傳送下列類型的資訊：

- 使用者資料表內的任何值
- 任何登入認證或其他驗證資訊
- 個人識別資訊 (PII)

SQL Server 2017 一律會收集並傳送與安裝程序中安裝體驗相關的資訊，以便我們能夠快速找出並修正客戶所遇到的任何安裝問題。 SQL Server 2017 可以設定為不傳送 （根據每個伺服器執行個體） 的資訊給 Microsoft，透過**mssql conf**。 mssql conf 是 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server 和 Ubuntu 安裝 SQL Server 2017 的組態指令碼。

> [!NOTE]
> 您僅可在付費版本的 SQL Server 中停用將資訊傳送給 Microsoft 的功能。

## <a name="disable-usage-and-diagnostic-data-collection"></a>停用使用狀況和診斷資料收集

此選項可讓您如果 SQL Server 傳送使用方式和收集診斷資料給 Microsoft 或未變更。 依預設，此值設定為 true。 若要變更的值，執行下列命令：

> [!IMPORTANT]
> 您可以關閉使用狀況和診斷資料集合免費的 SQL Server、 Express 和 Developer 版本。

### <a name="on-red-hat-suse-and-ubuntu"></a>Red Hat、 SUSE 和 Ubuntu 上

1. 以 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.customerfeedback**。 下列範例會關閉使用狀況和診斷資料集合，藉由指定**false**。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>在 Docker 上
若要停用使用量和 docker 上的診斷資料收集，您必須擁有 Docker[保存您的資料](sql-server-linux-configure-docker.md)。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 新增`mssql.conf`幾行的檔案`[telemetry]`和`customerfeedback = false`主應用程式目錄中：
 
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

1. 新增`mssql.conf`幾行的檔案`[telemetry]`和`customerfeedback = false`主應用程式目錄中：

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. 執行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>上的 Linux 使用方式和收集診斷資料的 SQL Server 的本機稽核

Microsoft SQL Server 2017 包含網際網路通訊功能，可收集並將您的電腦或裝置 （「 標準電腦資訊 」） 的相關資訊傳送給 Microsoft。 SQL Server 使用狀況和診斷資料集合的本機稽核元件可以寫入至指定的資料夾，代表將傳送給 Microsoft 的資料 （記錄） 服務所收集的資料。 本機稽核的目的是要讓客戶看到 Microsoft 以此功能收集的所有資料，以用於相容性、法規或隱私權驗證的理由。

在 Linux 上的 SQL Server，本機稽核是可以設定 SQL Server Database Engine 的執行個體層級。 其他 SQL Server 元件和 SQL Server Tools 沒有本機稽核功能的使用情況和診斷資料收集。

### <a name="enable-local-audit"></a>啟用本機稽核

此選項會啟用本機稽核，並可讓您設定本機稽核記錄檔建立所在的目錄。

1. 建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新 **/tmp/稽核**目錄：

   ```bash
   sudo mkdir /tmp/audit
   ```

2. 變更擁有者和群組的目錄**mssql**使用者：

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. 以 root 身分執行 mssql conf 指令碼**設定**命令**telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. 重新啟動 SQL Server 服務：

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>在 Docker 上
若要在 docker 上啟用本機稽核，您必須擁有 Docker[保存您的資料](sql-server-linux-configure-docker.md)。 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. 新的本機稽核記錄檔的目標目錄會在容器中。 在您的電腦上的主應用程式目錄中建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新 **/稽核**目錄：

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 新增`mssql.conf`幾行的檔案`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主應用程式目錄中：
 
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

1. 新的本機稽核記錄檔的目標目錄會在容器中。 在您的電腦上的主應用程式目錄中建立新的本機稽核記錄檔的目標目錄。 下列範例會建立新 **/稽核**目錄：

   ```bash
   sudo mkdir <host directory>/audit
   ```

1. 新增`mssql.conf`幾行的檔案`[telemetry]`和`userrequestedlocalauditdirectory = <host directory>/audit`主應用程式目錄中：
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```

1. 執行容器映像

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
   ```

::: moniker-end

## <a name="next-steps"></a>後續步驟

在 Linux 上 SQL Server 的相關資訊，請參閱[概觀的 SQL Server on Linux](sql-server-linux-overview.md)。
