---
title: "Linux 上安裝 SQL Server Integration Services |Microsoft 文件"
description: "本主題描述如何在 Linux 上安裝 SQL Server Integration Services。"
author: leolimsft
ms.author: lle
manager: craigg
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: integration-services
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c3943870ec10b8430ac4819398908c5459a8b03c
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-integration-services-ssis-on-linux"></a>Linux 上安裝 SQL Server Integration Services (SSIS)


遵循安裝 SQL Server Integration Services 這篇文章中的步驟 (`mssql-server-is`) 在 Linux 上。 如需適用於 Linux Integration Services 的此版本中支援之功能的資訊，請參閱[Release Notes](sql-server-linux-release-notes.md)。

安裝 SQL Server 的整合伺服器適用於您的平台。

- [Ubuntu](#ubuntu)
- [Red Hat Enterprise Linux](#RHEL)



## <a name="ubuntu"></a>在 Ubuntu 上中安裝 SSIS
若要安裝`mssql-server-is`Ubuntu 上的套件，請遵循下列步驟：


1.  匯入公用儲存機制 GPG 索引鍵。

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add –
    ```


2.  註冊 Microsoft SQL Server Ubuntu 儲存機制。

    ```bash
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server.list | sudo tee /etc/apt/sources.list.d/mssql-server.list
    ```


3.  執行下列命令來安裝 SQL Server Integration Services。

    ```bash
    sudo apt-get update
    sudo apt-get install -y mssql-server-is
    ```


4.  安裝 Integration Services 之後，執行`ssis-conf`。

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


5.  完成設定之後，設定的路徑。

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


如果您已經有`mssql-server-is`安裝，您可以更新為最新版本，使用下列命令：

```bash
sudo apt-get install mssql-server-is
```


若要移除`mssql-server-is`，您可以執行下列命令：
```bash
sudo apt-get remove msssql-server-is
```



## <a name="RHEL"></a>RHEL 上中安裝 SSIS
若要安裝`mssql-server-is`RHEL 上的套件，請遵循下列步驟：


1.  輸入超級使用者模式。

    ```bash
    sudo su
    ```


2.  下載 Microsoft SQL Server Red Hat 儲存機制設定檔。

    ```bash
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
    ```


3.  結束超級使用者模式。

    ```bash
    exit
    ```


4.  執行下列命令來安裝 SQL Server Integration Services。

    ```bash
    sudo yum install -y mssql-server-is
    ```


5.  安裝之後，請執行`ssis-conf`。

    ```bash
    sudo /opt/ssis/bin/ssis-conf setup
    ```


6.  一旦完成設定，設定路徑。

    ```bash
    export PATH=/opt/ssis/bin:$PATH
    ```


如果您已經有`mssql-server-is`安裝，您可以更新為最新版本，使用下列命令：

```bash
sudo yum update mssql-server-is
```


若要移除`mssql-server-is`，您可以執行下列命令：
```bash
sudo yum remove msssql-server-is
```




## <a name="run-a-package"></a>執行封裝
將 SSIS 封裝複製至 Linux 電腦。 然後使用下列命令來執行封裝。

```bash
dtexec /F <package name> /DE <protection password>
```



## <a name="next-steps"></a>後續的步驟

如需如何在 Linux 上使用 SSIS 來擷取、 轉換和載入資料的詳細資訊，請參閱[擷取、 轉換和載入資料的 SQL Server on Linux 與 SSIS](sql-server-linux-migrate-ssis.md)。
