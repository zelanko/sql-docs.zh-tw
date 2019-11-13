---
title: Microsoft SQL 資料庫的連接庫 |Microsoft Docs
description: 提供模組的下載連結，可讓您從各種不同的用戶端程式設計語言連接到 Microsoft SQL Server 和 Azure SQL Database。
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632812"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 資料庫的連接模組

本文提供用戶端程式可用來與[Microsoft SQL Server](../relational-databases/database-features.md)互動的連線模組或*驅動程式*的下載連結，以及其在雲端[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)中的對應項。 驅動程式適用于在下列作業系統上執行的各種程式設計語言：

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP 與關聯式不符

*關聯式*：以物件導向程式設計（OOP）語言撰寫的用戶端程式，通常會使用 SQL 驅動程式，以比物件導向更關聯式的格式來傳回查詢的資料。 C#使用 ADO.NET 是其中一個範例。 OOP 關聯式格式不相符，有時會使 OOP 程式碼更難寫入和瞭解。

*ORM*：其他驅動程式或架構會以 OOP 格式傳回查詢的資料，避免不相符。 這些驅動程式的作用是預期類別已定義為符合特定 SQL 資料表的資料行。 然後，驅動程式會執行*物件關聯式對應*（ORM），以傳回查詢的資料做為類別的實例。 Microsoft 的 Entity Framework （EF） for C#和休眠（適用于 JAVA）是兩個範例。

目前的文章會階層願意投入這兩種連接驅動程式的個別區段。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>關聯式存取的驅動程式


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Language | 下載 SQL 驅動程式 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[適用于 Linux 的 .NET Core-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core，適用于 MacOS](https://www.microsoft.com/net/core#macos)<br />[適用于 Windows 的 .NET Core](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 驅動程式，安裝指示](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc，安裝指示](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下載 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驅動程式，安裝指示](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 下載頁面](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 存取的驅動程式


下表列出用戶端應用程式用來連接到 Microsoft SQL 資料庫的物件關聯式對應（ORM）架構範例。


| Language | ORM 驅動程式下載 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework （6.x 或更新版本）](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM （包含在 Laravel 安裝中）](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>建立應用程式網頁
[https://aka.ms/sqldev](https://aka.ms/sqldev)會帶您前往一組*組建-應用程式*網頁。 網頁提供多種程式設計語言、作業系統和 SQL 連接驅動程式組合的相關資訊。 在組建-應用程式網頁所提供的資訊中，有下列專案：

- 關於每個語言 + 作業系統 + 驅動程式組合如何開始著手的詳細資料。
    - 安裝最新 SQL 連接驅動程式的指示。
- 下列每個專案的程式碼範例：
    - 物件關聯式程式碼範例。
    - ORM 程式碼範例。
    - 資料行存放區索引示範，以提供更快的效能。

#### <a name="first-page-of-build-an-app-webpages"></a>第一頁，內建應用程式網頁
![組建-應用程式網頁，第一頁螢幕擷取畫面][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>JAVA-Ubuntu 的功能表，適用于組建-應用程式網頁
![組建-應用程式網頁，功能表 JAVA Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>相關連結
- [使用 JAVA 和其他語言連接到雲端中 Azure SQL Database 的程式碼範例](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
