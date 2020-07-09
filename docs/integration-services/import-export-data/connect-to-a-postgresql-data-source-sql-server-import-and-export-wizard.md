---
title: 連線至 PostgreSQL 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0890fbce533a540300ebd6b7da37a1fc26572a52
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768067"
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>連線至 PostgreSQL 資料來源 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主題示範如何透過 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面，連線至 **PostgreSQL** 資料來源。 

> [!IMPORTANT]
> 這一篇 Microsoft 文章範圍未涵蓋連線至 PostgreSQL 資料庫的詳細需求和必要條件。 本文假設您已安裝 PostgreSQL 用戶端軟體，並已成功連線至目標 PostgreSQL 資料庫。 如需詳細資訊，請參閱 PostgreSQL 資料庫管理員或 PostgreSQL 文件。

## <a name="get-the-postgresql-odbc-driver"></a>取得 PostgreSQL ODBC 驅動程式

### <a name="install-the-odbc-driver-with-stack-builder"></a>使用堆疊產生器安裝 ODBC 驅動程式
執行堆疊產生器，將 PostgreSQL ODBC 驅動程式 (psqlODBC) 新增至您安裝的 PostgreSQL。

![使用堆疊產生器安裝 PostgreSQL ODBC](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>或下載最新的 ODBC 驅動程式
或者，直接從下列 FTP 網站，下載適用於最新版 PostgreSQL ODBC 驅動程式 (psqlODBC) 的 Windows 安裝程式：[https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/)。 從 .zip 檔解壓縮檔案，並執行 .msi 檔案。

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>使用 PostgreSQL ODBC 驅動程式 (psqlODBC) 連線至 PostgreSQL
ODBC 驅動程式未列在資料來源的下拉式清單中。 若要使用 ODBC 驅動程式連線，請先在 [選擇資料來源] 或 [選擇目的地] 頁面上，將 [.NET Framework Data Provider for ODBC] 選取為資料來源。 此提供者作用為 ODBC 驅動程式的包裝函式。

以下是您選取 .NET Framework Data Provider for ODBC 之後立即看到的一般畫面。

![之前使用 ODBC 連線至 PostgreSQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>要指定的選項 (MySQL ODBC 驅動程式)

> [!NOTE]
> 不論 PostgreSQL 是您的來源還是目的地，此資料提供者和 ODBC 驅動程式的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源]  和 [選擇目的地]  頁面上看到的選項會相同。

若要使用 PostgreSQL ODBC 驅動程式連線至 PostgreSQL，請組合包含下列設定和其值的連接字串。 完整連接字串的格式緊接在設定清單後面。

> [!TIP]
> 取得組合正確連接字串的說明。 或者，您可以提供現有 DSN (資料來源名稱) 或建立新的 DSN，而不提供連接字串。 如需這些選項的詳細資訊，請參閱[連線至 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
ODBC 驅動程式的名稱，為 **PostgreSQL ODBC Driver(UNICODE)** 或 **PostgreSQL ODBC Driver(ANSI)** 。

**Server**  
PostgreSQL 伺服器的名稱。 

**通訊埠**  
用來連線至 PostgreSQL 伺服器的連接埠。

**Database**  
PostgreSQL 資料庫的名稱。

**Uid** 和 **Pwd**   
用來進行連線的 **Uid** (使用者識別碼) 和 **Pwd** (密碼)。

### <a name="connection-string-format"></a>連接字串格式
以下是一般連接字串的格式。 

```console
Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
```

### <a name="enter-the-connection-string"></a>輸入連接字串
在 [選擇資料來源] 或 [選擇目的地] 頁面上，於 [ConnectionString] 欄位中輸入連接字串，或在 [Dsn] 欄位中輸入 DSN 名稱。 輸入連接字串之後，精靈會剖析字串，並在清單中顯示個別屬性和屬性值。

下列範例使用此連接字串。

```console
Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
```

以下是您在輸入連接字串之後看到的畫面。

![使用 ODBC 連線至 PostgreSQL](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
若要了解如何使用此處未列出的資料提供者連線至 PostgreSQL 的資訊，請參閱 [PostgreSQL connection strings](https://www.connectionstrings.com/postgresql/) (PostgreSQL 連接字串)。 此協力廠商網站也會包含此頁面上所述之資料提供者和連線參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

