---
title: SQL 用戶端程式設計的首頁 | Microsoft Docs
description: 包含適用於連線到 SQL Server 或 Azure SQL Database 的不同語言和作業系統的下載項目和文件之已註解連結的頁面。
author: David-Engel
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: v-daenge
ms.openlocfilehash: 19dafa831f6763c5c2da5b54f14326db38372be4
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243410"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server 用戶端程式設計的首頁


歡迎來到我們的首頁，了解如何以用戶端程式設計與 Microsoft SQL Server 及在雲端的 Azure SQL Database 互動。 本文提供下列資訊：

- 列出並描述可用的語言和驅動程式組合。
  - 提供的作業系統資訊包括 Linux (Ubuntu 和其他)、macOS 和 Windows。
- 提供每個組合的詳細文件連結。
- 在適當情況下，顯示特定語言階層式文件的區域和子區域。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何給定的語言中，連線至 SQL Server 的程式碼與連線至 Azure SQL Database 的程式碼幾乎完全相同。

如需連線至 Azure SQL Database 連接字串的詳細資訊，請參閱：

- [使用 .NET Core (C#) 查詢 Azure SQL 資料庫](/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 在目錄中位於先前文章附近，關於其他語言的其他 Azure SQL Database 文章。 例如，請參閱[使用 PHP 查詢 Azure SQL 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>Build-an-app 網頁

我們的 *Build-an-app* 網頁呈現程式碼範例和設定資訊 (以替代性格式)。 如需詳細資訊，請參閱本文稍後[標示為「Build-an-app 網站」  的小節](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>用戶端程式的語言和驅動程式


在下表中，每個語言的影像，都是使用該語言搭配 SQL Server 的詳細資料連結。 每個連結都會跳到本文中的後續章節。

:::row:::
    :::column:::
        [![C# 標誌][image-ref-320-csharp]](#an-110-ado-net-docu)  

        [![Node.js 標誌][image-ref-340-node]](#an-140-node-js-docu)  

        [![Python 標誌][image-ref-370-python]](#an-180-python-docu)  
    :::column-end:::
    :::column:::
        [![.NET Framework 的 ORM Entity Framework][image-ref-333-ef]](#an-116-csharp-ef-orm)  

        [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu)  

        [![Ruby 標誌][image-ref-380-ruby]](#an-190-ruby-docu)  
    :::column-end:::
    :::column:::
        [![Java 標誌][image-ref-330-java]](#an-130-jdbc-docu)  

        [![PHP 標誌][image-ref-360-php]](#an-170-php-docu)  
    :::column-end:::
:::row-end:::

#### <a name="downloads-and-installs"></a>下載並安裝

下列文章專門用於下載並安裝各種 SQL 連線驅動程式，以供程式設計語言使用：

- [SQL Server 驅動程式](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 標誌][image-ref-320-csharp] 使用 ADO.NET 的 C#

.NET 受控語言 (例如 C# 和 Visual Basic) 是最常見的 ADO.NET 使用者。 *ADO.NET* 是 .NET Framework 類別子集的非正式名稱。

#### <a name="code-examples"></a>程式碼範例

| 範例 | 描述 |
| :-- | :-- |
| [使用 ADO.NET 連接到 SQL 的概念證明](./ado-net/step-3-connect-sql-ado-net.md) | 著重在連線和查詢 SQL Server 的一小段程式碼範例。 |
| [使用 ADO.NET 彈性地連接到 SQL](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | 重試程式碼範例中的邏輯，因為連線偶爾會發生失去連線能力。<br /><br />重試邏輯很適合用於透過網際網路維持連線到雲端資料庫的連線，例如連線到 Azure SQL Database。 |
| [Azure SQL Database：示範如何在 Windows/Linux/macOS 上使用 .NET Core 建立 C# 程式，以連線並查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 範例。 |
| [Build-an-app：C#、ADO.NET、Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件

| 區域 | 說明 |
| :-- | :-- |
| [使用 ADO.NET 的 C#](./ado-net/index.md)| 我們文件的根頁面。 |
| [命名空間：System.Data](https://docs.microsoft.com/dotnet/api/system.data) \(部分機器翻譯\) | 用於 ADO.NET 的一組類別。 |
| [命名空間：Microsoft.Data.SqlClient](https://docs.microsoft.com/dotnet/api/microsoft.data.SqlClient) | 用於 Microsoft .NET Data Provider for SQL Server 的一組類別 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 標誌][image-ref-333-ef] Entity Framework (EF) 搭配 C&#x23;

Entity Framework (EF) 提供物件關聯式對應 (ORM)。 ORM 讓您的物件導向程式設計 (OOP) 原始程式碼能更輕鬆地操作從關聯式 SQL 資料庫中抓取的資料。

EF 與下列技術有直接或間接關聯性：

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/) \(部分機器翻譯\) 或 [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) \(部分機器翻譯\)
- 語言語法增強功能，例如 C# 中的 **=>** 運算子。
- 方便的程式，可產生對應至您 SQL 資料庫中資料表之類別的原始程式碼。 例如，[EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe) \(部分機器翻譯\)。


#### <a name="original-ef-and-new-ef"></a>原始的 EF 和新的 EF

[Entity Framework 的起始頁面](https://docs.microsoft.com/ef/) \(英文\) 介紹 EF 的描述如下所示：

- Entity Framework 是物件關聯式對應程式 (O/RM)，可讓 .NET 開發人員使用 .NET 物件來處理資料庫。 有了 Entity Framework，開發人員便不再需要撰寫通常必須撰寫的資料存取原始程式碼。

*Entity Framework* 是兩個不同原始程式碼分支共用的名稱。 一個 EF 分支較舊，而且其原始程式碼現在可以由大眾維護。 另一個 EF 是新的。 接下來會說明這兩個 EF：

| 版本 | 描述 |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft 在 2008 年 8 月首次發行 EF。 在 2015 年 3 月，Microsoft 宣佈 EF 6.x 是 Microsoft 開發的最終版本。 Microsoft 已將原始程式碼發行公眾領域。<br /><br />EF 起初是 .NET Framework 的一部分。 但 EF 6.x 已從 .NET Framework 中移除。<br /><br />[GitHub 上的 EF 6.x 原始程式碼，位於 *aspnet/EntityFramework6* 存放庫](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft 在 2016 年 6 月發行新開發的 EF Core。 EF Core 是針對更佳的彈性和可攜性而設計的。 EF Core 能在 Microsoft Windows 以外的作業系統上執行。 而且 EF Core 可以互動的資料庫，不僅限於 Microsoft SQL Server 和其他關聯式資料庫。<br /><br />**C&#x23; 程式碼範例：**<br />[Entity Framework Core 使用者入門](https://docs.microsoft.com/ef/core/get-started/index)<br />[以現有資料庫在 .NET Framework 上開始使用 EF Core](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 和相關技術有很強的功能，想要精通整個領域的開發人員必須學習很多。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 標誌][image-ref-330-java] Java 與 JDBC

Microsoft 提供 Java 資料庫連線 (JDBC) 驅動程式來搭配 SQL Server (以及 Azure SQL Database) 使用。 這是類型 4 JDBC 驅動程式，可以透過標準 JDBC 應用程式介面 (API) 來提供資料庫連接。

#### <a name="code-examples"></a>程式碼範例

| 範例 | 描述 |
| :-- | :-- |
| [程式碼範例](./jdbc/code-samples/index.md) | 教資料類型、結果集和大型資料的程式碼範例。 |
| [連接 URL 範例](./jdbc/connection-url-sample.md) | 描述如何使用連線 URL 來連線至 SQL Server。 然後用以使用 SQL 陳述式擷取資料。 |
| [資料來源範例](./jdbc/data-source-sample.md) | 描述如何使用資料來源來連線至 SQL Server。 然後使用預存程序來擷取資料。 |
| [使用 Java 查詢 Azure SQL 資料庫](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 範例。 |
| [在 Ubuntu 上使用 SQL Server 建立 Java 應用程式](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) \(英文\) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件

JDBC 文件包含下列主要區域：

| 區域 | 說明 |
| :-- | :-- |
| [Java 資料庫連線 (JDBC)](./jdbc/index.md) | JDBC 文件的根頁面。 |
| [參考](./jdbc/reference/index.md) | 介面、類別和成員。 |
| [JDBC SQL Driver 程式設計指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 標誌][image-ref-340-node] Node.js

您可以在 Windows、Linux 或 macOS 上使用 Node.js 連線到 SQL Server。 我們的 Node.js 文件根頁面在[這裡](./node-js/index.md)。

適用於 SQL Server 的 Node.js 連線驅動程式是使用 JavaScript 實作。 該驅動程式使用 TDS 通訊協定，所有現代化版本的 SQL Server 皆予支援。 驅動程式是開放原始碼專案，[可在 GitHub 上找到](https://tediousjs.github.io/tedious/) \(英文\)。

#### <a name="code-examples"></a>程式碼範例

| 範例 | 描述 |
| :-- | :-- |
| [使用 Node.js 連接到 SQL 的概念證明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 用來連接到 SQL Server 及執行查詢的準系統原始程式碼。 |
| [Azure SQL 資料庫：使用 Node.js 查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 雲端 Azure SQL Database 的範例。 |
| [在 macOS 上建立 Node.js 應用程式來使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) \(英文\) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>適用於 C++ 的 ODBC

![ODBC 標誌][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

開放式資料庫連接 (ODBC) 是在 1990 年代開發的，早於 .NET Framework。 ODBC 是設計成獨立於任何特定資料庫系統，也獨立於作業系統。

多年來，Microsoft 內外的群組已經建立並發行許多 ODBC 驅動程式。 驅動程式的範圍涵蓋數個用戶端程式設計語言。 資料目標的清單不僅限於 SQL Server。

某些其他連線能力驅動程式在內部是使用 ODBC。

#### <a name="code-example"></a>程式碼範例

- [使用 ODBC 的 C++ 程式碼範例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>文件大綱

本節中的 ODBC 內容著重於從 C++ 存取 SQL Server 或 Azure SQL Database。 下表列出 ODBC 主要文件的約略大綱。


| 區域 | 子區域 | 描述 |
| :--- | :------ | :---------- |
| [適用於 C++ 的 ODBC](./odbc/index.md) | 我們文件的根頁面。 |
| [Linux-macOS](./odbc/linux-mac/index.md) | &nbsp; | 在 Linux 或 macOS 作業系統上使用 ODBC 的相關資訊。 |
| [Windows](./odbc/windows/index.md)     | &nbsp; | 在 Windows 作業系統上使用 ODBC 的資訊。 |
| [管理](../odbc/admin/index.md) | &nbsp; | 管理 ODBC 資料來源的系統管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 由 Microsoft 建立及提供的各種 ODBC 驅動程式。 |
| [概念與參考文件](../odbc/reference/index.md) | &nbsp; | 除了傳統參考文件之外，還有 ODBC 介面的概念性資訊。 |
| &nbsp; " | [附錄](../odbc/reference/appendixes/index.md)    | 狀態轉換資料表、ODBC 資料指標等等。 |
| &nbsp; " | [開發應用程式](../odbc/reference/develop-app/index.md)  | 函式、控制代碼及其他更多功能。 |
| &nbsp; " | [開發驅動程式](../odbc/reference/develop-driver/index.md) | 如果您有特製資料來源，如何開發自己的 ODBC 驅動程式。 |
| &nbsp; " | [安裝](../odbc/reference/install/index.md) | ODBC 安裝、子機碼等等。 |
| &nbsp; " | [語法](../odbc/reference/syntax/index.md)   | 適用於安裝、安裝程式、轉譯和資料存取的 API。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 標誌][image-ref-360-php] PHP

您可以使用 PHP 與 SQL Server 互動。 我們的 PHP 文件根頁面在[這裡](./php/index.md)。

#### <a name="code-examples"></a>程式碼範例

| 範例 | 描述 |
| :-- | :-- |
| [使用 PHP 連接到 SQL 的概念證明](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 著重在連線和查詢 SQL Server 的一小段程式碼範例。 |
| [使用 PHP 彈性地連接到 SQL](./php/step-4-connect-resiliently-to-sql-with-php.md) | 重試程式碼範例中的邏輯，因為透過網際網路和雲端的連線偶爾會發生失去連線能力。 |
| [Azure SQL 資料庫：使用 PHP 查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 範例。 |
| [在 RHEL 上建立 PHP 應用程式來使用 SQL Server ](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) \(英文\) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 標誌][image-ref-370-python] Python


您可以使用 Python 與 SQL Server 互動。

#### <a name="code-examples"></a>程式碼範例

| 範例 | 描述 |
| :-- | :-- |
| [以 Python 使用 pyodbc 連線到 SQL 的概念證明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 著重在連線和查詢 SQL Server 的一小段程式碼範例。 |
| [Azure SQL 資料庫：使用 Python 查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 範例。 |
| [在 SLES 上建立 PHP 應用程式來使用 SQL Server ](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) \(英文\) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文件

| 區域 | 描述 |
| :--- | :---------- |
| [Python 連線到 SQL Server](./python/index.md) | 我們文件的根頁面。 |
| [pymssql 驅動程式](./python/pymssql/index.md) | Microsoft 不維護或測試 pymssql 驅動程式。<br /><br />pymssql 連線驅動程式是對 SQL 資料庫的簡單介面，可在 Python 程式中使用。 Pymssql 建置在 FreeTDS 之上，提供對 Microsoft SQL Server 的 Python DB-API (PEP-249) 介面。 |
| [pyodbc 驅動程式](./python/pyodbc/index.md)   | pyodbc 連線驅動程式是開放原始碼的 Python 模組，可讓存取 ODBC 資料庫變簡單。 其實作 DB API 2.0 規格，但還包含更類似 Python 的便利性。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 標誌][image-ref-380-ruby] Ruby

您可以使用 Ruby 與 SQL Server 互動。 我們的 Ruby 文件根頁面在[這裡](./ruby/index.md)。

#### <a name="code-examples"></a>程式碼範例

| 範例 | 描述 |
| :-- | :-- |
| [使用 Ruby 連接到 SQL 的概念證明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 著重在連線和查詢 SQL Server 的一小段程式碼範例。 |
| [Azure SQL 資料庫：使用 Ruby 查詢](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 範例。 |
| [在 macOS 上建立 Ruby 應用程式來使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) \(英文\) | 設定資訊，以及程式碼範例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-development"></a>[Build-an-app 網站，適用於 SQL 用戶端開發](https://www.microsoft.com/sql-server/developer-get-started/) \(英文\)


在我們的 [*Build-an-app*](https://www.microsoft.com/sql-server/developer-get-started/) \(英文\) 網頁上，您可以從包含許多程式設計語言的清單中選擇要用於連線到 SQL Server 的語言。 而且您的用戶端程式可在各種作業系統上執行。

*Build-an-app* 強調簡單與完整性，適合入門開發人員。 步驟說明下列工作：

1. 如何安裝 Microsoft SQL Server
2. 如何下載及安裝工具和驅動程式。
3. 如何進行必要設定，以適合您選擇的作業系統。
4. 如何編譯所提供的原始程式碼。
5. 如何執行程式。

接著是網站上所提供詳細資料的約略大綱：

#### <a name="java-on-ubuntu"></a>Ubuntu 上的 Java

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟 1.2 安裝 Java
    - 步驟 1.3 安裝 Java 開發套件 (JDK)
    - 步驟 1.4 安裝 Maven
2. 使用 SQL Server 建立 Java 應用程式
    - 步驟 2.1 建立連線到 SQL Server 並執行查詢的 Java 應用程式
    - 步驟 2.2 建立使用熱門架構 Hibernate 連線到 SQL Server 的 Java 應用程式
3. 讓您的 Java 應用程式加快達 100 倍
    - 步驟 3.1 建立 Java 應用程式來示範資料行存放區索引

#### <a name="python-on-windows"></a>Windows 上的 Python

1. 設定您的環境
    - 步驟 1.1 安裝 SQL Server
    - 步驟 1.2 安裝 Python
    - 步驟 1.3 安裝適用於 SQL Server 的 ODBC Driver 和 SQL 命令列公用程式
2. 使用 SQL Server 建立 Python 應用程式
    - 步驟 2.1 安裝適用於 SQL Server 的 Python 驅動程式
    - 步驟 2.2 為您的應用程式建立資料庫
    - 步驟 2.3 建立連線到 SQL Server 並執行查詢的 Python 應用程式
3. 讓您的 Python 應用程式加快達 100 倍
    - 步驟 3.1 使用 sqlcmd 建立包含 5 百萬的新資料表
    - 步驟 3.2 建立查詢此資料表的 Python 應用程式，並測量花費的時間
    - 步驟 3.3 測量執行查詢花費多少時間
    - 步驟 3.4 將資料行存放區索引新增至您的資料表
    - 步驟 3.5 測量使用資料行存放區索引來執行查詢花費多少時間

下列螢幕擷取畫面提供您我們 SQL 開發文件網站外觀的概念。

#### <a name="choose-a-language"></a>選擇語言

![SQL Dev 網站，開始使用][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>選擇作業系統

![SQL Dev 網站，Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他開發


本節提供其他開發選項的連結。 這些連接包括使用這些相同語言進行一般 Azure 開發。 資訊不僅限於以 Azure SQL Database 和 Microsoft SQL Server 為目標。

#### <a name="developer-hub-for-azure"></a>Azure 的開發人員中樞

- [Azure 的開發人員中樞](https://docs.microsoft.com/azure/)
- [適用於 .NET 開發人員的 Azure](https://docs.microsoft.com/dotnet/azure/)
- [適用於 Java 開發人員的 Azure](https://docs.microsoft.com/java/azure/)
- [適用於 Node.js 開發人員的 Azure](https://docs.microsoft.com/nodejs/azure/)
- [適用於 Python 開發人員的 Azure](https://docs.microsoft.com/python/azure/)
- [在 Azure 中建立 PHP Web 應用程式](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他語言

- [在 Windows 上使用 SQL Server 建立 Go 應用程式](https://www.microsoft.com/sql-server/developer-get-started/go/windows/) \(英文\)



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

