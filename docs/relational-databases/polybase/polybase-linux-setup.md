---
title: 在 Linux 上安裝 PolyBase
titlesuffix: SQL Server
description: 了解如何在 Linux 上安裝 SQL Server PolyBase。 PolyBase 可讓您針對遠端資料來源執行外部查詢。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: dakryze
ms.date: 8/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 6bed37e6fe0451e45e9d99fd9c15d03d12a30a4b
ms.sourcegitcommit: 19ae05bc69edce1e3b3d621d7fdd45ea5f74969d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564648"
---
# <a name="install-polybase-on-linux"></a>在 Linux 上安裝 PolyBase

[!INCLUDE [sqlserver2019-linux](../../includes/applies-to-version/sqlserver2019-linux.md)]

下列步驟會在 Linux 上安裝 [PolyBase](../../relational-databases/polybase/polybase-guide.md) (`mssql-server-polybase` 和 `mssql-server-polybase-hadoop`)。 PolyBase 可讓您針對遠端資料來源執行外部查詢。

>[!NOTE]
> 安裝 PolyBase 之前，請先[安裝 SQL Server 2019](../../linux/sql-server-linux-setup.md#platforms)。 這會設定在安裝 `mssql-server-polybase` 和 `mssql-server-polybase-hadoop` 套件時所使用的金鑰和存放庫。

>[!NOTE]
>
> - 適用於 Linux 的 SQL Server 2017 不支援 PolyBase。
> - 目前無法使用 Linux 上的 PolyBase 向外延展。

安裝您作業系統所適用的 PolyBase：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="install-on-rhel"></a><a name="RHEL"></a>在 RHEL 上安裝

使用下列命令，在 Red Hat Enterprise Linux 上安裝 `mssql-server-polybase`。 

```bash
sudo yum install -y mssql-server-polybase
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>安裝完成後，您必須[啟用 PolyBase 功能](#enable)。

使用下列命令來安裝 `mssql-server-polybase-hadoop`。 

```bash
sudo yum install -y mssql-server-polybase-hadoop
```

PolyBase Hadoop 套件具有下列套件的相依性：
- `mssql-server`
- `mssql-server-polybase`
- `mssql-server-extensibility`
- `mssql-zulu-jre-11`. 

安裝會提示重新啟動 `launchpadd`。 請使用下列命令來執行這項作業。

```bash
sudo systemctl restart mssql-launchpadd
```

>[!NOTE]
>安裝之後，即必須[設定 Hadoop 連接層級](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md#c-set-hadoop-connectivity)。

如果您需要離線安裝，請在[版本資訊](../../linux/sql-server-linux-release-notes.md)中找到 PolyBase 套件下載。 然後使用[安裝 SQL Server](../../linux/sql-server-linux-setup.md#offline)一文所述的相同離線安裝步驟。

## <a name="install-on-ubuntu"></a><a name="ubuntu"></a>在 Ubuntu 上安裝

使用下列命令，在 Ubuntu 上安裝 `mssql-server-polybase`。 

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

使用下列命令來安裝 `mssql-server-polybase-hadoop`。 

```bash
sudo apt-get install mssql-server-polybase-hadoop
```

PolyBase Hadoop 套件具有下列套件的相依性：
- `mssql-server`
- `mssql-server-polybase`
- `mssql-server-extensibility`
- `mssql-zulu-jre-11`. 

安裝會提示重新啟動 `launchpadd`。 請使用下列命令來執行這項作業。

```bash
sudo systemctl restart mssql-launchpadd
```

>[!NOTE]
>安裝之後，即必須[設定 Hadoop 連接層級](../../relational-databases/polybase/polybase-configure-hadoop.md#configure-hadoop-connectivity)。

## <a name="install-on-sles"></a><a name="SLES"></a>在 SLES 上安裝

使用下列命令，在 SUSE Linux Enterprise Server 上安裝 `mssql-server-polybase`。 

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


## <a name="enable-polybase"></a><a name="enable"></a> 啟用 PolyBase

安裝之後，您必須啟用 PolyBase 來存取其功能。 請連線到已安裝的 SQL Server 執行個體，並使用下列 Transact-SQL 命令來啟用。

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE WITH OVERRIDE;
```

## <a name="update-polybase"></a>更新 PolyBase

如果您已安裝 `mssql-server-polybase`，則可以使用下列命令更新為最新版本：

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase-hadoop
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
sudo yum install -y mssql-server-polybase-hadoop
```

系統將提示您重新啟動 SQL Server 執行個體。 請使用下列命令來執行這項作業。

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase-hadoop
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
sudo apt-get remove mssql-server-polybase-hadoop
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

Linux 上的 PolyBase 可以存取下列資料來源。 如需如何從這些 PolyBase 啟用來源建立外部資料表的詳細資訊，請遵循所提供的連結。 

- [SQL Server、SQL 資料庫、Azure Synapse Analytics)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Hadoop](../../relational-databases/polybase/polybase-configure-hadoop.md)
- [Azure Blob 儲存體](../../relational-databases/polybase/polybase-configure-azure-blob-storage.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (與 Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

如需使用此項目方式的詳細資訊，請參閱 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 的 Transact-SQL 參考文章。
