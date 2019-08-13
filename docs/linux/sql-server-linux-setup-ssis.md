---
title: 在 Linux 上安裝 SQL Server Integration Services
description: 本文描述如何在 Linux 上安裝 SQL Server Integration Services (SSIS)。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 68f3497e9f3f47d7e43c2bda0083bc25632d8221
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032432"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>在 Linux 上安裝 SQL Server Integration Services (SSIS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

請遵循本文中的步驟，在 Linux 上安裝 SQL Server Integration Services (`mssql-server-is`)。 如需此版本 Integration Services for Linux 支援功能的資訊，請參閱[版本資訊](sql-server-linux-release-notes.md)。

為您的平台安裝 SQL Server Integration Server：

- [Ubuntu 16.04](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> 在 Ubuntu 上安裝 SSIS
若要在 Ubuntu 上安裝 `mssql-server-is` 套件，請遵循下列步驟：

1. 匯入公用存放庫 GPG 金鑰。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 註冊 Microsoft SQL Server Ubuntu 存放庫。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. 安裝 Integration Services 之後，請執行 `ssis-conf`。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. 完成設定之後，請設定路徑。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果您已安裝 `mssql-server-is`，即可使用下列命令來更新為最新版本：

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除 `mssql-server-is`，您可以執行下列命令：
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> 在 RHEL 上安裝 SSIS
若要在 RHEL 上安裝 `mssql-server-is` 套件，請遵循下列步驟：

1. 下載 Microsoft SQL Server Red Hat 存放庫設定檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. 安裝後，請執行 `ssis-conf`。 如需詳細資訊，請參閱[使用 ssis-conf 設定 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成設定之後，請設定路徑。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果您已安裝 `mssql-server-is`，即可使用下列命令來更新為最新版本：

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除 `mssql-server-is`，您可以執行下列命令：
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>自動安裝
當您執行 `ssis-conf setup` 時，若要執行自動安裝，請執行下列動作：
1.  指定 `-n` (無提示) 選項。
2.  設定環境變數，以提供必要的值。

下列範例會執行下列動作：
-   安裝 SSIS。
-   提供 `SSIS_PID` 環境變數的值，以指定 Developer 版本。
-   提供 `ACCEPT_EULA` 環境變數的值，以接受 EULA。
-   指定 `-n` (無提示) 選項，以執行自動安裝。

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>自動安裝的環境變數

| 環境變數 | Description |
|---|---|
| **ACCEPT_EULA** | 當設定為任何值時 (例如 `Y`)，即接受 SQL Server 授權合約。|
| **SSIS_PID** | 設定 SQL Server 版本或產品金鑰。 下列為可能的值：<br/>Evaluation<br/>Developer<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>產品金鑰<br/><br/>如果您指定產品金鑰，則產品金鑰的格式必須為 `#####-#####-#####-#####-#####`，其中 `#` 是字母或數字。  |
| | |

## <a name="next-steps"></a>後續步驟

若要在 Linux 上執行 SSIS 套件，請參閱[使用 SSIS 在 Linux 上的 SQL Server 擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)。

若要在 Linux 上設定其他 SSIS 設定，請參閱[使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="related-content-about-ssis-on-linux"></a>Linux 上的 SSIS 相關內容
-   [使用 SSIS 在 Linux 上擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)
-   [使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md)
-   [使用 cron 排程 Linux 上的 SQL Server Integration Services 套件執行](sql-server-linux-schedule-ssis-packages.md)
