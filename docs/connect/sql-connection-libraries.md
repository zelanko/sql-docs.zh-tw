---
title: Microsoft SQL 資料庫的連線庫 |Microsoft Docs
description: 提供可從各種程式設計語言的用戶端連線到 Microsoft SQL Server 和 Azure SQL Database 的模組下載連結。
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 7f759dbe9022cff557461d900a35b3ccc91d2c4b
ms.sourcegitcommit: 0f452eca5cf0be621ded80fb105ba7e8df7ac528
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007571"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>適用於 Microsoft SQL 資料庫的連線模組

本文提供連線模組下載連結或*驅動程式*用戶端程式可用來與互動[Microsoft SQL Server](../relational-databases/database-features.md)，和在雲端中與其對應項[AzureSQL Database](https://docs.microsoft.com/azure/sql-database/)。 驅動程式可供各種程式設計語言，在下列作業系統上執行：

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP 關聯的不相符

*關聯式*： 通常以物件導向程式設計 (OOP) 語言撰寫的用戶端程式使用中的多個關聯式與物件導向的格式傳回查詢的資料的 SQL 驅動程式。 C# 使用 ADO.NET 是其中一個範例。 OOP 關聯式格式不符合有時甚至會使 OOP 程式碼難以撰寫及了解。

*ORM*： 其他驅動程式或架構查詢的格式傳回資料 OOP，避免不相符。 這些驅動程式來處理預期類別已定義以符合特定的 SQL 資料表的資料行。 驅動程式接著會執行*物件關聯式對應*(ORM) 類別的執行個體形式傳回查詢的資料。 Microsoft 的 Entity Framework (EF) 適用於 C# 和 java 的休眠是兩個範例。

現有的文章會專用於連線的驅動程式的這兩種的另一節。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>驅動程式的關聯式存取


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| 語言 | 下載 SQL 驅動程式 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br /><br />[.NET core for Linux Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[適用於 MacOS 的.NET core](https://www.microsoft.com/net/core#macos)<br />[.NET core for Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 驅動程式，安裝指示](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc，安裝指示](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下載 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驅動程式，安裝指示](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 的下載頁面](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 存取的驅動程式


下表列出物件關聯式對應 (ORM) 架構用戶端應用程式用來連線到 Microsoft SQL database 的範例。


| 語言 | ORM 驅動程式下載 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x 或更新版本)](https://docs.microsoft.com/ef/) |
| Java | [休眠 ORM](https://hibernate.org/orm)|
| PHP | [導師的 ORM，隨附於 Laravel 安裝](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>建置的應用程式網頁
[https://aka.ms/sqldev](https://aka.ms/sqldev) 會帶您前往一整組*建置的應用程式*網頁。 網頁提供的程式設計語言、 作業系統和 SQL 連接驅動程式的多個組合的資訊。 建置的應用程式網頁所提供的資訊包括下列項目：

- 如何開始從一開始，每個語言 + 作業系統驅動程式組合的詳細資料。
    - 安裝最新的 SQL 連接驅動程式的指示。
- 針對每個下列項目程式碼範例：
    - 物件關聯的程式碼範例。
    - ORM 程式碼範例。
    - 資料行存放區索引示範更快的效能。

#### <a name="first-page-of-build-an-app-webpages"></a>第一個頁面上，建置的應用程式的網頁
![建置應用程式的網頁，第一個頁面的螢幕擷取畫面][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>適用於 Java-Ubuntu，建置的應用程式的網頁的功能表
![建置應用程式的網頁，功能表 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>相關連結
- [程式碼連接到 Azure SQL Database 在雲端中，使用 Java 和其他語言的範例](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
