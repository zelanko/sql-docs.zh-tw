---
title: 連線程式庫和架構 |Microsoft Docs
description: 列出用戶端應用程式可以使用從各種不同的語言來連線到內部部署上執行的 Microsoft SQL Server，或在雲端、 Linux、 Windows 或 Docker 和 Azure SQL Database 和 Azure SQL 資料倉儲中的連線能力驅動程式。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: 1f0274a8eb84f9700378d266729afbdc91aebaf1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713211"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>連線程式庫和 Microsoft SQL server 的架構

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

請參閱[開始使用教學課程](https://aka.ms/sqldev)快速開始使用程式設計語言，例如 C#、 Java、 Node.js、 PHP 和 Python，並建置應用程式在 macOS 上使用 Linux 或 Windows 或 Docker 上的 SQL Server。

下表列出連線程式庫或*驅動程式*用戶端應用程式可以從各種不同的語言來連線至並使用 Microsoft SQL Server 執行內部部署或在雲端、 Linux、 Windows 或 Docker 上使用和也為 Azure SQL Database 和 Azure SQL 資料倉儲。 

| 語言 | 平台 | 其他資源 | 下載 | 開始使用 |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows、 Linux、 macOS | [Microsoft ADO.NET for SQL Server](https://msdn.microsoft.com/library/mt657768.aspx) | [下載](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [開始使用](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows、 Linux、 macOS | [Microsoft JDBC Driver for SQL Server](https://msdn.microsoft.com/library/mt484311.aspx) | [下載](https://go.microsoft.com/fwlink/?LinkId=245496) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows、 Linux、 macOS| [PHP SQL Driver for SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | 作業系統： <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows、 Linux、 macOS | [Node.js Driver for SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows、 Linux、 macOS | [Python SQL 驅動程式](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [開始使用](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows、 Linux、 macOS | [適用於 SQL Server 的 Ruby 驅動程式](../connect/ruby/ruby-driver-for-sql-server.md) | [開始使用](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows、 Linux、 macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [下載](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

下表列出一些物件關聯式對應 (ORM) 架構和 web 架構的用戶端應用程式可以使用內部部署上執行的 Microsoft SQL server，或在雲端、 Linux、 Windows 或 Docker 和 Azure SQL database 中的範例和Azure SQL 資料倉儲。 

| 語言 | 平台 | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows、 Linux、 macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows、 Linux、 macOS |[休眠 ORM](https://hibernate.org/orm)|
| PHP | Windows、 Linux | [Laravel （導師）](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows、 Linux、 macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows、 Linux、 macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows、 Linux、 macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>相關連結
- [SQL Server 驅動程式](https://msdn.microsoft.com/library/mt654049.aspx)從用戶端應用程式連線
