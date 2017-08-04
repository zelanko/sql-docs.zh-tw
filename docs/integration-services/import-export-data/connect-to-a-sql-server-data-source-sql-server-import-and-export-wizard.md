---
title: "連接到 SQL Server 資料來源 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17910c8e30dee98f39e977896fb67774b54a798d
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>連接到 SQL Server 資料來源 （SQL Server 匯入和匯出精靈）
本主題說明如何連接到**Microsoft SQL Server**資料來源從**選擇資料來源**或**選擇目的地**SQL Server 匯入和匯出精靈 頁面。 有數個可讓您連接到 SQL Server 資料提供者。

> [!TIP]
> 如果您在具有多部伺服器的網路，可能很容易輸入伺服器名稱，而不是展開下拉式清單的伺服器。 如果您按一下下拉式清單，可能需要大量時間來查詢網路上的所有可用的伺服器，結果可能不包含您要的伺服器。

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用 .NET Framework Data Provider for SQL Server 連接到 SQL Server 
選取後**.NET Framework Data Provider for SQL Server**上**選擇資料來源**或**選擇目的地**頁面在精靈的頁面會顯示群組的提供者的選項清單。 其中有許多惡意的名稱和不熟悉的設定。 幸運的是，若要連接至企業中的任何資料庫，通常必須提供只有幾項資訊。 您可以忽略其他設定的預設值。

> [!NOTE]
> SQL Server 為您的來源或目的地連接選項，此資料提供者都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

|所需的資訊|.Net framework Data Provider for SQL Server 屬性|
|---|---|
|伺服器名稱|**資料來源**|
|驗證 （登入） 資訊|**整合式安全性**; 或者，**使用者識別碼**和**密碼**<br/>如果您想要在伺服器上看到資料庫的下拉式清單，您需要先提供有效的登入資訊。|
|資料庫名稱|**初始目錄**|

![使用.NET 提供者連接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>選項來指定 (.NET Framework Data Provider for SQL Server)

> [!NOTE]
> SQL Server 為您的來源或目的地連接選項，此資料提供者都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

**資料來源**  
 輸入名稱或 IP 位址在來源或目的地伺服器，或從下拉式清單中選取伺服器。  
 
 若要指定非標準的 TCP 連接埠，輸入逗號之後的伺服器名稱或 IP 位址，然後輸入連接埠號碼。
 
 **初始目錄**  
 輸入來源或目的地資料庫的名稱，或從下拉式清單中選取資料庫。  
  
 **整合式安全性**  
 指定**True**連接使用 Windows 整合式驗證 （建議），或**False**要用來連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果您指定 **False**，則必須輸入使用者識別碼和密碼。 預設值為 **[False]**。  
  
 **使用者識別碼**  
 輸入使用者名稱，如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。  
  
 **密碼**  
 輸入的密碼，如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>連接到 SQL Server ODBC driver for SQL Server 
ODBC 驅動程式未列在下拉式清單中的資料來源。 若要連接的 ODBC 驅動程式，一開始選取**.NET Framework Data Provider for ODBC**做為資料來源。 此提供者做為包裝函式，ODBC 驅動程式。

> [!TIP]
> **取得最新的驅動程式**。 下載[Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)。

以下是您選取.NET Framework Data Provider for ODBC 之後，立即會看到泛用螢幕。

![連接到使用之前的 ODBC SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>選項來指定 （適用於 SQL Server ODBC 驅動程式）

> [!NOTE]
> SQL Server 為您的來源或目的地的 ODBC 驅動程式的連接選項都是相同的。 也就是您所看到的選項會同時針對相同**選擇資料來源**和**選擇目的地**精靈頁面。

若要連接到 SQL Server 的最新的 ODBC 驅動程式，組合連接字串，其中包含下列設定，以及它們的值。 完整的連線字串的格式緊接在後面設定的清單。

> [!TIP]
> 取得說明組裝正確的連接字串。 或者，而不是提供的連接字串，提供現有的資料來源名稱 （資料來源名稱），或另外新建一個。 如需這些選項的詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。

**驅動程式**  
ODBC 驅動程式的名稱。 名稱是不同的不同版本的驅動程式。

**Server**  
SQL Server 名稱。

**資料庫**  
資料庫的名稱。  

**Trusted_Connection**; 或者， **Uid**和**Pwd**  
指定**Trusted_Connection = Yes**來連接使用 Windows 整合式驗證; 或指定**Uid** （使用者識別碼） 和**Pwd** （密碼） 會透過 SQL Server 驗證進行連接。

### <a name="connection-string-format"></a>連接字串格式
以下是使用 Windows 整合式的驗證的連接字串的格式。

    Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;

以下是使用 SQL Server 驗證，而不是 Windows 整合式驗證的連接字串的格式。

     Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;

### <a name="enter-the-connection-string"></a>輸入連接字串
輸入中的連接字串**ConnectionString**欄位，或輸入中的 DSN 名稱**Dsn**欄位上**選擇資料來源**或**選擇目的地**頁面。 您輸入的連接字串之後，精靈會剖析字串，並會顯示個別的屬性及其值清單中。

下列範例會使用此連接字串。

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

以下是您輸入的連接字串之後，請參閱螢幕。

![連接到 SQL 搭配 ODBC 之後](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>SQL Server 或 SQL Server Native Client 連接至 SQL Server 的 Microsoft OLE DB 提供者

> [!IMPORTANT]
> Microsoft OLE DB Provider for SQL Server 和 SQL Server Native Client 不支援在 SQL Server 版本的 SQL Server 2012 之後。 請改用 ODBC 驅動程式。 若要了解有關轉換至 ODBC 驅動程式的詳細資訊，請參閱下列部落格文章。
>   -   [Microsoft 正在調整 ODBC 進行原生關聯式資料存取](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [介紹新的 Microsoft ODBC Driver for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>其他資料提供者和其他資訊
如需如何連接到 SQL Server 未在此處列出的資料提供者資訊，請參閱[SQL Server 連接字串](https://www.connectionstrings.com/sql-server/)。 此第三方網站也會包含資料提供者和描述在此頁面上的連接參數的詳細資訊。

## <a name="see-also"></a>另請參閱
[選擇資料來源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


