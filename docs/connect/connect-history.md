---
title: Microsoft SQL Server 的驅動程式記錄 |Microsoft 文件
ms.custom: ''
ms.date: 5/4/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 2f2f4bafe48018da5c6f634b272a540021fd4ca2
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server 的驅動程式歷程記錄

此頁面會描述 Microsoft 的歷程記錄資料連接技術，用於連接到 SQL Server。

## <a name="odbc"></a>ODBC

有三個不同層代的 Microsoft ODBC 驅動程式的 SQL Server。 第一個 「 SQL Server 「 ODBC 驅動程式仍隨附於[Windows Data Access Components](#microsoft-or-windows-data-access-components)。 不建議使用這個驅動程式，開發新項目。 在 SQL Server 2005 中，啟動[SQL Server Native Client](#sql-server-native-client)包含 ODBC 介面，而且是透過 SQL Server 2012 的 SQL Server 2005 所隨附的 ODBC 驅動程式。 不建議使用這個驅動程式，開發新項目。 SQL Server 2012 之後, [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)是已更新為最新的伺服器功能，接下來的驅動程式。

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client 是用於 OLE DB 和 ODBC 的獨立程式庫。 SQL Server Native Client (SNAC 通常縮寫) 隨附在 SQL Server 2005 透過 2012年。 SQL Server Native Client 可用於需要充分利用 SQL Server 2005 中透過 SQL Server 2012 中引進新功能的應用程式。 （Microsoft/Windows Data Access Components 不會更新為 SQL Server 中這些新功能）。超過 SQL Server 2012 的新功能，將不會更新 SQL Server Native Client。 切換至 Microsoft ODBC Driver for SQL Server 或 Microsoft OLE DB 驅動程式適用於 SQL Server 如果您想要利用新 SQL Server 功能從現在開始。

SQL Server Native Client 的完整文件，請參閱[SQL Server Native Client 文件](../relational-databases/native-client/sql-server-native-client-programming.md)。

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 之後, 的主要的 ODBC driver for SQL Server 在開發和發行為 Microsoft ODBC Driver for SQL Server。 如需詳細資訊，請參閱[Microsoft ODBC Driver for SQL Server 文件](./odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="ole-db"></a>OLE DB

有三個不同的層代的 SQL Server 的 Microsoft OLE DB 提供者。 第一個 「 Microsoft OLE DB Provider for SQL Server"(SQLOLEDB) 仍然隨附於[Windows Data Access Components](#microsoft-or-windows-data-access-components)。 此提供者將不會更新與新的功能並不建議使用這個驅動程式，開發新項目。 在 SQL Server 2005 中，啟動[SQL Server Native Client](#sql-server-native-client)包含 OLE DB 提供者介面 (SQLNCLI)，並隨附於 SQL Server 2005 中透過 SQL Server 2017 的 OLE DB 提供者。 它是[宣佈將被取代，在 2011年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)也不建議使用這個驅動程式，開發新項目。 在 2017，OLE DB 資料存取技術是後續[undeprecated 和新的已規劃的發行已宣布](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)2018年的。 新的 OLE DB 提供者稱為 「 Microsoft OLE DB 驅動程式的 SQL Server"(MSOLEDBSQL) 是目前維護及受支援。

## <a name="adonet"></a>ADO.NET

ADO.NET 以 Microsoft.NET Framework 中引進，而且會持續改進和維護。 它是 Microsoft.NET Framework 的核心元件。 如需詳細資訊，請參閱[for SQL Server 的 Microsoft ADO.NET](ado-net/microsoft-ado-net-for-sql-server.md)。

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>用於 SQL Server 的 Microsoft JDBC 驅動程式

Microsoft JDBC Driver for SQL Server 2000 中引進，繼續改善及維護。 它是開放 2016。 如需最新資訊，包括如何下載驅動程式，請參閱[JDBC 驅動程式概觀](./jdbc/overview-of-the-jdbc-driver.md)。

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>用於 SQL Server 之 PHP 的 Microsoft 驅動程式

在 2009 年引進，做為開放原始碼專案，繼續改善及維護 Microsoft Drivers for PHP for SQL Server。 如需最新資訊，包括如何下載 PHP 驅動程式，請參閱[Microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md)。

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Node.js for SQL Server 的 Microsoft 驅動程式

Node.js for SQL Server 的 Microsoft 驅動程式可讓 Microsoft Windows 和 Microsoft Windows Azure 上存取 Microsoft SQL Server 和 Microsoft Windows Azure SQL Database 的 Node.js 應用程式。 開發工作不會再被焦點放在此驅動程式。 不建議建立新的應用程式使用 for Node.js 的 Microsoft Driver for SQL Server。

如需詳細資訊，Microsoft 驅動程式 for Node.js for SQL Server，請參閱[WindowsAzure / 節點 sqlserver](https://github.com/Azure/node-sqlserver)。

### <a name="tedious"></a>冗長

Microsoft 目前提供給，並且支援開放原始碼冗長模組 Node.js 中使用 JavaScript 的 SQL Server 的連接能力。 如需詳細資訊，請參閱[Node.js Driver for SQL Server](./node-js/node-js-driver-for-sql-server.md)。

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 或 Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) 隨附於並支援的 Windows 應用程式的回溯相容性並不屬於目前的 SQL Server 技術堆疊。 MDAC/WDAC 中的元件將會加入任何新功能並不建議用於開發新應用程式。

基於本文的目的，您可以將 MDAC/WDAC 堆疊分成下列元件在根據技術和產品：

* **ADO** （包括 ADOMD 和 ADOX）
* **OLE DB** （包括 OLE DB 核心服務、 SQL Server OLE DB 提供者、 Oracle OLE DB 提供者、 OLE DB Provider for ODBC 驅動程式、 資料圖案提供者，以及遠端的資料提供者）
* **ODBC** （包括 ODBC 驅動程式管理員、 SQL ODBC 驅動程式，以及 Oracle ODBC 驅動程式）

### <a name="mdacwdac-components"></a>MDAC/WDAC 元件

MDAC/WDAC 包含下列元件：

* **ODBC:** Microsoft 開放式資料庫連接 (ODBC) 介面是 C 程式設計語言介面，可讓應用程式從各種不同的資料庫管理系統 (DBMS) 存取資料。 使用此 API 的應用程式受限於存取只使用關聯式資料來源。
* **OLE DB:** OLE DB 是一組存取各種資料存放區中的資料的 COM 介面。 OLE DB 提供者的存在存取資料庫、 檔案系統、 訊息存放區、 目錄服務、 工作流程，以及文件存放區中的資料。
* **ADO:** ActiveX Data Objects (ADO) 提供高層級的程式設計模型。 雖然較好的效能比直接編碼到 OLE DB 或 ODBC、 ADO 是容易學習和使用。 它可以用於指令碼語言，例如 Microsoft Visual Basic Scripting Edition (VBScript) 或 Microsoft JScript 語言。
* **ADOMD:** ADO 多維度 (ADOMD) 是用於與多維度資料提供者，例如 Microsoft OLAP 提供者，也稱為 Microsoft Analysis Services 提供者。 任何主要功能增強功能已不對它自 MDAC 2.0。
* **ADOX:** DDL 和安全性 (ADOX) ADO 延伸可讓建立和修改資料庫、 資料表、 索引或預存程序的定義。 您可以使用 ADOX 與任何提供者。 Microsoft Jet OLE DB 提供者會提供完整支援 ADOX，而 Microsoft SQL Server OLE DB 提供者提供有限的支援。
* **Microsoft SQL Server 網路程式庫：** SQLOLEDB 和 SQLODBC 與 SQL Server 資料庫通訊，允許 SQL Server 網路程式庫。 下列的 SQL Server 網路程式庫已被取代的 MDAC/WDAC 版本： Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC。 TCP/IP 和具名管道會繼續受到支援，而且適用於 64 位元 Windows 作業系統。
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL) 可讓應用程式來存取資料來源的 ODBC 驅動程式透過 OLE DB 和 ADO （這會在內部使用 OLEDB） 上建立。 MSDASQL 是 OLEDB 提供者連接到 ODBC，而非資料庫。 它可作為橋接器從 OLE DB，ODBC 驅動程式的資料來源沒有直接的 OLE DB 提供者存在時。 MSDASQL 隨附於 Windows 作業系統和 Windows Server 2008 和 Vista SP1 的第一個 Windows 釋放以包含 64 位元版本的技術。

### <a name="deprecated-mdacwdac-components"></a>已被取代的 MDAC/WDAC 元件

MDAC/WDAC，目前版本中仍然支援這些元件，但它們可能會在未來版本中移除。 在開發新的應用程式時，Microsoft 建議您避免使用這些元件。 此外，當您升級或修改現有的應用程式，移除這些元件的相依性。

* **SQLOLEDB:** Microsoft OLE DB Provider for SQL Server (SQLOLEDB)，可支援 Microsoft SQL Server 存取權，已被取代。 其連線至 SQL server 的未來版本可能不支援。 連接至的版本早於 SQL Server 7 的功能將從作業系統中移除，在 Windows 7 之後。 新的應用程式應該使用 Microsoft OLE DB 驅動程式的 SQL Server (MSOLEDBSQL)，可支援新的 SQL Server 功能。 現有的應用程式應該移轉到 Microsoft OLE DB 驅動程式的 SQL Server 也較佳的效能、 可靠性和可支援性的。 如需詳細資訊，請參閱[應用程式更新至 OLE DB 驅動程式的 SQL Server 從 MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。
* **SQLODBC:** Microsoft SQL Server ODBC 驅動程式 (SQLODBC)，可支援 Microsoft SQL Server 存取權，已被取代。 其連線至 SQL server 的未來版本可能不支援。 連接至的版本早於 SQL Server 7 的功能將從作業系統中移除，在 Windows 7 之後。 新的應用程式應該使用 Microsoft ODBC Driver for SQL Server 在 Windows 中，可支援新的 SQL Server 功能。 現有的應用程式應該移轉到 Microsoft ODBC Driver for SQL Server 也較佳的效能、 可靠性和可支援性的。 相關資訊，請參閱[更新至 SQL Server Native Client 應用程式從 MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。
* **Microsoft Jet Database Engine 4.0:** 從 2.6 版開始，MDAC 不再包含 Jet 元件。 換句話說，MDAC 2.6、 2.7 和 2.8 不包含 Microsoft Jet、 Microsoft Jet OLE DB 提供者、 ODBC 桌面資料庫驅動程式或 Jet 資料存取物件 (DAO)。 Microsoft Jet 資料庫引擎 4.0 元件輸入的功能已被取代的狀態和工程 持續偏，哪些尚未收到功能層級的增強功能自 Windows 2000 中的 Microsoft Windows 的一部分而變得。

  沒有可用的 64 位元版本的 Jet 資料庫引擎、 Jet OLEDB 驅動程式、 Jet ODBC 驅動程式或 Jet DAO。 如需詳細資訊，請參閱[知識庫文章 957570](http://support.microsoft.com/kb/957570)。 在 64 位元版本的 Windows，32 位元 Jet 是 Windows WOW64 子系統下執行。 如需 WOW64 的詳細資訊，請參閱[MSDN WOW64 文件](https://msdn.microsoft.com/library/windows/desktop/aa384274(v=vs.85).aspx)。 原生 64 位元應用程式無法與在 WOW64 中執行的 32 位元 Jet 驅動程式通訊。

  而不是 Microsoft Jet，Microsoft 建議使用[Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)開發新的非 Microsoft Access 應用程式需要關聯式資料存放區時。 這些新的或已轉換的 Jet 應用程式可以繼續使用 Jet 區分，用意在於使用 Microsoft Office 2003 和舊版的檔案 （.mdb 及.xls） 儲存非主要資料。 不過，這些應用程式，您應該規劃將從 Jet 移轉到 2007 Office System 驅動程式。 您可以[下載 2007 Office System 驅動程式](https://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=7554f536-8c28-4598-9b72-ef94e038c891)，可讓您讀取和寫入至已存在的檔案 （.mdb 及.xls） 的 Office 2003 或 Office 2007 （.accdb、 *.xlsm、 *.xlsx 和 *.xlsb） 檔案格式中。

  > [!IMPORTANT]
  > 請閱讀 2007 Office System 使用者授權合約的特定使用方式的限制。

  > [!NOTE]
  > SQL Server 應用程式也可以存取在 2007 Office System 中，和更早版本，檔案從 SQL Server 異質資料連線和整合服務功能，透過 2007 Office System 驅動程式。 此外，64 位元 SQL Server 應用程式可以存取 32 位元 Jet 和 2007 Office System 檔案的 64 位元 Windows 上使用 32 位元 SQL Server Integration Services (SSIS)。

* **MSDADS:** Microsoft OLE DB 提供者使用的資料來形成 (MSDADS)，您可以建立索引鍵、 欄位或資料列集之間的階層式關聯性的應用程式中。 任何主要功能增強功能不已自 MDAC 2.1。 此提供者已被取代。 Microsoft 建議您使用的 XML，而不是 MSDADS。
* **Oracle ODBC 和 Oracle OLE DB:** Microsoft Oracle ODBC 驅動程式 (Oracle ODBC) 和 Microsoft OLE DB Provider for Oracle (Oracle OLE DB) 提供存取 Oracle 資料庫伺服器。 它們會使用 Oracle Call Interface (OCI) 第 7 版所建置，並提供 Oracle 7 的完整支援。 此外，它會使用 Oracle 7 模擬針對 Oracle 8 資料庫提供有限的支援。 Oracle 不支援使用 OCI 第 7 版呼叫的應用程式。 已被取代這些技術。 如果您使用 Oracle 資料來源，您應該移轉到 Oracle 提供的驅動程式和提供者。
* **RDS:** 遠端資料服務 (RDS) 是透過網際網路或內部網路存取遠端的 ADO 資料錄集物件的專屬 Microsoft 機制。 RDS 已被取代。任何主要功能增強功能已不對 RDS 自 MDAC 2.1。 Microsoft 已發行的.NET Framework 中，有大量的 SOAP 功能，並取代 RDS 元件。 所有的 RDS 伺服器元件將從作業系統中移除，在 Windows 7 之後。
* **JRO:** Jet 複寫物件 」 (JRO) 已被取代。 JRO 用於 ADO 與 Jet (*.mdb) 建立及壓縮 Jet 資料庫 (.mdb) 和執行 Jet 複寫管理的資料庫。MDAC 2.7 將其最後一個版本。JRO 將無法在 64 位元 Windows 作業系統上使用。Microsoft Access 2007 檔案格式中不支援 JRO (*.accdb)。
* **16 位元 ODBC 支援：** 如果您使用 16 位元應用程式，您應該將它移轉至 32 位元應用程式。 16 位元的功能已經過時，正在從 64 位元作業系統中移除。 如需詳細資訊，請參閱[Knowledge base 文章 896458](http://support.microsoft.com/kb/896458)。
* **OLEDB 簡單提供者 (MSDAOSP):** OLEDB 簡單提供者會提供快速建立簡單的資料上的 OLE DB 提供者架構。 MSDAOSP 已被取代。
* **ODBC 資料指標程式庫：** ODBC 資料指標程式庫 (ODBCCR32.dll) 提供有限的用戶端資料指標。 ODBC 資料指標程式庫已被取代。您的應用程式可以使用伺服器端資料指標實作，以取代。
* **OLE DB 跨處理序介面遠端執行功能：** OLEDB 介面遠端處理 (msdaps.dll) 嘗試讓 OLE DB 提供者跨處理序。 OLEDB 跨處理序介面遠端執行功能已被取代。
* **AppleTalk 和 Banyan Vines SQL 網路程式庫：** Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC SQL 網路程式庫中已被取代。 如果您使用這些技術，您應該修改您的應用程式使用其中一種其他網路程式庫，例如 TCP/IP 和具名管道。

### <a name="mdacwdac-releases"></a>MDAC/WDAC 版本

以下是可支援性案例，過去的 MDAC/WDAC 版本，從最早的清單。

* **MDAC 1.5、 MDAC 2.0 和 MDAC 2.1:** 這些 MDAC 的版本是透過 Microsoft Windows NT 選項組件、 Microsoft Windows 平台 SDK 或 MDAC 網站發行的獨立版本。 不再支援這些版本的 MDAC。
* **MDAC 2.5:** MDAC 的此版本隨附於 Windows 2000 作業系統。 Service pack 的 MDAC 2.5 都包含對應的 Windows 2000 service pack。
* **MDAC 2.6:** MDAC 2.6 RTM、 SP1 和 SP2 隨附於 Microsoft SQL Server 2000 RTM、 SP1 和 SP2，分別是。 此外，這些 MDAC service pack 已發行至 MDAC 網站根據 Microsoft SQL Server 2000 service pack 版本的排程。 您可以在 Windows 2000、 Windows Millennium Edition、 Windows NT、 Windows 95 和 Windows 98 平台上安裝此版本的 MDAC 和其 service pack。 這個版本的 MDAC 不再支援。
* **MDAC 2.7:** MDAC 的此版本隨附於 Microsoft Windows XP RTM 和 SP1 作業系統。 您可以在 Windows 2000、 Windows Millennium、 Windows NT 和 Windows 98 平台上安裝此版本的 MDAC 和其 service pack。 您可以安裝此版本 Windows XP 平台，只能透過作業系統或其服務組件。 這個版本的 MDAC 不再支援。
* **MDAC 2.8:** MDAC 的這個版本是隨附於 Windows Server 2003 和 Windows XP SP2 和更新版本。 您也可以在 Windows 2000 上安裝此版本的 MDAC 和其 service pack。

  * 32 位元版本的 MDAC 2.8 也被發行至 MDAC 網站在相同 Windows Server 2003 發行給客戶的時間。
  * MDAC 2.8 64 位元版本的 Windows Server 2003 和 Windows XP 的 64 位元版本一起發行。

* **Windows Data Access Components (WDAC):** MDAC 變更其名稱為 WDAC-「 Windows Data Access Components"開頭為 Windows Vista 和 Windows Server 2008。 WDAC 是作業系統的一部分，而且不使用個別的轉散發。 WDAC 如服務性受限於生命週期的作業系統。

  WDAC 32 位元和 64 位元版本隨附的 32 位元和 64 位元版本的 Windows 作業系統中，分別。

## <a name="obsolete-data-access-technologies"></a>過時的資料存取技術

過時技術的技術和，尚未增強型或更新在數個產品版本中，將會排除未來的產品版本。 當您撰寫新的應用程式時，請勿使用這些技術。 當您修改現有的寫法是使用這些技術的應用程式時，請考慮移轉這些應用程式以 ADO.NET 或另一個新的技術。

下列元件會被視為過時：

* **Db-library:** Db-library 是 SQL Server 特有的程式設計模型，其中包含 C 應用程式開發介面。 SQL Server 6.5 之後已無增強資料程式庫的功能。 在最終發行搭配 SQL Server 2000，而且它將無法移植到 64 位元 Windows 作業系統。
* **(E-SQL) 的內嵌 SQL:** E SQL 是 SQL Server 特有的程式設計模型，可讓要內嵌在 Visual C 程式碼中的 TRANSACT-SQL 陳述式。 已為 E SQL 進行 SQL Server 6.5 之後無增強功能。 在最終發行搭配 SQL Server 2000，而且它將無法移植到 64 位元 Windows 作業系統。
* **資料存取物件 (DAO):** DAO 提供 JET (Access) 資料庫的存取權。 此 API 可從 Microsoft Visual Basic、 Microsoft Visual c + + 和指令碼語言。 它是隨附在 Microsoft Office 2000 和 Office XP。 DAO 3.6 是這項技術的最終版本。 它無法在 64 位元 Windows 作業系統上。
* **遠端資料物件 (RDO):** RDO 已特別設計用來存取遠端 ODBC 關聯式資料來源，並讓它更容易不複雜的應用程式程式碼會使用 ODBC。 它是隨附於 Microsoft Visual Basic 版本 4、 5 和 6。 RDO 2.0 版是這項技術的最終版本。