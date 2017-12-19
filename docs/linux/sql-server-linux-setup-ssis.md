---
title: "Linux 上安裝 SQL Server Integration Services |Microsoft 文件"
description: "本文說明如何在 Linux 上安裝 SQL Server Integration Services (SSIS)。"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 13bd5bde7e4e4ec63bb7e3bd7d8959440f499672
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux 上安裝 SQL Server Integration Services (SSIS)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

遵循安裝 SQL Server Integration Services 這篇文章中的步驟 (`mssql-server-is`) 在 Linux 上。 如需適用於 Linux Integration Services 的此版本中支援之功能的資訊，請參閱[Release Notes](sql-server-linux-release-notes.md)。

安裝 SQL Server 的整合伺服器適用於您的平台。

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)

## <a name="ubuntu"></a>在 Ubuntu 上中安裝 SSIS
若要安裝`mssql-server-is`Ubuntu 上的套件，請遵循下列步驟：

1. 匯入公用儲存機制 GPG 索引鍵。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. 註冊 Microsoft SQL Server Ubuntu 儲存機制。

   ```bash
   sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
   ```

3. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo apt-get update
   sudo apt-get install -y mssql-server-is
   ```

4. 安裝 Integration Services 之後，執行`ssis-conf`。 如需詳細資訊，請參閱[設定 ssis conf 與 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

5. 完成設定之後，設定的路徑。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果您已經有`mssql-server-is`安裝，您可以更新為最新版本，使用下列命令：

```bash
sudo apt-get install mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除`mssql-server-is`，您可以執行下列命令：
```bash
sudo apt-get remove msssql-server-is
```

## <a name="RHEL"></a>RHEL 上中安裝 SSIS
若要安裝`mssql-server-is`RHEL 上的套件，請遵循下列步驟：

1. 下載 Microsoft SQL Server Red Hat 儲存機制設定檔。

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
   ```

1. 執行下列命令來安裝 SQL Server Integration Services。

   ```bash
   sudo yum install -y mssql-server-is
   ```


1. 安裝之後，執行`ssis-conf`。 如需詳細資訊，請參閱[設定 ssis conf 與 Linux 上的 SSIS](sql-server-linux-configure-ssis.md)。

   ```bash
   sudo /opt/ssis/bin/ssis-conf setup
   ```

1. 一旦完成設定，設定路徑。

   ```bash
   export PATH=/opt/ssis/bin:$PATH
   ```

### <a name="update-ssis"></a>更新 SSIS
如果您已經有`mssql-server-is`安裝，您可以更新為最新版本，使用下列命令：

```bash
sudo yum update mssql-server-is
```

### <a name="remove-ssis"></a>移除 SSIS
若要移除`mssql-server-is`，您可以執行下列命令：
```bash
sudo yum remove mssql-server-is
```

## <a name="next-steps"></a>後續的步驟

若要在 Linux 上執行 SSIS 封裝，請參閱[擷取、 轉換及載入資料的 SQL Server on Linux 與 SSIS](sql-server-linux-migrate-ssis.md)。

若要設定在 Linux 上的 SSIS 的其他設定，請參閱[ssis conf 與 Linux 上設定 SQL Server Integration Services](sql-server-linux-configure-ssis.md)。
