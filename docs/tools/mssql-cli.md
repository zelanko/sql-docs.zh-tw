---
title: mssql-cli
description: mssql-cli 是互動式命令列查詢工具，適用於在 Windows、macOS 或 Linux 上執行的 SQL Server。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein, maghan
ms.custom: tools|mssql-cli
ms.date: 02/22/2018
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 03bc52a6f8941bbc8d04f8f795876b0ca664f08c
ms.sourcegitcommit: 6c2232c4d2c1ce5710296ce97b909f5ed9787f66
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2020
ms.locfileid: "84462282"
---
# <a name="mssql-cli-command-line-query-tool-for-sql-server-preview"></a>SQL Server 的 mssql-cli 命令列查詢工具 (預覽)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

mssql-cli 是用於查詢 SQL Server 的互動式命令列工具，並在 Windows、macOS 或 Linux 上執行。

## <a name="install-mssql-cli"></a>安裝 mssql-cli

如需詳細的安裝指示，請參閱[安裝指南](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)。 以下摘要說明最常見的安裝案例。

### <a name="windows-and-macos-installation"></a>Windows 和 macOS 安裝

在 Windows 和 macOS 上，可使用 `pip` 來安裝 mssql-cli：

```$ pip install mssql-cli```

如需更詳細的指示，請參閱[安裝指南](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)。

### <a name="linux-installation"></a>Linux 安裝

註冊 Microsoft 存放庫之後，可在數個 Linux 發行版本上透過封裝管理員來安裝和升級 mssql-cli。

下列範例適用於 Ubuntu 18.04 (Bionic)，如需其他發行版本的詳細資訊和範例，請參閱[安裝指南](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)。

```
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod

# Update the list of products
sudo apt-get update

# Install mssql-cli
sudo apt-get install mssql-cli

# Install missing dependencies
sudo apt-get install -f
```

## <a name="mssql-cli-documentation"></a>mssql-cli 文件

mssql-cli 的文件位於 [mssql-cli GitHub 存放庫](https://github.com/dbcli/mssql-cli)。

- [主頁面/讀我檔案](https://github.com/dbcli/mssql-cli)
- [安裝指南](https://github.com/dbcli/mssql-cli/tree/master/doc/installation)
- [使用指南](https://github.com/dbcli/mssql-cli/blob/master/doc/usage_guide.md)

其他文件位於 [doc 資料夾](https://github.com/dbcli/mssql-cli/tree/master/doc)。
