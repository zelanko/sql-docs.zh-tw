---
title: "選擇資料來源 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.chooseadatasource.f1"
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 113
---
# 選擇資料來源 (SQL Server 匯入和匯出精靈)
  在 [歡迎使用] 頁面出現之後，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選擇資料來源]。 在此頁面上，您可以提供資料來源及其連接方式的相關資訊。
  
如需您可以使用之資料來源的資訊，請參閱[我可以使用哪些資料來源和目的地？](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>[選擇資料來源] 頁面的螢幕擷取畫面 
下列螢幕擷取畫面顯示精靈的 [選擇資料來源] 頁面中的第一個部分。

![選擇來源](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>選擇資料來源
 **資料來源**  
選取可連接到來源的資料提供者來指定資料來源。 在大部分情況下，您需要的資料提供者可透過其名稱一目暸然，因為提供者的名稱包含來源 (例如 SQL Server、Oracle、一般檔案、Excel 和 Access) 的名稱。

[資料來源] 清單中可用的資料提供者清單取決於您電腦上安裝的提供者。 這也取決於您執行的是 64 位元或 32 位元精靈。

您的資料來源可能有一個以上的提供者可用。 通常，您可以選取適用於來源的任何提供者。 例如，若要連接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、.NET Framework Data Provider for SQL Server 或 Microsoft OLE DB Provider for SQL Server。 

在某些情況下，您必須從泛型資料提供者開始選取。 例如，如果您有適用於資料來源的 ODBC 驅動程式，請選取 .NET Framework Data Provider for ODBC。  
 
針對某些資料來源，您可能必須從 Microsoft 或協力廠商下載資料提供者。 如需您可以使用之資料來源的資訊，請參閱[我可以使用哪些資料來源和目的地？](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)

## <a name="after-you-choose-a-data-source"></a>選擇資料來源之後
選擇資料來源之後，[選擇資料來源] 頁面屬性的其餘部分會有不同數目的選項，視您選擇的資料提供者而定。

下列各節列出一些經常使用之資料來源的重要選項。 這裡並未列出 [資料來源] 下拉式清單提供的所有來源。 如需其他提供者的其他選項，請參閱提供者特定文件。 
  
> [!TIP]  如果您的資料來源需要連接字串，您可以在下列協力廠商網站上找到範例 - [The Connection Strings Reference](https://www.connectionstrings.com/) (連接字串參考)。  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>使用 SQL Server Native Client 或 Microsoft OLE DB Provider for SQL Server 連接到 SQL Server  

SQL Server Native Client 和 Microsoft OLE DB Provider for SQL Server 會顯示一組相同的選項。 下列螢幕擷取畫面以 SQL Server Native Client 的選項為例。

![SQL Server 連接原生](../../integration-services/import-export-data/media/sql-server-connection-native.png)

 **伺服器名稱**  
 輸入包含資料之伺服器的名稱或 IP 位址，或者從清單中選擇伺服器。  
  
> [!NOTE] 如果您在具有多部伺服器的網路上，輸入伺服器名稱可能更容易。 如果您按一下下拉式清單，查詢網路中所有可用的伺服器可能需要很多時間，而且您的伺服器名稱可能不會列於結果中。

若要指定非標準的 TCP 連接埠，請在伺服器名稱或 IP 位址後輸入一個逗點，再輸入連接埠號碼。
  
 **使用 Windows 驗證**  
 指定精靈是否應使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證來登入資料庫。 建議使用 Windows 驗證，以獲得較佳的安全性。  
  
 **使用 SQL Server 驗證**  
 指定精靈是否應使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來登入資料庫。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  
  
 **資料庫**  
 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之指定執行個體上的資料庫清單中選取。  
  
 **重新整理**  
 按一下 [重新整理] 來重新整理可用資料庫的清單。  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用 .NET Framework Data Provider for SQL Server 連接到 SQL Server 

此頁面會呈現 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的選項群組清單。 此處列出重要的選項。 選取此提供者時所列出的其他選項通常非成功連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來源資料庫的必要選項。 

如需詳細資訊，請參閱 [.NET Framework Data Provider for SQL Server connection strings](https://www.connectionstrings.com/sqlconnection/)。

![SQL Server 連接網路](../../integration-services/import-export-data/media/sql-server-connection-net.png)
  
 **資料來源**  
 輸入包含資料之伺服器的名稱或 IP 位址，或者從清單中選擇伺服器。  
  
> [!NOTE] 如果您在具有多部伺服器的網路上，輸入伺服器名稱可能更容易。 如果您按一下下拉式清單，查詢網路中所有可用的伺服器可能需要很多時間，而且您的伺服器名稱可能不會列於結果中。  
 
 若要指定非標準的 TCP 連接埠，請在伺服器名稱或 IP 位址後輸入一個逗點，再輸入連接埠號碼。
 
 **初始目錄**  
 輸入來源資料庫的名稱，或從清單中選擇資料庫。  
  
 **整合式安全性**  
 指定 **True** 以使用 Windows 整合式驗證進行連接 (建議使用)，或指定 **False** 以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接。 如果您指定 **False**，則必須輸入使用者識別碼和密碼。 預設值為 **[False]**。  
  
 **使用者識別碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  

## <a name="oracle"></a>Oracle

使用 .NET Framework Data Provider for Oracle 或 Microsoft OLE DB Provider for Oracle 連接到 Oracle。 .NET Framework Data Provider for Oracle 設定起來比較容易，如下列螢幕擷取畫面所示。

如需詳細資訊，請參閱 [.NET Framework Data Provider for Oracle connection strings](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) 或 [Microsoft OLE DB Provider for Oracle connection strings](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/)。

![Oracle 連接](../../integration-services/import-export-data/media/oracle-connection.png)

## <a name="odbc-data-sources"></a>ODBC 資料來源

若要從提供 ODBC 驅動程式的任何來源載入資料，請選取 .NET Framework Data Provider for ODBC。

若要提供 ODBC 資料來源的連接字串，請參閱您要使用之 ODBC 驅動程式的文件，或在下列位置尋找範例 - [The Connection Strings Reference](https://www.connectionstrings.com/) (連接字串參考)。 

下列螢幕擷取畫面以 SQL Server 的 ODBC 連接為例。 範例中使用的連接字串如下：

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

在 [ConnectionString] 欄位中輸入連接字串之後，精靈會剖析字串，並在清單的 [其他] 區段中，顯示個別屬性及其值。

![ODBC 連接 SQL](../../integration-services/import-export-data/media/odbc-connection-sql.png)

## <a name="text-files-flat-files"></a>文字檔 (一般檔案)
 
 有數個頁面的選項供一般檔案資料來源使用。
 
 ### <a name="general-page"></a>[一般] 頁面
 在 [一般] 頁面上，瀏覽並選取檔案，然後確認 [格式] 區段中的設定。
 
 ![一般檔案連接一般](../../integration-services/import-export-data/media/flat-file-connection-general.png)  
   
如需 [一般] 頁面的詳細資訊，請參閱下列 Integration Services 參考頁面 - [一般檔案連線管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)。  

### <a name="columns-page"></a>資料行頁面

 在 [資料行] 頁面上，確認精靈已識別的資料行和分隔符號清單。
 
 ![一般檔案連接 (資料行)](../../integration-services/import-export-data/media/flat-file-connection-columns.png)
  
如需 [資料行] 頁面的詳細資訊，請參閱下列 Integration Services 參考頁面 - [一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)。

### <a name="advanced-page"></a>進階頁面

[進階] 頁面會顯示資料來源中每個資料行的詳細資訊，包括其資料類型和大小。

在下列螢幕擷取畫面中，請注意 [識別碼] 資料行一開始會有字串資料類型。

![一般檔案連接 (進階前)](../../integration-services/import-export-data/media/flat-file-connection-advanced-before.png)

按一下 [建議類型] 以顯示 [建議資料行類型] 對話方塊。 

![一般檔案連接建議](../../integration-services/import-export-data/media/flat-file-connection-suggest.png)

選擇在 [建議資料行類型] 對話方塊中的選項，並按一下 [確定] 之後，精靈可能會變更部分要匯入之資料行的資料類型。

下列螢幕擷取畫面顯示，精靈已辨識出資料來源中的 [識別碼] 資料行實際上是數字而不是文字字串，並且已將資料行的資料類型從字串變更為整數。

![一般檔案連接 (進階後)](../../integration-services/import-export-data/media/flat-file-connection-advanced-after.png)
  
如需 [進階] 頁面的詳細資訊，請參閱下列 Integration Services 參考頁面 - [一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)。

### <a name="preview-page"></a>預覽頁面

在 [預覽] 頁面上，確認資料行和範例資料的清單是否如您預期的一樣。

![一般檔案連接 (預覽)](../../integration-services/import-export-data/media/flat-file-connection-preview.png)

如需 [預覽] 頁面的詳細資訊，請參閱下列 Integration Services 參考頁面 - [一般檔案連接管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)。  
 
## <a name="microsoft-excel"></a>Microsoft Excel

下列螢幕擷取畫面顯示 Microsoft Excel 活頁簿的連接範例。

![Excel 連接](../../integration-services/import-export-data/media/excel-connection.png) 
 
 **Excel 檔案路徑**  
 指定要從中匯入資料之試算表的路徑和檔案名稱。 例如，本機電腦檔案為 **C:\\MyData.xlsx**，或網路共用檔案為 **\\\\Sales\\Database\\Northwind.xlsx**。 或按一下 [瀏覽]。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出試算表。  

> [!NOTE] 精靈無法開啟受密碼保護的 Excel 檔案。

 **Excel 版本**  
 選取來源活頁簿所使用的 Excel 版本。

您可能必須下載並安裝其他檔案，才能連接到您選取的 Excel 版本。 請參閱本頁面的[取得您需要的 Excel 和 Access 下載](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads)，以取得詳細資訊。

如果指定版本時發生問題，例如，因為有 Microsoft Office 365 而無法安裝 Access 2016 執行階段，請嘗試指定不同的版本，甚至是較舊的版本，例如 2013 而非 2016。

**第一個資料列有資料行名稱**  
指出來源資料的第一個資料列是否包含資料行名稱。
-   如果來源資料不包含資料行名稱，但您啟用了此選項，則精靈會將來源資料的第一列視為資料行名稱。
-   如果來源資料包含資料行名稱，但您停用了此選項，則精靈會將資料行名稱的資料列視為資料的第一列。

如果來源資料沒有資料行名稱，精靈會在內部使用 F1、F2 等作為暫時資料行標題。

## <a name="microsoft-access"></a>Microsoft Access  

下列螢幕擷取畫面顯示 Microsoft Access 資料庫的連接範例。

![存取連接](../../integration-services/import-export-data/media/access-connection.png)

 **檔案名稱**  
 指定要從中匯入資料之資料庫檔案的路徑和檔案名稱。 例如 **C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**。 或按一下 [瀏覽]。
 
 >   [!NOTE] 此精靈只能連接到 .MDB 檔案格式的 Access 資料庫。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出資料庫檔案。  
  
 **使用者名稱**  
當工作群組資訊檔案與資料庫相關聯時，請提供該資料庫連接的有效使用者名稱。  
  
 **密碼**  
當工作群組資訊檔案與資料庫相關聯時，請提供該資料庫連接的使用者密碼。
 
如果資料庫針對所有使用者都是用單一密碼來保護，請在 [資料連結屬性] 對話方塊中提供這個值。 若要開啟 [資料連結屬性] 對話方塊，請按一下 [進階]。  
  
 **進階**  
使用 [資料連結屬性] 對話方塊來指定進階選項，例如資料庫密碼或非預設工作群組資訊檔案。  
  
## <a name="a-nameofficedownloadsaget-the-downloads-you-need-for-excel-and-access"></a><a name="officeDownloads"></a>取得您需要的 Excel 和 Access 下載  
您可能必須下載 Microsoft Excel 和 Access 資料來源的連線元件，如果它們尚未安裝。

新版的元件可以開啟舊版程式所建立的檔案。 在某些情況下，新版的元件也可以開啟舊版程式所建立的檔案。  
  
如果電腦有 32 位元版的 Office，您就必須安裝 32 位元版的元件。 您也必須確保在 32 位元模式中執行精靈 (或它所建立的 Integration Services 套件)。  
|Microsoft Office 版本|下載|  
|------------------------------|--------------|  
|2007|[2007 Office System 驅動程式：資料連線元件](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 執行階段](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 執行階段](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 執行階段](https://www.microsoft.com/download/details.aspx?id=50040)|  
 
 
## <a name="azure-blob-storage"></a>Azure BLOB 儲存  
若要使用 Azure Blob 來源，您必須安裝 SSIS 的 Azure Feature Pack。 如需詳細資訊，請參閱 [Azure Feature Pack for Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。  

>   [!NOTE] 為了確保 Azure 儲存體連線管理員及使用它的元件 (包括 Blob 來源) 可同時連接到一般目的儲存體帳戶和 Blob 儲存體帳戶，請務必從[這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 如需這兩種儲存體帳戶類型的詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。

![Azure blob 儲存體連接](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

 **使用 Azure 帳戶**  
 指定是否要使用線上帳戶。
  
 **儲存體帳戶名稱**  
 指定 Azure 儲存體帳戶的名稱。  
  
**帳戶金鑰**  
提供 Azure 儲存體帳戶的金鑰。  
  
 **使用 HTTPS**  
 指定要使用 HTTP 或 HTTPS 連線到儲存體帳戶。  
  
 **使用本機開發人員帳戶**  
 指定是否在本機電腦上使用儲存體模擬器。  
  
 **Blob 容器名稱**  
 從指定儲存體帳戶的可用儲存體容器清單中選取。  
  
 **Blob 檔案格式**  
 選取 [文字] 或 [Avro] 檔案格式。  
  
 **資料行分隔符號字元**  
 如果您選取了 [文字] 格式，請指定資料行分隔符號字元。  
  
 **使用第一個資料列作為資料行名稱**  
 指定資料的第一個資料列是否包含資料行名稱。  
  
## <a name="whats-next"></a>下一步是什麼？  
 在您提供資料來源及其連接方式的相關資訊之後，下一個頁面為 [選擇目的地]。 在此頁面上，您可以提供資料目的地及其連接方式的相關資訊。 如需詳細資訊，請參閱[選擇目的地](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)。  
