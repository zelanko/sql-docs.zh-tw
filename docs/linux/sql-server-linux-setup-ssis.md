---
title: 在 Linux 上安裝 SQL Server Integration Services |Microsoft Docs
description: 本文說明如何在 Linux 上安裝 SQL Server Integration Services (SSIS)。
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: d2e72c77ad5f200c07a6e71025a3461d6397032a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38062047"
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>在 Linux 上安裝 SQL Server Integration Services (SSIS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

遵循這篇文章，若要安裝 SQL Server Integration Services 中的步驟 (`mssql-server-is`) 在 Linux 上。 如需在這一版的 linux Integration Services 中支援之功能的資訊，請參閱 < [Release Notes](sql-server-linux-release-notes.md)。

安裝適用於您平台的 SQL Server 整合的伺服器：

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a> 在 Ubuntu 上安裝 SSIS
若要安裝`mssql-server-is`封裝在 Ubuntu 上，請遵循下列步驟：

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

4. 安裝 Integration Services 之後, 執行`ssis-conf`。 如需詳細資訊，請參閱 <<c0> [ 設定的 SSIS 在 Linux 上使用 ssis conf](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. 完成設定之後，設定的路徑。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果您已經有`mssql-server-is`安裝，您可以更新為最新的版本，使用下列命令：

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除`mssql-server-is`，您可以執行下列命令：
```bash
sudo apt-get remove mssql-server-is
```

## <a name="RHEL"></a> 在 RHEL 上安裝 SSIS
若要安裝`mssql-server-is`RHEL 上的封裝，請遵循下列步驟：

1. 下載 Microsoft SQL Server Red Hat 存放庫的組態檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. 安裝之後，執行`ssis-conf`。 如需詳細資訊，請參閱 <<c0> [ 設定的 SSIS 在 Linux 上使用 ssis conf](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 完成設定之後，請將路徑設定。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果您已經有`mssql-server-is`安裝，您可以更新為最新的版本，使用下列命令：

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除`mssql-server-is`，您可以執行下列命令：
```bash
sudo yum remove mssql-server-is
```

## <a name="unattended-installation"></a>自動安裝
若要執行自動的安裝，當您執行`ssis-conf setup`，執行下列動作：
1.  指定`-n`（沒有提示） 選項。
2.  設定環境變數，以提供必要的值。

下列範例會執行下列動作：
-   安裝 SSIS。
-   藉由提供的值指定 Developer edition`SSIS_PID`環境變數。
-   接受使用者授權合約所提供的值`ACCEPT_EULA`環境變數。
-   藉由指定執行自動的安裝`-n`（沒有提示） 選項。

```
sudo SSIS_PID=Developer ACCEPT_EULA=Y /opt/ssis/bin/ssis-conf -n setup 
```

### <a name="environment-variables-for-unattended-installation"></a>自動安裝的環境變數

| 環境變數 | 描述 |
|---|---|
| **ACCEPT_EULA** | 接受 SQL Server 授權合約，當設定為任何值 (例如`Y`)。|
| **SSIS_PID** | 設定 SQL Server 版本或產品金鑰。 以下是可能的值：<br/>Evaluation<br/>Developer<br/>Express <br/>Web <br/>Standard<br/>Enterprise <br/>產品金鑰<br/><br/>如果您指定產品金鑰，必須在表單中的產品金鑰`#####-#####-#####-#####-#####`，其中`#`是字母或數字。  |
| | |

## <a name="next-steps"></a>後續的步驟

若要在 Linux 上執行 SSIS 套件，請參閱[擷取、 轉換及載入資料，使用 SSIS 在 Linux 上的 SQL server](sql-server-linux-migrate-ssis.md)。

若要在 Linux 上設定 SSIS 的其他設定，請參閱[在 Linux 上使用 ssis conf 設定 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。

## <a name="related-content-about-ssis-on-linux"></a>關於 Linux 上的 SSIS 的相關的內容
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上設定 SQL Server Integration Services 使用 ssis conf](sql-server-linux-configure-ssis.md)
-   [限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md)
-   [排程 SQL Server Integration Services 封裝執行在 Linux 上的使用 cron](sql-server-linux-schedule-ssis-packages.md)
