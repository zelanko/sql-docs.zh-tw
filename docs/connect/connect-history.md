---
title: Microsoft SQL Server 的驅動程式歷程記錄 |Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: genemi
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: jroth
ms.openlocfilehash: 5c312421c7934690c947dbe0bf23b6404afaf56f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770507"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server 的驅動程式歷程記錄

此頁面說明 Microsoft 的歷程記錄資料連線技術連接到 SQL Server。

## <a name="odbc"></a>ODBC

有三個不同世代的 Microsoft OLE DB Provider for SQL Server。 第一個"SQL Server"ODBC 驅動程式仍隨附於[Windows Data Access Components](#microsoft-or-windows-data-access-components)。 不建議用於新的開發中使用此驅動程式。 在 SQL Server 2005 中，啟動[SQL Server Native Client](#sql-server-native-client)包含 ODBC 介面，並隨附於 SQL Server 2005 到 SQL Server 2012 的 ODBC 驅動程式。 不建議用於新的開發中使用此驅動程式。 SQL Server 2012 之後, [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)會更新為最新的伺服器功能，接下來的驅動程式。

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client 是用於 OLE DB 和 ODBC 的獨立程式庫。 到 2012 年，SQL Server 2005 中包含了 SQL Server Native Client (SNAC 通常縮寫)。 SQL Server Native Client 可用於需要利用 SQL Server 2005 到 SQL Server 2012 中引進的新功能的應用程式。 （Microsoft/Windows Data Access Components 不會更新 SQL Server 中的這些新功能）。除了 SQL Server 2012 的新功能，將不會更新 SQL Server Native Client。 切換至 Microsoft ODBC Driver for SQL Server 或 Microsoft OLE DB Driver for SQL Server 如果您想要利用新的 SQL Server 功能，從現在開始。

SQL Server Native Client 的完整文件，請參閱 < [SQL Server Native Client 文件](../relational-databases/native-client/sql-server-native-client-programming.md)。

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 之後, 主要 ODBC driver for SQL Server 已開發和發行為 Microsoft ODBC Driver for SQL Server。 如需詳細資訊，請參閱 < [Microsoft ODBC Driver for SQL Server 文件](./odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="ole-db"></a>OLE DB

有三個不同世代的 Microsoft OLE DB Provider for SQL Server。 [Microsoft OLE DB Provider for SQL Server](#microsoft-or-windows-data-access-components) (SQLOLEDB) 仍隨附於 Windows Data Access Component \(英文\)。 此提供者將不會更新與新功能，並不建議用於新的開發中使用此驅動程式。 在 SQL Server 2005 中，啟動[SQL Server Native Client](#sql-server-native-client)包含 OLE DB 提供者介面 (SQLNCLI)，並隨附於 SQL Server 2005 到 SQL Server 2017 的 OLE DB 提供者。 [已在 2011 年宣布取代](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) \(英文\) 它，因此，不建議使用此驅動程式來進行新開發。 在 2017 中，OLE DB 資料存取技術的後續[取消和新的已規劃的發行已宣布](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)2018。 新的 OLE DB 提供者稱為 「 Microsoft OLE DB Driver for SQL Server"(MSOLEDBSQL) 是目前維護和支援。

## <a name="adonet"></a>ADO.NET

ADO.NET 引進了以 Microsoft.NET Framework，並持續改善及維護。 它是 Microsoft.NET Framework 的核心元件。 如需詳細資訊，請參閱 <<c0> [ 適用於 SQL Server 的 Microsoft ADO.NET](ado-net/microsoft-ado-net-for-sql-server.md)。

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>用於 SQL Server 的 Microsoft JDBC 驅動程式

在 2000年中引進，Microsoft JDBC Driver for SQL Server 會繼續改善及維護。 它是開放原始碼，在 2016年。 如需最新資訊，包括如何下載驅動程式，請參閱[JDBC 驅動程式概觀](./jdbc/overview-of-the-jdbc-driver.md)。

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>用於 SQL Server 之 PHP 的 Microsoft 驅動程式

在 2009 年引進，做為開放原始碼專案，繼續改善及維護的 Microsoft Drivers for PHP for SQL Server。 如需最新資訊，包括如何下載 PHP 驅動程式，請參閱[Microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md)。

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>適用於 Node.js 的 SQL Server 的 Microsoft 驅動程式

適用於 Node.js 的 SQL Server 的 Microsoft 驅動程式可讓 Microsoft Windows 和 Microsoft Windows Azure 上存取 Microsoft SQL Server 和 Microsoft Windows Azure SQL Database 的 Node.js 應用程式。 不會再被開發工作著重在此驅動程式。 不建議建立新的應用程式使用適用於 Node.js 的 Microsoft Driver for SQL Server。

如需詳細資訊，Microsoft 驅動程式適用於 Node.js 的 SQL Server，請參閱[WindowsAzure / 節點 sqlserver](https://github.com/Azure/node-sqlserver)。

### <a name="tedious"></a>單調乏味

Microsoft 目前提供，並支援連線到 SQL Server 使用 JavaScript 在 Node.js 中的開放原始碼冗長乏味的模組。 如需詳細資訊，請參閱 < [Node.js Driver for SQL Server](./node-js/node-js-driver-for-sql-server.md)。

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 或 Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) 隨附於並支援 Windows 應用程式的回溯相容性，不是目前的 SQL Server 技術堆疊的一部分。 MDAC/WDAC 中的元件，將會加入任何新功能，並不建議用於開發新應用程式。

基於本文的目的，您可以將 MDAC/WDAC 堆疊分成下列元件，並根據技術和產品：

* **ADO** （包括 ADOMD 和 ADOX）
* **OLE DB** （包括 OLE DB 核心服務、 SQL Server OLE DB 提供者、 Oracle OLE DB 提供者、 OLE DB Provider for ODBC 驅動程式、 Data Shape 提供者和遠端的資料提供者）
* **ODBC** （包括 ODBC 驅動程式管理員、 SQL ODBC 驅動程式和 Oracle 的 ODBC 驅動程式）

### <a name="mdacwdac-components"></a>MDAC/WDAC 元件

MDAC/WDAC 包含下列元件：

* **ODBC:** Microsoft 開放式資料庫連接 (ODBC) 介面是 C 程式設計語言介面，可讓應用程式從各種不同的資料庫管理系統 (DBMS) 存取資料。 使用此 API 的應用程式僅限於存取只使用關聯式資料來源。
* **OLE DB:** OLE DB 是一組 COM 介面來存取各種資料存放區中的資料。 OLE DB 提供者有存取資料庫、 檔案系統、 訊息存放區、 目錄服務、 工作流程，以及文件存放區中的資料。
* **ADO:** ActiveX Data Objects (ADO) 提供高階的程式設計模型。 雖然較好的效能比直接編碼至 OLE DB 或 ODBC、 ADO 是容易學習和使用。 它可從指令碼語言，例如 Microsoft Visual Basic Scripting Edition (VBScript) 或 Microsoft JScript。
* **ADOMD:** .ADO 多維度 (ADOMD) 是用於多維度資料提供者，例如 Microsoft OLAP 提供者，也就是 Microsoft Analysis Services 提供者。 任何主要的強化功能，已對它自 MDAC 2.0。
* **ADOX:** DDL 和安全性 (ADOX) 的 ADO 延伸模組讓您建立及修改資料庫、 資料表、 索引或預存程序的定義。 您可以使用 ADOX 與任何提供者。 Microsoft Jet OLE DB 提供者會提供完整支援 ADOX，而 Microsoft SQL Server OLE DB 提供者提供有限的支援。
* **Microsoft SQL Server 網路程式庫：** SQLOLEDB 和 SQLODBC 與 SQL Server 資料庫進行通訊，可讓 SQL Server 的網路程式庫。 下列的 SQL Server 網路程式庫已被取代的 MDAC/WDAC 版本： Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC。 TCP/IP 和具名管道會繼續受到支援，並可在 64 位元 Windows 作業系統上。
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL) 可讓來存取資料來源的 ODBC 驅動程式透過 OLE DB 和 ADO (在內部使用 OLEDB） 建置的應用程式。 MSDASQL 是 OLEDB 提供者連接到 ODBC，而非資料庫。 它是要作為橋接器從 OLE DB ODBC 驅動程式沒有直接的 OLE DB 提供者存在資料來源時。 MSDASQL 隨附於 Windows 作業系統和 Windows Server 2008 和 Vista SP1 是第一個 Windows 版本，以包含 64 位元版本的技術。

### <a name="deprecated-mdacwdac-components"></a>已被取代的 MDAC/WDAC 元件

在目前版本中的 MDAC/WDAC，仍然支援這些元件，但它們可能在未來版本中移除。 在開發新的應用程式時，Microsoft 建議您避免使用這些元件。 此外，當您升級或修改現有的應用程式時，移除這些元件上的任何相依性。

* **SQLOLEDB:** Microsoft OLE DB Provider for SQL Server (SQLOLEDB)，可支援 Microsoft SQL server 的存取，已被取代。 其連線到 SQL Server 的未來版本可能不支援。 Windows 7 之後，將從作業系統移除連接版本早於 SQL Server 7 的能力。 新的應用程式應該使用 Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)，可支援新的 SQL Server 功能。 現有的應用程式應該移轉至 Microsoft OLE DB Driver for SQL Server 也較佳的效能、 可靠性和可支援性的。 如需詳細資訊，請參閱 <<c0> [ 應用程式更新至 OLE DB Driver for SQL Server 從 MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。
* **SQLODBC:** Microsoft SQL Server ODBC 驅動程式 (SQLODBC)，可支援 Microsoft SQL server 的存取，已被取代。 其連線到 SQL Server 的未來版本可能不支援。 Windows 7 之後，將從作業系統移除連接版本早於 SQL Server 7 的能力。 新的應用程式應該使用可支援新的 SQL Server 功能的 Windows 上的 SQL Server 的 Microsoft ODBC 驅動程式。 現有的應用程式應該移轉至 Microsoft ODBC Driver for SQL Server 也較佳的效能、 可靠性和可支援性的。 相關的資訊，請參閱[更新至 SQL Server Native Client 應用程式從 MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。
* **Microsoft Jet Database Engine 4.0:** 從 2.6 版開始，MDAC 不會再包含 Jet 元件。 換句話說，MDAC 2.6，2.7、 2.8 不包含 Microsoft Jet、 Microsoft Jet OLE DB 提供者、 ODBC 桌面資料庫驅動程式或 Jet 資料存取物件 (DAO)。 

  沒有可用的 64 位元版本的 Jet Database Engine、 Jet OLEDB 驅動程式、 Jet ODBC 驅動程式或 Jet DAO。 如需詳細資訊，請參閱[知識庫文章 957570](https://support.microsoft.com/kb/957570)。 在 64 位元版本的 Windows，32 位元 Jet 是 Windows WOW64 子系統下執行。 如需有關 WOW64 的詳細資訊，請參閱[MSDN WOW64 文件](/windows/desktop/WinProg64/wow64-implementation-details)。 原生的 64 位元應用程式無法與在 WOW64 中執行的 32 位元 Jet 驅動程式通訊。

  而不是 Microsoft Jet，Microsoft 建議您使用[Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)開發新的、 需要關聯式資料存放區的非 Microsoft Access 應用程式時。 這些新的或已轉換的 Jet 應用程式可以繼續使用 Jet 藉由使用 Microsoft Office 2003 和舊版的檔案 （.mdb 和.xls），來儲存非主要資料。 不過，對於這些應用程式中，您應該規劃從 Jet 移轉至 Microsoft Access 資料庫引擎。 您可以[下載 Microsoft Access 資料庫引擎](https://www.microsoft.com/download/details.aspx?id=54920)，可讓您讀取和寫入至已存在的檔案 （.mdb 和.xls） 的 Office 2003 或 Office 2007 （*.accdb、 *.xlsm、 *.xlsx 和 *.xlsb） 檔案格式中。

  > [!IMPORTANT]
  > 請閱讀 2007 Office System 使用者授權合約的特定使用方式的限制。

  > [!NOTE]
  > SQL Server 應用程式也可以存取 2007 Office System 及更早版本，檔案從 SQL Server 異質資料連線和整合服務功能，透過 2007 Office System 驅動程式。 此外，64 位元 SQL Server 應用程式可以在 64 位元 Windows 上使用 32 位元 SQL Server Integration Services (SSIS) 存取 32 位元 Jet 和 2007 Office 系統檔案。

* **MSDADS:** 的 Microsoft OLE DB 提供者的資料成形 (MSDADS)，您可以建立索引鍵、 欄位或資料列集之間的階層式關聯性的應用程式中。 MDAC 2.1 後未不發生任何重大的功能增強功能。 此提供者已被取代。 Microsoft 建議，您會使用 XML，而不是 MSDADS。
* **Oracle ODBC 和 Oracle OLE DB:** Microsoft Oracle ODBC 驅動程式 (Oracle ODBC) 和 Microsoft OLE DB Provider for Oracle (Oracle OLE DB) 提供的 Oracle 資料庫伺服器的存取權。 它們會使用 Oracle Call Interface (OCI) 第 7 版所建置，並提供適用於 Oracle 7 的完整支援。 此外，它會使用 Oracle 7 模擬為 Oracle 8 資料庫提供有限的支援。 Oracle 不支援使用 OCI 第 7 版呼叫的應用程式。 這些技術已被取代。 如果您使用 Oracle 資料來源，您應該移轉到 Oracle 提供的驅動程式和提供者。
* **RDS:** 遠端資料服務 (RDS) 是透過網際網路或近端內部網路存取遠端的 ADO 資料錄集物件的專屬 Microsoft 機制。 RDS 是已被取代;任何主要功能增強功能不進行了 RDS 自 MDAC 2.1。 Microsoft 已發行.NET Framework，但有廣泛的 SOAP 功能，並取代 RDS 元件。 在 Windows 7 之後，將從作業系統移除所有 RDS 伺服器元件。
* **JRO:** Jet 複寫物件 」 (JRO) 已被取代。 JRO 用於 ADO 與 Jet ( *.mdb) 資料庫，以建立並壓縮 Jet 資料庫 (.mdb)，並執行 Jet 複寫管理。MDAC 2.7 會其最後一個版本。JRO 無法在 64 位元 Windows 作業系統上。Microsoft Access 2007 檔案格式中不支援 JRO (* .accdb)。
* **16 位元 ODBC 支援：** 如果您使用的 16 位元應用程式，您應該將它移轉至 32 位元應用程式。 16 位元功能已被取代，正在從 64 位元作業系統中移除。 如需詳細資訊，請參閱[知識庫文章 896458](https://support.microsoft.com/kb/896458)。
* **OLEDB 簡單提供者 (MSDAOSP):** OLEDB 簡單提供者提供快速建置簡單的資料上的 OLE DB 提供者架構。 MSDAOSP 已被取代。
* **ODBC 資料指標程式庫：** ODBC 資料指標程式庫 (ODBCCR32.dll) 提供有限的用戶端資料指標。 ODBC 資料指標程式庫已被取代;您的應用程式可以使用伺服器端資料指標實作，來取代。
* **OLE DB 跨處理序介面的遠端處理：** OLEDB 介面遠端 (msdaps.dll) 嘗試讓 OLE DB 提供者跨處理序。 OLEDB 跨處理序介面的遠端執行功能已被取代。
* **AppleTalk 和 Banyan Vines SQL 網路程式庫：** Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC SQL 網路程式庫已被取代。 如果您使用這些技術，您應該修改應用程式以使用其中一個其他網路程式庫，例如 TCP/IP 和具名管道。

### <a name="mdacwdac-releases"></a>MDAC/WDAC 版本

以下是可支援性的案例，最早開始的過去 MDAC/WDAC 版本的清單。

* **MDAC 1.5、 MDAC 2.0 和 MDAC 2.1:** MDAC 的這些版本已透過 Microsoft Windows NT Option Pack、 Microsoft Windows 平台 SDK 或 MDAC 網站發行的獨立版本。 不再支援這些版本的 MDAC。
* **MDAC 2.5:** 這個版本的 MDAC 是隨附在 Windows 2000 作業系統。 Service pack 的 MDAC 2.5 都包含對應的 Windows 2000 service pack。
* **MDAC 2.6:** MDAC 2.6 RTM、 SP1 和 SP2 是分別隨附於 Microsoft SQL Server 2000 RTM、 SP1 和 SP2。 此外，這些 MDAC service pack 已發行至根據 Microsoft SQL Server 2000 service pack 版本排程 MDAC 的網站。 您可以在 Windows 2000、 Windows Millennium Edition、 Windows NT、 Windows 95 和 Windows 98 平台上安裝此版本的 MDAC 和其 service pack。 這個版本的 MDAC 不再支援。
* **MDAC 2.7:** 這個版本的 MDAC 已隨附於 Microsoft Windows XP RTM 和 SP1 作業系統。 您可以在 Windows 2000、 Windows Millennium、 Windows NT 和 Windows 98 平台上安裝此版本的 MDAC 和其 service pack。 您可以只透過作業系統或其服務套件在 Windows XP 平台上安裝此版本。 這個版本的 MDAC 不再支援。
* **MDAC 2.8:** 這個版本的 MDAC 已隨附於 Windows Server 2003 和 Windows XP SP2 和更新版本。 您也可以在 Windows 2000 上安裝此版本的 MDAC 和其 service pack。

  * 32 位元版本的 MDAC 2.8 也被發行至 MDAC 網站在此同時，Windows Server 2003 發行給客戶。
  * MDAC 2.8 64 位元版本的 64 位元版本的 Windows Server 2003 和 Windows XP 發行。

* **Windows Data Access Components (WDAC):** MDAC 會變更其名稱為 WDAC-「 Windows Data Access Components"開頭為 Windows Vista 和 Windows Server 2008。 WDAC 是作業系統的一部分，而且不提供個別的轉散發。 WDAC 的服務性受限於生命週期的作業系統。

  WDAC 32 位元和 64 位元版本隨附的 32 位元和 64 位元版本 Windows 作業系統中，分別。

## <a name="obsolete-data-access-technologies"></a>過時的資料存取技術

已淘汰的技術是的技術和，尚未增強或更新產品的數個版本中，將會排除未來的產品版本。 當您撰寫新的應用程式時，請務必使用這些技術。 當您修改現有的寫法是使用這些技術的應用程式時，請考慮這些應用程式移轉到 ADO.NET 或另一個目前的技術。

下列元件會被視為過時的：

* **DB-Library:** DB 程式庫是 SQL Server 特有的程式設計模型，包括 C Api。 SQL Server 6.5 之後已有資料程式庫的任何功能增強功能。 在最終發行了 SQL Server 2000 中，並將移植到 64 位元 Windows 作業系統。
* **內嵌的 SQL (E-SQL):** E SQL 是 SQL Server 特有的程式設計模型，可讓 Visual C 程式碼中內嵌的 TRANSACT-SQL 陳述式。 無增強對 E SQL SQL Server 6.5 之後。 在最終發行了 SQL Server 2000 中，並將移植到 64 位元 Windows 作業系統。
* **資料存取物件 (DAO):** DAO 提供 （存取） 的 JET 資料庫的存取權。 此 API 可以使用從 Microsoft Visual Basic、 Microsoft Visual C++，以及指令碼語言。 它是隨附於 Microsoft Office 2000 和 Office XP。 DAO 3.6 是這項技術的最終版本。 它無法在 64 位元 Windows 作業系統上。
* **遠端資料物件 (RDO):** RDO 已特別設計用來存取遠端的 ODBC 關聯式資料來源，並更輕鬆地使用 ODBC，不需要複雜的應用程式程式碼。 它是隨附於 Microsoft Visual Basic 版本 4、 5 和 6。 RDO 2.0 版是這項技術的最終版本。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
