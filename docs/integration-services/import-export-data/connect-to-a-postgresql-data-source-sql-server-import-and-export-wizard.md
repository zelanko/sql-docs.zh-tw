---
title: "連接到 PostgreSQL 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c82ae7eedc3e18e7591cf7ab30a507920695247
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>連接到 PostgreSQL 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**PostgreSQL**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。 

> [!IMPORTANT]
> 詳細的需求和必要條件 PostgreSQL 資料庫連接等已超出 Microsoft 本文的範圍。 本文假設您已經安裝 PostgreSQL 用戶端軟體，而且，您可以已成功連接到目標 PostgreSQL 資料庫。 如需詳細資訊，請參閱 PostgreSQL 資料庫管理員或 PostgreSQL 文件。

## <a name="get-the-postgresql-odbc-driver"></a>取得 PostgreSQL ODBC 驅動程式

### <a name="install-the-odbc-driver-with-stack-builder"></a>安裝 ODBC 驅動程式堆疊產生器
執行將 PostgreSQL ODBC 驅動程式 (psqlODBC) 新增至您安裝的 PostgreSQL 堆疊產生器。

![使用堆疊產生器安裝 PostgreSQL ODBC](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>或者，您也可以下載最新的 ODBC 驅動程式
或者，您也可以直接從這個 FTP 站台-下載 PostgreSQL ODBC 驅動程式 (psqlODBC) 的最新版本的 Windows 安裝程式[https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/)。 從.zip 檔解壓縮檔案，並執行.msi 檔案。

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>連接到 PostgreSQL PostgreSQL ODBC 驅動程式 (psqlODBC)
ODBC 驅動程式未列在下拉式清單中的資料來源。 若要連接的 ODBC 驅動程式，一開始選取**.NET Framework Data Provider for ODBC**做為資料來源上**選擇資料來源**或**選擇目的地**頁面。 此提供者做為包裝函式，ODBC 驅動程式。

以下是您選取.NET Framework Data Provider for ODBC 之後，立即會看到泛用螢幕。

![連接到使用之前的 ODBC PostgreSQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>選項來指定 （PostgreSQL ODBC 驅動程式）

> [!NOTE]
> PostgreSQL 為您的來源或目的地，此資料提供者和 ODBC 驅動程式的連接選項都相同。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

若要連線到 PostgreSQL PostgreSQL ODBC 驅動程式，組合連接字串，其中包含下列設定，以及它們的值。 完整的連線字串的格式緊接在後面設定的清單。

> [!TIP]
> 取得說明組裝正確的連接字串。 或者，而不是提供的連接字串，提供現有的資料來源名稱 （資料來源名稱），或另外新建一個。 如需這些選項的詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
名稱的 ODBC 驅動程式-請**PostgreSQL ODBC Driver(UNICODE)**或**PostgreSQL ODBC Driver(ANSI)**。

**Server**  
PostgreSQL 伺服器的名稱。 

**通訊埠**  
用來連接到 PostgreSQL 伺服器連接埠。

**資料庫**  
PostgreSQL 資料庫的名稱。

**Uid**和**Pwd**   
**Uid** （使用者識別碼） 和**Pwd** （密碼） 來連接。

### <a name="connection-string-format"></a>連接字串格式
以下是一般連接字串的格式。 

    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>

### <a name="enter-the-connection-string"></a>輸入連接字串
輸入中的連接字串**ConnectionString**欄位，或輸入中的 DSN 名稱**Dsn**欄位上**選擇資料來源**或**選擇目的地**頁面。 您輸入的連接字串之後，精靈會剖析字串，並會顯示個別的屬性及其值清單中。

下列範例會使用此連接字串。

    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********

以下是您輸入的連接字串之後，請參閱螢幕。

![連接到使用 ODBC PostgreSQL](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
如需如何連接到 PostgreSQL 此處未列出的資料提供者資訊，請參閱[PostgreSQL 連接字串](https://www.connectionstrings.com/postgresql/)。 此第三方網站也會包含資料提供者和描述在此頁面上的連接參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


