---
title: 連線程式庫和架構
description: 列出用戶端應用程式可透過各種語言使用的連線驅動程式，以連線到在內部部署或雲端中、於 Linux、Windows 或 Docker 上執行的 Microsoft SQL Server，以及 Azure SQL Database 和 Azure Synapse Analytics。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: c626df1042ed3b3d9ecb5e25bbd219ceb468bfee
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115491"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Microsoft SQL Server 的連線程式庫和架構

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

請查看[使用者入門教學課程](https://aka.ms/sqldev)，以快速開始使用 C#、Java、node.js、PHP 和 Python 等程式語言，並使用 Linux 上的 SQL Server 或 macOS 上的 Windows 或 Docker 來建置應用程式。

下表列出用戶端應用程式可透過各種語言使用的連線程式庫或「驅動程式」，以連線並使用在內部部署或雲端中、於 Linux、Windows 或 Docker 上執行的 Microsoft SQL Server，以及 Azure SQL Database 和 Azure Synapse Analytics。 

| Language | 平台 | 其他資源 | 下載 | 開始使用 |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows、Linux、macOS | [Microsoft ADO.NET for SQL Server](../connect/ado-net/microsoft-ado-net-sql-server.md) | [下載](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [開始使用](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows、Linux、macOS | [Microsoft JDBC Driver for SQL Server](../connect/jdbc/microsoft-jdbc-driver-for-sql-server.md) | [下載](https://go.microsoft.com/fwlink/?LinkId=245496) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows、Linux、macOS| [適用於 SQL Server 的 PHP SQL 驅動程式](../connect/php/microsoft-php-driver-for-sql-server.md) | 作業系統： <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows、Linux、macOS | [Node.js Driver for SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows、Linux、macOS | [Python SQL 驅動程式](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](../connect/python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows、Linux、macOS | [適用於 SQL Server 的 Ruby 驅動程式](../connect/ruby/ruby-driver-for-sql-server.md) | [開始使用](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows、Linux、macOS | [Microsoft ODBC Driver for SQL Server](../connect/odbc/microsoft-odbc-driver-for-sql-server.md) | [下載](../connect/odbc/microsoft-odbc-driver-for-sql-server.md) |  

下表列出幾個物件關聯式對應 (ORM) 架構與 Web 架構範例，可供用戶端應用程式搭配在內部部署或雲端中、於 Linux、Windows 或 Docker 上執行的 Microsoft SQL Server，以及 Azure SQL Database 和 Azure Synapse Analytics 使用。 

| Language | 平台 | ORM |
| :-- | :-- | :-- |
| C# | Windows、Linux、macOS | [Entity Framework](/ef)<br>[Entity Framework Core](/ef/core/index) |
| Java | Windows、Linux、macOS |[Hibernate ORM](https://hibernate.org/orm)|
| PHP | Windows、Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows、Linux、macOS | [Sequelize ORM](http://sequelize.org/) |
| Python | Windows、Linux、macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows、Linux、macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>相關連結
- 可供用戶端應用程式連接的 [SQL Server 驅動程式](../connect/sql-connection-libraries.md)