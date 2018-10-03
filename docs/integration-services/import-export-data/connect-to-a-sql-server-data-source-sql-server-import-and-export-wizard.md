---
title: 連線至 SQL Server 資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b49d5a4bee30a8fc5b225bf12e15c29bf942631b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47750556"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>連線至 SQL Server 資料來源 (SQL Server 匯入和匯出精靈)
本主題示範如何從 [SQL Server 匯入和匯出精靈] 的 [選擇資料來源] 或 [選擇目的地] 頁面中連線至 **Microsoft SQL Server** 資料來源。 您可以使用數個資料提供者來連線至 SQL Server。

> [!TIP]
> 如果您的網路具有多部伺服器，則輸入伺服器名稱會比展開伺服器下拉式清單更為簡單。 如果您按一下下拉式清單，查詢網路中所有可用的伺服器可能需要很多時間。

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用 .NET Framework Data Provider for SQL Server 連接到 SQL Server 
在您選取精靈的 [選擇資料來源] 或 [選擇目的地] 頁面上的 [.NET Framework Data Provider for SQL Server] 之後，頁面會顯示提供者的分組選項清單。 其中有許多是不友善的名稱和不熟悉的設定。 幸運的是，若要連線至任何企業資料庫，您通常只需要提供幾項資訊。 您可以忽略其他設定的預設值。

> [!NOTE]
> 不論 SQL Server 是您的來源還是目的地，此資料提供者的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

|必要資訊|.Net Framework Data Provider for SQL Server 屬性|
|---|---|
|伺服器名稱|**資料來源**|
|驗證 (登入) 資訊|[整合式安全性]；或 [使用者識別碼] 和 [密碼]<br/>如果您想要在伺服器上看到資料庫下拉式清單，則需要先提供有效的登入資訊。|
|資料庫名稱|**初始目錄**|

![使用 .NET 提供者連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>要指定的選項 (.NET Framework Data Provider for SQL Server)

> [!NOTE]
> 不論 SQL Server 是您的來源還是目的地，此資料提供者的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

**資料來源**  
 輸入來源或目的地伺服器的名稱或 IP 位址，或從下拉式清單中選取伺服器。  
 
 若要指定非標準 TCP 連接埠，請在伺服器名稱或 IP 位址後面輸入一個逗點，然後輸入連接埠號碼。
 
 **初始目錄**  
 輸入來源或目的地資料庫的名稱，或從下拉式清單中選取資料庫。  
  
 **整合式安全性**  
 指定 **True** 以使用 Windows 整合式驗證進行連線 (建議使用)，或指定 **False** 以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連線。 如果您指定 **False**，則必須輸入使用者識別碼和密碼。 預設值為 **[False]**。  
  
 **使用者識別碼**  
 如果您要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請輸入使用者名稱。  
  
 **密碼**  
 如果您要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請輸入密碼。  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>使用 SQL Server 的 ODBC 驅動程式連線至 SQL Server 
ODBC 驅動程式未列在下拉式資料來源清單中。 若要使用 ODBC 驅動程式連線，請從選取 **.NET Framework Data Provider for ODBC** 作為資料來源開始。 此提供者用作為 ODBC 驅動程式的包裝函式。

> [!TIP]
> **取得最新的驅動程式**. 下載 [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)。

以下是您選取 .NET Framework Data Provider for ODBC 之後立即看到的泛型畫面。

![之前使用 ODBC 連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>要指定的選項 (SQL Server 的 ODBC 驅動程式)

> [!NOTE]
> 不論 SQL Server 是您的來源還是目的地，此資料提供者的連線選項都會相同。 也就是，您在精靈的 [選擇資料來源] 和 [選擇目的地] 頁面上看到的選項會相同。

若要使用最新 ODBC 驅動程式連線至 SQL Server，請組合包含下列設定和其值的連接字串。 完整連接字串的格式緊接在設定清單後面。

> [!TIP]
> 取得組合正確連接字串的說明。 或者，您可以提供現有 DSN (資料來源名稱) 或建立新的 DSN，而不提供連接字串。 如需這些選項的詳細資訊，請參閱[連線至 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
ODBC 驅動程式的名稱。 針對不同版本的驅動程式，名稱會不同。

**Server**  
SQL Server 的名稱。

**[資料庫備份]**  
資料庫的名稱。  

**Trusted_Connection**；或 **Uid** 和 **Pwd**  
指定 **Trusted_Connection=Yes** 以與 Windows 整合式驗證連線；或者，指定 **Uid** (使用者識別碼) 和 **Pwd** (密碼) 以與 SQL Server 驗證連線。

### <a name="connection-string-format"></a>連接字串格式
以下是使用 Windows 整合式驗證的連接字串格式。

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

以下是使用 SQL Server 驗證的連接字串格式，而非 Windows 整合式驗證。

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>輸入連接字串
在 [選擇資料來源] 或 [選擇目的地] 頁面上，於 [ConnectionString] 欄位中輸入連接字串，或在 [Dsn] 欄位中輸入 DSN 名稱。 輸入連接字串之後，精靈會剖析字串，並在清單中顯示個別屬性和其值。

下列範例使用此連接字串。

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

以下是您在輸入連接字串之後看到的畫面。

![之後使用 ODBC 連線至 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>使用 Microsoft OLE DB Provider for SQL Server 或 SQL Server Native Client 連線至 SQL Server

> [!IMPORTANT]
> SQL Server 2012 之後的 SQL Server 版本不支援 Microsoft OLE DB Provider for SQL Server 和 SQL Server Native Client。 請改用 ODBC 驅動程式。 若要深入了解如何轉換至 ODBC 驅動程式，請參閱下列部落格文章。
>   -   [Microsoft 正在調整 ODBC 進行原生關聯式資料存取](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [介紹新 Microsoft ODBC Drivers for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
如需如何使用這裡未列出的資料提供者連線至 SQL Server 的資訊，請參閱 [SQL Server 連接字串](https://www.connectionstrings.com/sql-server/)。 此協力廠商網站也會包含此頁面上所述之資料提供者和連線參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

