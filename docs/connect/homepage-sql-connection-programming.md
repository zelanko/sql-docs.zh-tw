---
title: SQL 用戶端程式設計的首頁 |Microsoft Docs
description: 包含適用于多種語言和作業系統組合之下載和檔的已標注連結的中樞頁面，用於連接到 SQL Server 或 Azure SQL Database。
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451857"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server 用戶端程式設計的首頁


歡迎來到我們的首頁，瞭解用戶端程式設計如何與 Microsoft SQL Server 互動，以及如何在雲端中 Azure SQL Database。 本文提供下列資訊：

- 列出並描述可用的語言和驅動程式組合。
    - 系統會提供適用于 Linux （Ubuntu 和其他）、MacOS 和 Windows 作業系統的資訊。
- 提供每個組合的詳細檔連結。
- 在適當的情況下，顯示特定語言之階層式檔的區域和子領域。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何指定的語言中，連接到 SQL Server 的程式碼與連接至 Azure SQL Database 的程式碼幾乎完全相同。

如需連接到 Azure SQL Database 連線字串的詳細資訊，請參閱：

- [使用 .Net Core （C#）來查詢 Azure SQL 資料庫](/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 如目錄中的先前文章附近的其他 Azure SQL Database，關於其他語言。 例如，請參閱[使用 PHP 查詢 AZURE SQL 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>建立應用程式網頁

我們的*組建應用程式*網頁提供了程式碼範例，以及其他格式的設定資訊。 如需詳細資訊，請參閱本文稍後的[標記為*組建-應用程式網站*一節](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>用戶端程式的語言和驅動程式


在下表中，每個語言映射都是使用語言搭配 SQL Server 的詳細資訊連結。 每個連結都會跳到本文中的後續章節。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C#標誌][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework，屬於 .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 標誌][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node .js 標誌][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 標誌][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 標誌][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 標誌][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>下載並安裝

下列文章專門用於下載和安裝各種 SQL 連接驅動程式，以供程式設計語言使用：

- [SQL Server 驅動程式](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#標誌][image-ref-320-csharp] C#使用 ADO.NET

.NET managed 語言（例如C#和 Visual Basic）是最常見的 ADO.NET 使用者。 *ADO.NET*是 .NET Framework 類別子集的一般名稱。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 ADO.NET 連接到 SQL 的概念證明](./ado-net/step-3-connect-sql-ado-net.md) | 著重于連接和查詢 SQL Server 的小型程式碼範例。 |
| [使用 ADO.NET 彈性地連接到 SQL](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | 程式碼範例中的重試邏輯，因為連接有時可能會遇到連線中斷的情況。<br /><br />重試邏輯適用于透過網際網路維護的連接到任何雲端資料庫，例如 Azure SQL Database。 |
| [Azure SQL Database：示範如何在 Windows/Linux/macOS 上使用 .NET Core 來建立C#程式，以進行連線和查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 範例。 |
| [組建-應用程式： C#、ADO.NET、Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

|||
| :-- | :-- |
| [C#使用 ADO.NET](./ado-net/index.md)| 檔的根目錄。 |
| [命名空間： System.object](https://docs.microsoft.com/dotnet/api/system.data) | 用於 ADO.NET 的一組類別。 |
| [命名空間：System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 最直接是 ADO.NET 中心的一組類別。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 標誌][image-ref-333-ef] 使用 C Entity Framework （EF）&#x23;

Entity Framework （EF）提供物件關聯式對應（ORM）。 ORM 可讓您的物件導向程式設計（OOP）原始程式碼更輕鬆地操作從關聯式 SQL 資料庫中抓取的資料。

EF 具有與下列技術的直接或間接關聯性：

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)或[LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 語言語法增強功能，例如中  C#的 => 運算子。
- 便利的程式，會產生對應至 SQL 資料庫中資料表之類別的原始程式碼。 例如， [edmgen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)。


#### <a name="original-ef-and-new-ef"></a>原始 EF 和新的 EF

[Entity Framework 的起始頁](https://docs.microsoft.com/ef/)引進 EF，其描述如下所示：

- Entity Framework 是物件關聯式對應程式（O/RM），可讓 .NET 開發人員使用 .NET 物件來處理資料庫。 這不需要開發人員通常需要撰寫的大部分資料存取原始程式碼。

*Entity Framework*是兩個不同的原始程式碼分支所共用的名稱。 一個 EF 分支較舊，而且其原始程式碼現在可以由公開維護。 另一個 EF 是新的。 接下來會說明這兩個 EFs：

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft 首次於2008年8月發行 EF。 Microsoft 于2015年3月宣佈，EF 6.x 是 Microsoft 開發的最終版本。 Microsoft 已將原始程式碼發行至公用網域。<br /><br />一開始 EF 是 .NET Framework 的一部分。 但是 EF 6.x 已從 .NET Framework 中移除。<br /><br />[Github 上的 EF 6.x 原始碼，位於存放庫*aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft 已于2016年6月發行新開發的 EF Core。 EF Core 是針對更佳的彈性和可攜性而設計的。 EF Core 只能在 Microsoft Windows 以外的作業系統上執行。 而且 EF Core 可以與資料庫互動，而不只是 Microsoft SQL Server 和其他關係資料庫。<br /><br />**C&#x23;程式碼範例：**<br />[使用 Entity Framework Core 的消費者入門](https://docs.microsoft.com/ef/core/get-started/index)<br />[開始在具有現有資料庫的 .NET Framework 上使用 EF Core](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 和相關技術的功能強大，對於想要掌握整個領域的開發人員而言，這是很重要的。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 標誌][image-ref-330-java] JAVA 和 JDBC

Microsoft 提供了 JAVA 資料庫連線（JDBC）驅動程式，可與 SQL Server 搭配使用（當然也適用于 Azure SQL Database）。 這是類型 4 JDBC 驅動程式，可以透過標準 JDBC 應用程式介面 (API) 來提供資料庫連接。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [程式碼範例](./jdbc/code-samples/index.md) | 教資料類型、結果集和大型資料的程式碼範例。 |
| [連接 URL 範例](./jdbc/connection-url-sample.md) | 描述如何使用連接 URL 來連接到 SQL Server。 然後使用它來使用 SQL 語句來取出資料。 |
| [資料來源範例](./jdbc/data-source-sample.md) | 描述如何使用資料來源連接到 SQL Server。 然後使用預存程式來取出資料。 |
| [使用 JAVA 查詢 Azure SQL 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 範例。 |
| [使用 Ubuntu 上的 SQL Server 建立 JAVA 應用程式](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

JDBC 檔包含下列主要區域：

|||
| :-- | :-- |
| [JAVA 資料庫連線（JDBC）](./jdbc/index.md) | JDBC 檔的根目錄。 |
| [參考](./jdbc/reference/index.md) | 介面、類別和成員。 |
| [JDBC SQL Driver 程式設計指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 標誌][image-ref-340-node] Node.js

使用 node.js，您可以從 Windows、Linux 或 Mac 連接到 SQL Server。 我們的 node.js 檔的根目錄位於[這裡](./node-js/index.md)。

適用于 SQL Server 的 node.js 連接驅動程式會在 JavaScript 中執行。 驅動程式會使用 TDS 通訊協定，這是所有新式 SQL Server 版本所支援的。 此驅動程式是開放原始碼專案，[可在 Github 上](https://tediousjs.github.io/tedious/)取得。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 Node.js 連接到 SQL 的概念證明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 用來連接到 SQL Server 及執行查詢的裸機原始程式碼。 |
| [Azure SQL database：使用 node.js 進行查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 雲端中 Azure SQL Database 的範例。 |
| [建立要在 macOS 上使用 SQL Server 的 node.js 應用程式](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBCC++ 

![ODBC 標誌][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

開放式資料庫連接（ODBC）是在二十年代開發，而且它比較舊 .NET Framework。 ODBC 的設計可獨立于任何特定的資料庫系統，並與作業系統無關。

多年來，許多 ODBC 驅動程式都是由 Microsoft 內外的群組所建立和發行。 驅動程式的範圍牽涉到數種用戶端程式設計語言。 資料目標的清單遠高於 SQL Server。

某些其他連接驅動程式會在內部使用 ODBC。

#### <a name="code-example"></a>程式碼範例

- [使用 ODBC 的 C++ 程式碼範例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>檔大綱

本節中的 ODBC 內容著重于從C++存取 SQL Server 或 Azure SQL Database。 下表列出 ODBC 主要檔的大致大綱。


| 區域 | 區域 | Description |
| :--- | :------ | :---------- |
| [ODBCC++](./odbc/index.md) | 檔的根目錄。 |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | 在 Linux 或 MacOS 作業系統上使用 ODBC 的相關資訊。 |
| [Windows](./odbc/windows/index.md)     | &nbsp; | 在 Windows 作業系統上使用 ODBC 的相關資訊。 |
| [管理](../odbc/admin/index.md) | &nbsp; | 管理 ODBC 資料來源的系統管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 由 Microsoft 建立及提供的各種 ODBC 驅動程式。 |
| [概念和參考](../odbc/reference/index.md) | &nbsp; | 有關 ODBC 介面的概念資訊，以及傳統的參考。 |
| &nbsp; " | [附錄](../odbc/reference/appendixes/index.md)    | 狀態轉換資料表、ODBC 資料指標程式庫等。 |
| &nbsp; " | [開發應用程式](../odbc/reference/develop-app/index.md)  | 函式、控制碼及其他更多功能。 |
| &nbsp; " | [開發驅動程式](../odbc/reference/develop-driver/index.md) | 如果您有特製化的資料來源，如何開發自己的 ODBC 驅動程式。 |
| &nbsp; " | [安裝](../odbc/reference/install/index.md) | ODBC 安裝、子機碼等等。 |
| &nbsp; " | [語法](../odbc/reference/syntax/index.md)   | 適用于安裝程式、安裝程式、轉譯和資料存取的 Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 標誌][image-ref-360-php] PHP

您可以使用 PHP 與 SQL Server 進行互動。 PHP 檔的根目錄位於[這裡](./php/index.md)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 PHP 連接到 SQL 的概念證明](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 著重于連接和查詢 SQL Server 的小型程式碼範例。 |
| [使用 PHP 彈性地連接到 SQL](./php/step-4-connect-resiliently-to-sql-with-php.md) | 在程式碼範例中重試邏輯，因為透過網際網路和雲端的連線偶爾會遇到連接中斷的時刻。 |
| [Azure SQL database：使用 PHP 進行查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 範例。 |
| [建立 PHP 應用程式以在 RHEL 上使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 標誌][image-ref-370-python] Python


您可以使用 Python 與 SQL Server 進行互動。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 pyodbc 以 Python 連接到 SQL 的概念證明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 著重于連接和查詢 SQL Server 的小型程式碼範例。 |
| [Azure SQL database：使用 Python 進行查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 範例。 |
| [建立 PHP 應用程式，以在 SLES 上使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件集

| 區域 | Description |
| :--- | :---------- |
| [Python 至 SQL Server](./python/index.md) | 檔的根目錄。 |
| [pymssql 驅動程式](./python/pymssql/index.md) | Microsoft 不會維護或測試 pymssql 驅動程式。<br /><br />Pymssql 連接驅動程式是 SQL 資料庫的簡單介面，可用於 Python 程式。 Pymssql 是以 FreeTDS 為基礎，以提供 Python DB-API （PEP-249）介面來 Microsoft SQL Server。 |
| [pyodbc 驅動程式](./python/pyodbc/index.md)   | Pyodbc 連接驅動程式是一種開放原始碼 Python 模組，可讓您輕鬆存取 ODBC 資料庫。 它會實行 DB API 2.0 規格，但會封裝起來更 Pythonic 的便利性。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 標誌][image-ref-380-ruby] Ruby

您可以使用 Ruby 與 SQL Server 進行互動。 我們的 Ruby 檔的根目錄位於[這裡](./ruby/index.md)。

#### <a name="code-examples"></a>程式碼範例

|||
| :-- | :-- |
| [使用 Ruby 連接到 SQL 的概念證明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 著重于連接和查詢 SQL Server 的小型程式碼範例。 |
| [Azure SQL database：使用 Ruby 進行查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 範例。 |
| [建立要在 MacOS 上使用 SQL Server 的 Ruby 應用程式](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[建立-應用程式網站，適用于 SQL 用戶端開發](https://www.microsoft.com/sql-server/developer-get-started/)


在我們的[*組建應用*](https://www.microsoft.com/sql-server/developer-get-started/)程式網頁上，您可以從一長串的程式設計語言中選擇，以便連接到 SQL Server。 而您的用戶端程式可以執行各種不同的作業系統。

對於剛開始使用的開發人員而言，*組建應用程式*強調簡單和完整性。 這些步驟會說明下列工作：

1. 如何安裝 Microsoft SQL Server
2. 如何下載和安裝工具和驅動程式。
3. 如何根據您選擇的作業系統進行任何必要的設定。
4. 如何編譯提供的原始程式碼。
5. 如何執行程式。

接下來是網站上所提供詳細資料的幾個大致大綱：

#### <a name="java-on-ubuntu"></a>Ubuntu 上的 JAVA：

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟1.2 安裝 JAVA
    - 步驟1.3 安裝 JAVA 開發工具組（JDK）
    - 步驟1.4 安裝 Maven
2. 使用 SQL Server 建立 JAVA 應用程式
    - 步驟2.1 建立 JAVA 應用程式，以連接到 SQL Server 並執行查詢
    - 步驟2.2 建立 JAVA 應用程式，以使用受歡迎的架構休眠來連接到 SQL Server
3. 讓您的 JAVA 應用程式更快100倍
    - 步驟3.1 建立 JAVA 應用程式以示範資料行存放區索引

#### <a name="python-on-windows"></a>Windows 上的 Python：

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟1.2 安裝 Python
    - 步驟1.3 安裝 ODBC 驅動程式和 SQL 命令列公用程式，以進行 SQL Server
2. 使用 SQL Server 建立 Python 應用程式
    - 步驟2.1 安裝適用于 SQL Server 的 Python 驅動程式
    - 步驟2.2 為您的應用程式建立資料庫
    - 步驟2.3 建立 Python 應用程式，以連接到 SQL Server 並執行查詢
3. 讓您的 Python 應用程式更快100倍
    - 步驟3.1 使用 sqlcmd 建立具有5000000的新資料表
    - 步驟3.2 建立 Python 應用程式，以查詢此資料表並測量所花費的時間
    - 步驟3.3 測量執行查詢所需的時間
    - 步驟3.4 將資料行存放區索引新增至您的資料表
    - 步驟3.5 測量使用資料行存放區索引執行查詢所需的時間

下列螢幕擷取畫面可讓您瞭解我們的 SQL 開發檔網站看起來的樣子。

#### <a name="choose-a-language"></a>選擇語言：

![SQL Dev 網站，開始使用][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>選擇作業系統：

![SQL Dev 網站，JAVA Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他開發


本節提供有關其他開發選項的連結。 其中包括一般使用這些相同的語言來進行 Azure 開發。 此資訊的目標不僅僅是 Azure SQL Database 和 Microsoft SQL Server。

#### <a name="developer-hub-for-azure"></a>適用于 Azure 的開發人員中樞

- [適用于 Azure 的開發人員中樞](https://docs.microsoft.com/azure/)
- [適用于 .NET 開發人員的 Azure](https://docs.microsoft.com/dotnet/azure/)
- [適用于 JAVA 開發人員的 Azure](https://docs.microsoft.com/java/azure/)
- [適用于 node.js 開發人員的 Azure](https://docs.microsoft.com/nodejs/azure/)
- [適用于 Python 開發人員的 Azure](https://docs.microsoft.com/python/azure/)
- [在 Azure 中建立 PHP web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他語言

- [在 Windows 上使用 SQL Server 建立 Go 應用程式](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

