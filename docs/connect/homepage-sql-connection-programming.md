---
title: SQL 用戶端程式設計的首頁 |Microsoft 文件
description: 註解式連結來下載和文件的語言和作業系統，連線到 SQL Server 或 Azure SQL Database 的許多組合中樞 頁面。
author: MightyPen
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: meetb
ms.author: genemi
ms.openlocfilehash: cfb1ac82894ef8fed001077d54665c9f89239787
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306217"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>用戶端程式設計與 Microsoft SQL Server 首頁


歡迎使用我們的首頁，有關用戶端程式設計來與 Microsoft SQL Server，和雲端中的 Azure SQL Database 互動。 本文提供下列資訊：

- 列出並說明可用的語言和驅動程式組合。
    - 針對 Linux （Ubuntu 和其他項目）、 MacOS 和 Windows 作業系統提供的資訊。
- 提供每個組合的詳細文件的連結。
- 顯示在適當的區域和子區域的特定語言的階層式文件。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何給定的語言中，連接至 SQL Server 的程式碼是與連接到 Azure SQL Database 的程式碼幾乎完全相同。

如需連接到 Azure SQL Database 的連接字串的詳細資訊，請參閱：

- [使用.NET Core (C#) 來查詢 Azure SQL database](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 附近的其他語言的相關內容，上述資料表中發行項是其他 Azure SQL Database。 例如，請參閱[查詢 Azure SQL database 使用 PHP](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>建置應用程式的網頁

我們*建置的應用程式*網頁替代格式呈現程式碼範例，以及組態資訊。 如需詳細資訊，請參閱本文稍後[標示為區段*建置的應用程式網站*](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>語言和用戶端程式的驅動程式


下表中每個語言的映像會是與 SQL Server 中使用語言的詳細資料的連結。 每個連結會跳到本文中稍後的章節。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C# 標誌][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework 的.NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 標誌][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node.js 標誌][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![cpp 大加號][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 標誌][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 標誌][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![拼音標誌][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>下載與安裝

下列文件專用於下載及安裝不同的 SQL 連接驅動程式，以供程式設計語言：

- [SQL Server 驅動程式](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 標誌][image-ref-320-csharp] C# 使用 ADO.NET

.NET managed 語言，例如 C# 和 Visual Basic 中，是 ADO.NET 的最常見的使用者。 *ADO.NET*是.NET Framework 類別的子集的任意名稱。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [連接到使用 ADO.NET 的 SQL 的概念證明](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | 小的程式碼範例著重於連接和查詢 SQL Server。 |
| [彈性地連接到使用 ADO.NET 的 SQL](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | 請重試邏輯，在程式碼範例中，因為連接可能偶爾會遇到連線中斷的時段。<br /><br />重試邏輯也適用於維護透過網際網路到任何雲端資料庫，例如 Azure SQL database 的連線。 |
| [Azure SQL Database： 示範，說明如何使用.NET Core Windows/Linux/macOS 上建立的 C# 程式，用於連接及查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 範例。 |
| [組建的-應用程式： C# 中，ADO.NET 中，Windows](http://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

|||
| :-- | :-- |
| [C# 使用 ADO.NET](./ado-net/index.md)| 我們的文件的根節點。 |
| [命名空間： System.Data](http://docs.microsoft.com/dotnet/api/system.data) | 使用 ado.net 類別的一組。 |
| [命名空間： System.Data.SqlClient](http://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 一組類別是最直接的 ADO.NET 的中心。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 標誌][image-ref-333-ef] Entity Framework (EF) 與 C&#x23;

Entity Framework (EF) 提供物件關聯式對應 (ORM)。 ORM，方便您 Object-Oriented 程式設計 (OOP) 的原始碼來操作從 SQL 關聯式資料庫擷取的資料。

EF 具有直接或間接關聯性的下列技術：

- .NET Framework
- [LINQ to SQL](http://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)，或[LINQ to Entities](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 語言語法的增強功能，例如**=>** C# 中的運算子。
- 產生 SQL 資料庫中資料表的對應類別的原始程式碼好用的程式。 比方說， [EdmGen.exe](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)。


#### <a name="original-ef-and-new-ef"></a>原始的 EF 和新的 EF

[Entity Framework 的起始頁](http://docs.microsoft.com/ef/)介紹 EF 描述與下列類似：

- Entity Framework 是物件關聯式對應工具 (O/RM)，可讓.NET 開發人員使用.NET 物件的資料庫使用。 它不必將大部分的開發通常需要撰寫資料存取原始碼。

*Entity Framework*是由兩個不同的來源的程式碼分支所共用的名稱。 一個 EF 分支都是較舊的而現在可公開來維護其原始程式碼。 其他 EF 是新功能。 以下將說明兩個 EFs:

|     |     |
| :-- | :-- |
| [EF 6.x](http://docs.microsoft.com/ef/ef6/) | 首先，Microsoft 會在 2008 年 8 月發行 EF。 2015 年 3 月中 Microsoft 宣布的 EF 6.x 已像開發 Microsoft 的最終版本。 Microsoft 會發行到公用網域的原始程式碼。<br /><br />一開始 EF 是.NET Framework 的一部分。 但 EF 6.x 已從.NET Framework 中移除。<br /><br />[EF 6.x 原始碼 Github 儲存機制上的*aspnet/EntityFramework6*](http://github.com/aspnet/EntityFramework6) |
| [EF Core](http://docs.microsoft.com/ef/core/) | Microsoft 於 2016 年 6 月發行新開發的 EF Core。 EF Core 專為較佳的彈性和可攜性。 EF Core 可以執行超出只是 Microsoft Windows 作業系統上。 而且 EF Core 可以只 Microsoft SQL Server 以外的資料庫和其他關聯式資料庫互動。<br /><br />**C&#x23;程式碼範例：**<br />[開始使用 Entity Framework Core](https://docs.microsoft.com/ef/core/get-started/index)<br />[開始使用.NET Framework 與現有的資料庫上的 EF Core](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 和相關的技術是強大，而且開發人員想要主要的整個區域學到許多內容。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 標誌][image-ref-330-java] 使用 Java 和 JDBC

Microsoft 提供的 Java Database Connectivity (JDBC) 驅動程式使用具有 SQL Server （或使用 Azure SQL Database 的課程）。 它是類型 4 JDBC 驅動程式，並提供資料庫連接，透過標準的 JDBC 應用程式介面 (Api)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [程式碼範例](./jdbc/code-samples/index.md) | 教導有關資料類型，結果集和大型資料的程式碼範例。 |
| [連接 URL 範例](./jdbc/connection-url-sample.md) | 描述如何使用連接 URL 來連接到 SQL Server。 然後使用它使用 SQL 陳述式來擷取資料。 |
| [資料來源範例](./jdbc/data-source-sample.md) | 描述如何使用資料來源，連接到 SQL Server。 然後使用預存程序來擷取資料。 |
| [使用 Java 查詢 Azure SQL database](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 範例。 |
| [建立在 Ubuntu 上使用 SQL Server 的 Java 應用程式](http://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

JDBC 文件包含下列主要區域：

|||
| :-- | :-- |
| [Java 資料庫連線 (JDBC)](./jdbc/index.md) | JDBC 文件的根節點。 |
| [參考](./jdbc/reference/index.md) | 介面、 類別和成員。 |
| [JDBC SQL Driver 程式設計指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 標誌][image-ref-340-node] Node.js

Node.js 您可以從連接到 SQL Server Windows、 Linux 或 mac。 Node.js 文件的根是[這裡](./node-js/index.md)。

SQL Server 的 Node.js 連接驅動程式是在 JavaScript 中實作。 驅動程式會使用 TDS 通訊協定，這會受到所有現代化版本的 SQL Server。 驅動程式是開放原始碼專案， [github](http://tediousjs.github.io/tedious/)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [連接到使用 Node.js SQL 的概念證明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 最基本來源的程式碼連接至 SQL Server，以及執行查詢。 |
| [Azure SQL database： 查詢使用 Node.js](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | Azure SQL Database 在雲端中的範例。 |
| [建立使用 SQL Server 上 macOS Node.js 應用程式](http://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C + + ODBC 

![ODBC 標誌][image-ref-350-odbc] ![cpp 大加號][image-ref-322-cpp]

開放式資料庫連接 (ODBC) 所開發在 1990，和它之前的.NET Framework。 ODBC 被設計為獨立於任何特定資料庫的系統，且獨立的作業系統。

過去幾年許多 ODBC 驅動程式已建立並釋放群組內，並在 Microsoft 外。 驅動程式的範圍包括數種用戶端程式設計語言。 資料的目標清單完全超出 SQL Server。

其他連接驅動程式會在內部使用 ODBC。

#### <a name="code-example"></a>程式碼範例

- [使用 ODBC 的 c + + 程式碼範例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>文件大綱

本節中的 ODBC 內容著重於從 c + + 存取 SQL Server 或 SQL Azure。 下表列出近似的 ODBC 的主要文件大綱。


| 區域 | 子區域 | 描述 |
| :--- | :------ | :---------- |
| [C + + ODBC](./odbc/index.md) | 我們的文件的根節點。 |
| [Linux Mac](./odbc/linux-mac/index.md) | &nbsp; | Linux 或 MacOS 作業系統上使用 ODBC 的相關資訊。 |
| [視窗](./odbc/windows/index.md)     | &nbsp; | Windows 作業系統上使用 ODBC 的相關資訊。 |
| [系統管理](../odbc/admin/index.md) | &nbsp; | 管理 ODBC 資料來源的系統管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 各種 ODBC 驅動程式會建立並由 Microsoft 提供。 |
| [概念和參考](../odbc/reference/index.md) | &nbsp; | ODBC 介面，除了傳統的參考的概念性資訊。 |
| &nbsp; " | [附錄](../odbc/reference/appendixes/index.md)    | 轉換資料表、 ODBC 資料指標程式庫，以及更多的狀態。 |
| &nbsp; " | [開發應用程式](../odbc/reference/develop-app/index.md)  | 函式、 控制代碼，以及執行更多。 |
| &nbsp; " | [開發驅動程式](../odbc/reference/develop-driver/index.md) | 如何在開發您自己的 ODBC 驅動程式，如果您有特定的資料來源。 |
| &nbsp; " | [安裝](../odbc/reference/install/index.md) | ODBC 安裝、 子機碼，等等。 |
| &nbsp; " | [語法](../odbc/reference/syntax/index.md)   | 安裝程式、 安裝程式、 轉移和資料存取 Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 標誌][image-ref-360-php] PHP

您可以使用 PHP 來與 SQL Server 互動。 Node.js 文件的根是[這裡](./php/index.md)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [連接到使用 PHP 的 SQL 的概念證明](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 小的程式碼範例著重於連接和查詢 SQL Server。 |
| [彈性地連接到 SQL 與 PHP](./php/step-4-connect-resiliently-to-sql-with-php.md) | 請重試邏輯，在程式碼範例中，因為透過網際網路與雲端的連線可能偶爾會遇到連線中斷的時段。 |
| [Azure SQL database： 使用 PHP 來查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 範例。 |
| [建立使用 SQL Server 上 RHEL 的 PHP 應用程式](http://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 標誌][image-ref-370-python] Python


您可以使用 Python 與 SQL Server 互動。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [連接到 SQL 搭配使用 pyodbc Python 的概念證明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 小的程式碼範例著重於連接和查詢 SQL Server。 |
| [Azure SQL database： 查詢使用 Python](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 範例。 |
| [建立 SLES 上使用 SQL Server 的 PHP 應用程式](http://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

| 區域 | 描述 |
| :--- | :---------- |
| [SQL Server 的 Python](./python/index.md) | 我們的文件的根節點。 |
| [pymssql 驅動程式](./python/pymssql/index.md) | Microsoft 不會維護或測試 pymssql 驅動程式。<br /><br />Pymssql 連線驅動程式是一個簡單的介面與 SQL 資料庫，以供 Python 程式使用。 Pymssql 是建置基礎 freetds 才能使用 Microsoft SQL server 提供 Python DB API (PEP 249) 介面。 |
| [pyodbc 驅動程式](./python/pyodbc/index.md)   | Pyodbc 連線驅動程式是開放原始碼 Python 模組，簡化了存取 ODBC 資料庫。 它實作 DB API 2.0 規格中，但封裝使用更多的 Pythonic 便利性。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![拼音標誌][image-ref-380-ruby] Ruby

您可以使用 Ruby 與 SQL Server 互動。 拼音文件的根是[這裡](./ruby/index.md)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [連接到與 Ruby SQL 的概念證明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 小的程式碼範例著重於連接和查詢 SQL Server。 |
| [Azure SQL database： 使用 Ruby 查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 範例。 |
| [建立使用 SQL Server 上 MacOS Ruby 應用程式](http://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpwwwmicrosoftcomsql-serverdeveloper-get-started"></a>[針對 SQL 用戶端開發的應用程式建置的網站](http://www.microsoft.com/sql-server/developer-get-started/)


在我們[*建置的應用程式*](https://www.microsoft.com/sql-server/developer-get-started/)網頁，您可以選擇從一長串的程式設計語言來連接到 SQL Server。 用戶端程式可以執行各種不同的作業系統。

*建置的應用程式*強調簡化和完整性，開發人員剛開始使用。 步驟將說明下列工作：

1. 如何安裝 Microsoft SQL Server
2. 如何下載及安裝工具與驅動程式。
3. 如何進行任何必要的設定，視您所選擇的作業系統。
4. 如何提供的原始程式碼的編譯。
5. 如何執行程式。

接下來的幾個相近的外框網站上提供的詳細資料：

#### <a name="java-on-ubuntu"></a>在 Ubuntu 上 Java:

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟 1.2 安裝 Java
    - 步驟 1.3 安裝 Java Development Kit (JDK)
    - 步驟 1.4 安裝 Maven
2. 建立與 SQL Server 的 Java 應用程式
    - 步驟 2.1 建立連接至 SQL Server，並執行查詢的 Java 應用程式
    - 步驟 2.2 建立連接至 SQL Server 使用熱門架構休眠的 Java 應用程式
3. 讓更高達 100 倍的 Java 應用程式
    - 若要示範資料行存放區索引的步驟 3.1 建立 Java 應用程式

#### <a name="python-on-windows"></a>在 Windows 上的 Python:

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟 1.2 安裝 Python
    - 步驟 1.3 for SQL Server 安裝的 ODBC 驅動程式和 SQL 命令列公用程式
2. 建立與 SQL Server 的 Python 應用程式
    - 步驟 2.1 for SQL Server 安裝 Python 驅動程式
    - 步驟 2.2 建立您的應用程式的資料庫
    - 步驟 2.3 建立連接至 SQL Server，並執行查詢的 Python 應用程式
3. 更快，讓您的 Python 應用程式，高達 100 倍
    - 步驟 3.1 5 百萬個使用 sqlcmd 以建立新的資料表
    - 3.2 步驟建立的 Python 應用程式會查詢此資料表，並測量所花費的時間
    - 步驟 3.3 測量花費的時間來執行查詢
    - 3.4 步驟新增至您的資料表資料行存放區索引
    - 步驟 3.5 測量花費的時間來執行與資料行存放區索引的查詢

下列螢幕擷取畫面可讓您了解我們的 SQL 開發文件網站的外觀。

#### <a name="choose-a-language"></a>選擇的語言：

![SQL 開發人員網站開始][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>選擇的作業系統：

![SQL 開發人員網站，Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他開發


本章節提供有關開發的其他選項的連結。 這些包括 Azure 開發中一般使用這些相同的語言。 資訊會超出目標只 Azure SQL Database 和 Microsoft SQL Server。

#### <a name="developer-hub-for-azure"></a>Azure 的開發人員中心

- [Azure 的開發人員中心](http://docs.microsoft.com/azure/)
- [Azure.NET 開發人員](http://docs.microsoft.com/dotnet/azure/)
- [Azure 的 Java 開發人員](http://docs.microsoft.com/java/azure/)
- [Node.js 開發人員的 azure](http://docs.microsoft.com/nodejs/azure/)
- [Python 開發人員的 azure](http://docs.microsoft.com/python/azure/)
- [在 Azure 中建立的 PHP web 應用程式](http://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他語言

- [建立在 Windows 上使用 SQL Server 移至應用程式](http://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

