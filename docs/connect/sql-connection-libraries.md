---
title: Microsoft SQL 資料庫的連線庫 |Microsoft 文件
description: 提供的模組可讓連接到 Microsoft SQL Server 和 Azure SQL Database 中，從各種不同的程式設計語言的用戶端下載的連結。
author: MightyPen
ms.service: ''
ms.component: connect
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.technology: dbe-data-tier-apps
ms.custom: ''
ms.workload: data-management
ms.topic: article
ms.date: 08/09/2017
ms.author: genemi
ms.openlocfilehash: 33df5e13dcdeb205a1dbc9fa9c1a5dc7efc754c2
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 資料庫的連接模組

本文提供連接模組的下載連結或*驅動程式*，可以使用用戶端程式與互動[Microsoft SQL Server](../index.md)，並使用其雲端中的兩個[AzureSQL Database](http://docs.microsoft.com/azure/sql-database/)。 驅動程式可供各種不同的程式語言中，執行下列作業系統上：

- Linux (Ubuntu)
- MacOS
- 視窗


#### <a name="oop-to-relational-mismatch"></a>OOP 到關聯式的不相符

*關聯式*： 通常在物件導向程式設計 (OOP) 語言撰寫的用戶端程式使用的 SQL 驅動程式會傳回查詢的資料會於物件導向多個關聯式格式。 C# 中使用 ADO.NET 是其中一個範例。 OOP 關聯式格式不符合有時候讓 OOP 的程式碼更不容易撰寫，並了解。

*ORM*： 其他驅動程式或架構傳回查詢的資料 OOP 格式，避免不相符。 這些驅動程式的運作方式必須是類別已被定義之符合特定的 SQL 資料表的資料行。 然後此驅動程式會執行*物件關聯式對應*(ORM) 做為類別的執行個體傳回查詢的資料。 Microsoft 的 Entity Framework (EF) 的 C# 和 java，休眠是兩個範例。

現有的文章會專用於這兩種連線的驅動程式的另一節。


<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>驅動程式的關聯式存取


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  http://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is http://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->


| 語言 | 下載 SQL 驅動程式 |
| :------- | :---------------------- |
| C#       | [ADO.NET](http://www.microsoft.com/net/download/)<br /><br />[.NET core，for Linux Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, for MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET core for Windows](https://www.microsoft.com/net/core) |
| C++      | [ODBC](http://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server) |
| Java     | [JDBC](http://www.microsoft.com/download/details.aspx?id=55539) |
| Node.js  | [Node.js 驅動程式、 安裝指示](http://docs.microsoft.com/sql/connect/node-js/step-1-configure-development-environment-for-node-js-development) |
| PHP      | *作業系統：*<br /><br />[Windows PHP driver](https://www.microsoft.com/download/details.aspx?id=55642)<br />[從 Github 的 Linux 或 macOS PHP driver](http://github.com/Microsoft/msphpsql/) |
| Python   | [pyodbc、 安裝指示](http://docs.microsoft.com/sql/connect/python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development)<br />[下載 ODBC](http://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server) |
| Ruby     | [拼音驅動程式、 安裝指示](https://docs.microsoft.com/sql/connect/ruby/step-1-configure-development-environment-for-ruby-development)<br />[Ruby 的下載頁面](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |


<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 存取驅動程式


下表列出的物件關聯式對應 (ORM) 架構用戶端應用程式用來連接到 Microsoft SQL 資料庫的範例。


| 語言 | ORM 驅動程式下載 |
| :------- | :------------------ |
| C# | [Entity Framework Core](http://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x 或更新版本)](http://docs.microsoft.com/ef/) |
| Java | [休眠 ORM](http://hibernate.org/orm)|
| PHP | [最具有說服力 ORM，隨附於 Laravel 安裝](http://laravel.com/docs/) |
| Node.js | [Sequelize ORM](http://docs.sequelizejs.com) |
| Python | [Django](http://www.djangoproject.com/) |
| Ruby | [Ruby 滑軌上](http://rubyonrails.org/) |
| &nbsp; | <br /> |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>建置應用程式的網頁


[http://aka.ms/sqldev](http://aka.ms/sqldev) 將帶您到一組*建置的應用程式*網頁。 網頁提供許多組合的程式設計語言、 作業系統和 SQL 連線的驅動程式的相關資訊。 建置應用程式的網頁所提供的資訊，其中包括下列項目：

- 如何從一開始，每個組合語言 + 作業系統 + 驅動程式快速入門的詳細資料。
    - 安裝最新的 SQL 連接驅動程式的指示。
- 程式碼範例，每個下列項目：
    - 物件關聯的程式碼範例。
    - ORM 程式碼範例。
    - 資料行存放區索引示範更快的效能。


#### <a name="first-page-of-build-an-app-webpages"></a>第一個頁面上，建置的應用程式的網頁

![建置應用程式的網頁，第一個頁面的螢幕擷取畫面][image-ref-163-buildanapp-webpages-first-page]


#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>功能表 Java-Ubuntu，建置的應用程式的網頁

![建置應用程式的網頁，功能表 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]


&nbsp;


## <a name="related-links"></a>相關連結

- [程式碼範例連接到 Azure SQL Database 在雲端中，使用 Java 和其他語言](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。


<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
