---
title: SQL 用戶端程式設計的首頁 |Microsoft Docs
description: 下載和語言和作業系統，連線到 SQL Server 或 Azure SQL Database 的多個組合文件註解連結的 [中樞] 頁面。
author: MightyPen
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: meetb
ms.author: genemi
ms.openlocfilehash: e2c3da2ba71661602f69f85f5eb79ba6d550be9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633796"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>用戶端程式設計 Microsoft SQL server 首頁


歡迎使用我們的首頁，關於用戶端程式設計來使用 Microsoft SQL Server，和在雲端中的 Azure SQL database 進行互動。 本文提供下列資訊：

- 列出並說明可用的語言和驅動程式組合。
    - 適用於 Linux （Ubuntu 和其他項目）、 MacOS 和 Windows 作業系統提供資訊。
- 提供每個組合的詳細文件的連結。
- 在適當的地方，會顯示區域和子區域的特定語言的階層式文件。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何給定的語言中，連接至 SQL Server 的程式碼會連接到 Azure SQL Database 的程式碼幾乎完全相同。

如需有關連接到 Azure SQL Database 的連接字串的詳細資訊，請參閱：

- [使用.NET Core (C#) 來查詢 Azure SQL database](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 附近的其他語言的相關內容，上述資料表中發行項是其他 Azure SQL Database。 比方說，請參閱 <<c0> [ 使用 PHP 查詢 Azure SQL database](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>建置的應用程式網頁

我們*建置的應用程式*網頁呈現程式碼範例，以及組態資訊的替代格式。 如需詳細資訊，請參閱本文稍後[標示為區段*建置的應用程式網站*](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>語言和用戶端程式的驅動程式


下表中，每個語言的映像會是有關使用使用 SQL Server 的語言的詳細資料的連結。 每個連結會跳到本文中稍後的章節。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C# 標誌][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM 的 Entity Framework、.NET framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 標誌][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node.js 標誌][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![cpp 回票價][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 標誌][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 標誌][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 標誌][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>下載及安裝完成

下列文件用來下載並安裝各種不同的 SQL 連接驅動程式，以供程式設計語言：

- [SQL Server 驅動程式](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 標誌][image-ref-320-csharp] C# 使用 ADO.NET

.NET managed 語言，例如 C# 和 Visual Basic 中，是 ADO.NET 的最常見的使用者。 *ADO.NET*是.NET Framework 類別的子集的一般名稱。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 ADO.NET 連接到 SQL 的概念證明](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | 小型程式碼範例著重於連接和查詢 SQL Server。 |
| [使用 ADO.NET 彈性地連接到 SQL](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | 因為連線可能偶爾會遇到的連線中斷，請重試邏輯的程式碼範例中。<br /><br />重試邏輯也適用於維護透過網際網路到任何雲端資料庫，例如 Azure SQL database 的連線。 |
| [Azure SQL Database： 示範如何在 Windows/Linux/macOS 上使用.NET Core 建立 C# 程式，來連線及查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 的範例。 |
| [組建的-應用程式： C# 中，ADO.NET 中，Windows](http://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

|||
| :-- | :-- |
| [C# 使用 ADO.NET](./ado-net/index.md)| 我們的文件的根目錄。 |
| [命名空間： System.Data](http://docs.microsoft.com/dotnet/api/system.data) | 一組用於 ADO.NET 的類別。 |
| [命名空間：System.Data.SqlClient](http://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 一組類別是最直接的 ADO.NET 的中心。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 標誌][image-ref-333-ef] 使用 c# 的 entity Framework (EF)&#x23;

Entity Framework (EF) 提供物件關聯式對應 (ORM)。 ORM 容易操作關聯式 SQL 資料庫中已擷取的資料物件導向程式設計 (OOP) 原始程式碼。

EF 有直接或間接的關聯性，使用下列技術：

- .NET Framework
- [LINQ to SQL](http://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)，或[LINQ to Entities](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 語言語法增強功能，例如**=>** C# 中的運算子。
- 針對對應至您的 SQL database 中的資料表類別產生原始程式碼的實用程式。 比方說， [EdmGen.exe](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)。


#### <a name="original-ef-and-new-ef"></a>原始的 EF 和新的 EF

[Entity Framework 的起始頁](http://docs.microsoft.com/ef/)介紹 EF 的描述如下所示：

- Entity Framework 是物件關聯式對應程式 (O/RM)，可讓.NET 開發人員使用使用.NET 物件的資料庫。 它可免除大部分開發人員通常需要撰寫資料存取原始碼的需求。

*Entity Framework*是共用的兩個不同來源的程式碼分支的名稱。 其中一個的 EF 分支是更舊版本，和其原始碼現在可以維護由公用。 其他的 EF 是新功能。 以下將說明兩個 EFs:

|     |     |
| :-- | :-- |
| [EF 6.x](http://docs.microsoft.com/ef/ef6/) | 首先，Microsoft 會在 2008 年八月發行 EF。 在 2015 年 3 月 Microsoft 宣佈了 EF 6.x 是像在開發 Microsoft 的最終版本。 Microsoft 發行的原始程式碼到公用網域。<br /><br />一開始 EF 是.NET Framework 的一部分。 但 EF 6.x 已從.NET Framework 中移除。<br /><br />[在 Github 存放庫中的 EF 6.x 來源程式碼*aspnet/EntityFramework6*](http://github.com/aspnet/EntityFramework6) |
| [EF Core](http://docs.microsoft.com/ef/core/) | Microsoft 在 2016 年 6 月發行新開發的 EF Core。 EF Core 被設計用於較佳的彈性和可攜性。 EF Core 可以執行超出只是 Microsoft Windows 作業系統上。 而且 EF Core 可以只是 Microsoft SQL Server 以外的資料庫和其他關聯式資料庫互動。<br /><br />**C&#x23;程式碼範例：**<br />[Entity Framework Core 使用者入門](https://docs.microsoft.com/ef/core/get-started/index)<br />[與現有的資料庫的.NET Framework 上的 EF Core 使用者入門](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 及相關的技術強大，並很多開發人員想要精通的整個區域，了解。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 標誌][image-ref-330-java] Java 和 JDBC

Microsoft 提供的 Java Database Connectivity (JDBC) 驅動程式與 SQL Server （或使用 Azure SQL Database 的課程） 使用。 這是類型 4 JDBC 驅動程式，可以透過標準 JDBC 應用程式介面 (API) 來提供資料庫連接。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [程式碼範例](./jdbc/code-samples/index.md) | 教導資料型別，結果集和大型資料相關的程式碼範例。 |
| [連接 URL 範例](./jdbc/connection-url-sample.md) | 描述如何使用連接 URL 來連接到 SQL Server。 然後使用它來使用 SQL 陳述式來擷取資料。 |
| [資料來源範例](./jdbc/data-source-sample.md) | 描述如何使用資料來源連接到 SQL Server。 然後使用預存程序來擷取資料。 |
| [使用 Java 查詢 Azure SQL database](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 的範例。 |
| [建立 Ubuntu 上使用 SQL Server 的 Java 應用程式](http://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

JDBC 文件包含下列主要區域：

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | JDBC 文件的根目錄。 |
| [參考](./jdbc/reference/index.md) | 介面、 類別和成員。 |
| [JDBC SQL Driver 程式設計指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 標誌][image-ref-340-node] Node.js

使用 Node.js 您可以連接到 SQL Server 從 Windows、 Linux 或 mac。 我們的 Node.js 文件的根[此處](./node-js/index.md)。

SQL Server 的 Node.js 連線驅動程式是以 JavaScript 進行實作。 驅動程式會使用 TDS 通訊協定，所有現代化版本的 SQL Server 支援。 驅動程式是開放原始碼專案，[可在 Github 上](http://tediousjs.github.io/tedious/)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 Node.js 連接到 SQL 的概念證明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 最基本來源連接到 SQL Server 和執行查詢的程式碼。 |
| [Azure SQL database： 使用 Node.js 查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 在雲端中的 Azure SQL Database 的範例。 |
| [建立 Node.js 應用程式，以在 macOS 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C + + ODBC 

![ODBC 標誌][image-ref-350-odbc] ![cpp 回票價][image-ref-322-cpp]

開放式資料庫連接 (ODBC) 所開發，1990 年代，以及它之前的.NET Framework。 ODBC 被設計為獨立於任何特定的資料庫系統，且獨立的作業系統。

多年來許多 ODBC 驅動程式已建立並發行 Microsoft 內外的群組。 驅動程式各種牽涉到數種用戶端程式設計語言。 資料目標清單遠遠超越了 SQL Server。

其他連線能力驅動程式會在內部使用 ODBC。

#### <a name="code-example"></a>程式碼範例

- [使用 ODBC 的 c + + 程式碼範例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>文件大綱

在本節中的 ODBC 內容著重於從 c + + 存取 SQL Server 或 Azure SQL Database。 下表列出 ODBC 的主要文件的概略大綱。


| 區域 | 子區域 | Description |
| :--- | :------ | :---------- |
| [C + + ODBC](./odbc/index.md) | 我們的文件的根目錄。 |
| [Linux Mac](./odbc/linux-mac/index.md) | &nbsp; | 在 Linux 或 MacOS 作業系統上使用 ODBC 的相關資訊。 |
| [視窗](./odbc/windows/index.md)     | &nbsp; | Windows 作業系統上使用 ODBC 的相關資訊。 |
| [管理](../odbc/admin/index.md) | &nbsp; | 管理 ODBC 資料來源的系統管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 各種 ODBC 驅動程式會建立並由 Microsoft 所提供。 |
| [概念和參考](../odbc/reference/index.md) | &nbsp; | ODBC 介面，除了傳統的參考相關的概念資訊。 |
| &nbsp; " | [附錄](../odbc/reference/appendixes/index.md)    | 狀態轉換資料表、 ODBC 資料指標程式庫，和更多功能。 |
| &nbsp; " | [開發應用程式](../odbc/reference/develop-app/index.md)  | 函式、 控制代碼，以及其他等等。 |
| &nbsp; " | [開發驅動程式](../odbc/reference/develop-driver/index.md) | 如何開發您自己的 ODBC 驅動程式，如果您有特定的資料來源。 |
| &nbsp; " | [安裝](../odbc/reference/install/index.md) | ODBC 安裝、 子機碼，和更多功能。 |
| &nbsp; " | [語法](../odbc/reference/syntax/index.md)   | 安裝程式，安裝程式、 轉譯和資料存取 Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 標誌][image-ref-360-php] PHP

您可以使用 PHP 來與 SQL Server 互動。 PHP 文件的根[此處](./php/index.md)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 PHP 連接到 SQL 的概念證明](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 小型程式碼範例著重於連接和查詢 SQL Server。 |
| [使用 PHP 彈性地連接到 SQL](./php/step-4-connect-resiliently-to-sql-with-php.md) | 因為透過網際網路和雲端的連線可以偶爾會遇到的連線中斷，請重試邏輯的程式碼範例中。 |
| [Azure SQL database： 使用 PHP 來查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 的範例。 |
| [建立使用 RHEL 上的 SQL Server 的 PHP 應用程式](http://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 標誌][image-ref-370-python] Python


您可以使用 Python 與 SQL Server 互動。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [連接到使用 pyodbc Python 與 SQL 的概念證明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 小型程式碼範例著重於連接和查詢 SQL Server。 |
| [Azure SQL database： 使用 Python 查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 的範例。 |
| [建立在 SLES 上使用 SQL Server 的 PHP 應用程式](http://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

| 區域 | Description |
| :--- | :---------- |
| [SQL server 的 Python](./python/index.md) | 我們的文件的根目錄。 |
| [pymssql 驅動程式](./python/pymssql/index.md) | Microsoft 不會維護或測試 pymssql 驅動程式。<br /><br />Pymssql 連接驅動程式是 SQL database，以供 Python 程式的簡單介面。 Pymssql 建置上 FreeTDS 來提供 Microsoft SQL server 的 Python DB API (PEP 249) 介面。 |
| [pyodbc 驅動程式](./python/pyodbc/index.md)   | Pyodbc 連接驅動程式會簡化存取 ODBC 資料庫的開放原始碼 Python 模組。 但實作 DB API 2.0 規格，富含更多 Pythonic 的便利性。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 標誌][image-ref-380-ruby] Ruby

您可以使用 Ruby 來與 SQL Server 互動。 Ruby 文件的根[此處](./ruby/index.md)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 Ruby 連接到 SQL 的概念證明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 小型程式碼範例著重於連接和查詢 SQL Server。 |
| [Azure SQL database︰ 使用 Ruby 來查詢](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 的範例。 |
| [建立 Ruby 應用程式，以在 MacOS 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 組態資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpwwwmicrosoftcomsql-serverdeveloper-get-started"></a>[建置的應用程式的網站，SQL 用戶端開發](http://www.microsoft.com/sql-server/developer-get-started/)


在我們[*建置的應用程式*](https://www.microsoft.com/sql-server/developer-get-started/)網頁，您可以選擇從一長串的程式設計語言連線到 SQL Server。 而用戶端程式可以執行各種不同的作業系統。

*建置的應用程式*強調的開發人員剛開始的簡易性和完整性。 步驟會說明下列工作：

1. 如何安裝 Microsoft SQL Server
2. 如何下載及安裝工具和驅動程式。
3. 如何進行任何必要的設定，視您所選擇的作業系統。
4. 如何將提供的原始程式碼編譯。
5. 如何執行程式。

接下來的幾個近似的外框輪廓的網站上提供詳細資料：

#### <a name="java-on-ubuntu"></a>在 Ubuntu 上的 Java:

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟 1.2 安裝 Java
    - 步驟 1.3 安裝 Java Development Kit (JDK)
    - 步驟 1.4 安裝 Maven
2. 使用 SQL Server 中建立 Java 應用程式
    - 步驟 2.1 建立 Java 應用程式，連接至 SQL Server 執行查詢
    - 步驟 2.2 建立連接至使用受歡迎的架構休眠的 SQL Server 的 Java 應用程式
3. 更快做出 100 倍之多的 Java 應用程式
    - 步驟 3.1 建立 Java 應用程式來示範資料行存放區索引

#### <a name="python-on-windows"></a>在 Windows 上的 Python:

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟 1.2 安裝 Python
    - 步驟 1.3 安裝 SQL server 的 ODBC 驅動程式和 SQL 命令列公用程式
2. 使用 SQL Server 中建立 Python 應用程式
    - 步驟 2.1 安裝 Python driver for SQL Server
    - 步驟 2.2 建立您的應用程式的資料庫
    - 步驟 2.3 建立 Python 應用程式，連接到 SQL Server，並執行查詢
3. 加速您的 Python 應用程式，100 倍之多
    - 步驟 3.1 5 百萬個使用 sqlcmd 以建立新的資料表
    - 步驟 3.2 建立 Python 應用程式來查詢此資料表，以及測量所花費的時間
    - 步驟 3.3 量值來執行查詢所花費
    - 步驟 3.4 新增至您的資料表資料行存放區索引
    - 步驟 3.5 測量執行查詢的資料行存放區索引需要多久

下列螢幕擷取畫面可讓您了解我們的 SQL 開發文件網站的外觀。

#### <a name="choose-a-language"></a>選擇語言：

![SQL 開發人員網站，開始使用][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>選擇的作業系統：

![SQL 開發人員網站，Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他開發


本節提供關於其他開發選項的連結。 其中包括適用於 Azure 的開發中一般使用這些相同的語言。 資訊不僅只是 Azure SQL Database 和 Microsoft SQL Server 為目標。

#### <a name="developer-hub-for-azure"></a>適用於 Azure 的開發人員中樞

- [適用於 Azure 的開發人員中樞](http://docs.microsoft.com/azure/)
- [適用於.NET 開發人員的 azure](http://docs.microsoft.com/dotnet/azure/)
- [適用於 Java 開發人員的 azure](http://docs.microsoft.com/java/azure/)
- [適用於 Node.js 開發人員的 azure](http://docs.microsoft.com/nodejs/azure/)
- [適用於 Python 開發人員的 azure](http://docs.microsoft.com/python/azure/)
- [在 Azure 中建立 PHP web 應用程式](http://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他語言

- [建立 Go 應用程式在 Windows 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

