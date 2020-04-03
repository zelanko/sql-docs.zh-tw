---
title: Microsoft SQL Databases 的連線程式庫 | Microsoft Docs
description: 提供模組下載連結，這些模組可供從各種用戶端程式設計語言連線到 Microsoft SQL Server 與 Azure SQL Database。
author: RothJa
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 03/05/2020
ms.author: JRoth
ms.openlocfilehash: 88fbd0e3fd01492b8e7d920eb132196f8a005478
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79434115"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 資料庫的連線模組

此文章提供連線模組或驅動程式  的下載連結，這些可讓您的用戶端程式用來與 [Microsoft SQL Server](../relational-databases/database-features.md)互動，以及其在雲端的對應項 [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/) 互動。 驅動程式適用於在下列作業系統上執行的各種程式設計語言：

- Linux
- macOS
- Windows

**OOP 與關聯式不相符：**

*關聯式*：以物件導向程式設計 (OOP) 語言撰寫的用戶端程式通常會使用 SQL 驅動程式，這些驅動程式會以比導向物件更具關聯性的格式來傳回所查詢資料。 使用 ADO.NET 的 C# 是其中一個範例。 OOP 關聯式格式不相符有時會使 OOP 程式碼更難撰寫及理解。

*ORM*：其他驅動程式或架構會以 OOP 格式傳回查詢的資料，進而避免不相符。 這些驅動程式的運作方式是預期類別已定義以符合特定 SQL 資料表的資料行。 接著，驅動程式會執行*物件關聯式對應* (ORM)，以類別執行個體的形式傳回查詢的資料。 適用於 C# 的 Microsoft 的 Entity Framework (EF) 與適用於 Java 的 Hibernate 就是兩個範例。

目前的文章會專節討論這兩種連線驅動程式。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>關聯式存取的驅動程式

| Language | 下載 SQL 驅動程式 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[適用於下列作業系統的 .NET Core：Linux-Ubuntu、macOS、Windows](https://dotnet.microsoft.com/download) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 驅動程式，安裝指示](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc，安裝指示](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下載 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驅動程式，安裝指示](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 下載頁面](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br/> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 存取的驅動程式

下表列出用戶端應用程式用來連線到 Microsoft SQL 資料庫的物件關聯式對應 (ORM) 架構範例。

| Language | ORM 驅動程式下載 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x 或更新版本)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM，包含在 Laravel 安裝中](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |
| &nbsp; | <br/> |

<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Build-an-app 網頁

**[https://aka.ms/sqldev](https://aka.ms/sqldev)** 會帶您前往一組「建立應用程式」  網頁。 網頁提供多種程式設計語言、作業系統與 SQL 連線驅動程式組合的相關資訊。 在「建立用程式」網頁提供的資訊包括下列項目：

- 關於針對每種語言 + 作業系統 + 驅動程式的組合，如何開始著手的詳細資料。
  - 有關安裝最新 SQL 連線驅動程式的指示。
- 下列每個項目的程式碼範例：
  - 物件關聯式程式碼範例。
  - ORM 程式碼範例。
  - 資料行存放區索引示範，以提供更快的效能。

**「建立應用程式」網頁的第一頁：**  
![「建立應用程式」網頁的第一頁螢幕擷取畫面](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png)

**「建立應用程式」網頁的 [Java - Ubuntu] 功能表**  
![「建立應用程式」網頁的 [Java Ubuntu] 功能表](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png)

&nbsp;

## <a name="related-links"></a>相關連結

- [用於使用 Java 與其他語言連線到雲端 Azure SQL Database 的程式碼範例](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!--
Image references, **obsolete** markdown syntax alternative:

![Build-an-app webpages, first page screenshot][image-ref-163-buildanapp-webpages-first-page]
![Build-an-app webpages, menu Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
-->
