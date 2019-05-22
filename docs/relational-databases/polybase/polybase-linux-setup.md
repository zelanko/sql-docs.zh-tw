---
title: 在 Linux 上安裝 PolyBase | Microsoft Docs
description: 本文描述如何在 Linux 上安裝 SQL Server 全文檢索搜尋。
author: aboke
ms.author: aboke
manager: craigg
ms.date: 4/12/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.openlocfilehash: 69c256ef52d9c302d55ef1499059d959ed55b528
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759065"
---
# <a name="install-polybase-on-linux"></a>在 Linux 上安裝 PolyBase

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟會在 Linux 上安裝 [PolyBase](../../relational-databases/search/full-text-search.md) (**mssql-server-polybase**)。 PolyBase 可讓您針對遠端資料來源執行外部查詢。 

>[!NOTE]
> 在第一次安裝 Polybase 之前，請[安裝 SQL Server](../../linux/sql-server-linux-setup.md#platforms)。 這會設定您在安裝 **mssql-server-polybase** 套件時所使用的金鑰和存放庫。

> 目前無法使用 Linux 上的 PolyBase 向外延展。


安裝您作業系統所適用的 PolyBase：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name="RHEL">在 RHEL 上安裝</a>

使用下列命令，在 Red Hat Enterprise Linux 上安裝 **mssql-server-polybase**。 

```bash
sudo yum install -y mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安裝完成後，您必須[啟用 PolyBase 功能](#enable)。

如果您需要離線安裝，請在[版本資訊](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 套件下載。 然後使用[安裝 SQL Server](../../linux/sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="ubuntu">在 Ubuntu 上安裝</a>

使用下列命令，在 Ubuntu 上安裝 **mssql-server-polybase**。 

```bash
sudo apt-get install mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安裝完成後，您必須[啟用 PolyBase 功能](#enable)。

如果您需要離線安裝，請在[版本資訊](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 套件下載。 然後使用[安裝 SQL Server](../../linux/sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="SLES">在 SLES 上安裝</a>

使用下列命令，在 SUSE Linux Enterprise Server 上安裝 **mssql-server-polybase**。 

```bash
sudo zypper install mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安裝完成後，您必須[啟用 PolyBase 功能](#enable)。


如果您需要離線安裝，請在[版本資訊](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 套件下載。 然後使用[安裝 SQL Server](../../linux/sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。


## <a name="enable">啟用 PolyBase</a> 

安裝之後，您必須啟用 PolyBase 來存取其功能。 請連線到已安裝的 SQL Server 執行個體，並使用下列 Transact-SQL 命令來啟用。

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [WITH OVERRIDE];
```

## <a name="update-polybase"></a>更新 PolyBase

如果您已安裝 **mssql-server-polybase**，則可以使用下列命令更新為最新版本：

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>安裝完成後，您必須[啟用 PolyBase 功能](#enable)。

## <a name="next-steps"></a>後續步驟

### <a name="supported-external-data-sources-on-linux"></a>Linux 上支援的外部資料來源

Linux 上的 PolyBase 可以存取下列資料來源。 如需如何從這些 PolyBase 啟用來源建立外部資料表的詳細資訊，請遵循所提供的連結。 

- [SQL Server (與 SQL DB、Azure SQL DW)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (與 Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

如需使用此項目方式的詳細資訊，請參閱 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 的 Transact-SQL 參考文章。