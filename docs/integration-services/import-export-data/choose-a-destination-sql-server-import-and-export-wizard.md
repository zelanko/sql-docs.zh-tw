---
title: "選擇目的地 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
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
  - "sql13.dts.impexpwizard.chooseadestination.f1"
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 95
---
# 選擇目的地 (SQL Server 匯入和匯出精靈)
 在您提供有關資料來源及其連接方式的資訊之後，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [選擇目的地]。 在此頁面上，您可以提供資料目的地及其連接方式的相關資訊。
  
如需您可以使用之資料目的地的資訊，請參閱[我可以使用哪些資料來源和目的地？](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)。 

## <a name="screen-shot-of-the-destination-page"></a>[目的地] 頁面的螢幕擷取畫面
下列螢幕擷取畫面顯示精靈的 [選擇目的地] 頁面中的第一個部分。

![選擇目的地](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>選擇目的地
 **目的地**  
 選取可將資料匯入目的地的資料提供者來指定目的地。 在大部分情況下，您需要的資料提供者可透過其名稱一目暸然，因為提供者的名稱包含目的地 (例如 SQL Server、Oracle、一般檔案、Excel 和 Access) 的名稱。
 
[目的地] 清單中可用的資料提供者清單取決於您電腦上安裝的提供者。 這也取決於您執行的是 64 位元或 32 位元精靈。

您的目的地可能有一個以上的提供者可用。 通常，您可以選取適用於目的地的任何提供者。 例如，若要連接到 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、.NET Framework Data Provider for SQL Server 或 Microsoft OLE DB Provider for SQL Server。
 
在某些情況下，您必須從泛型資料提供者開始選取。 例如，如果您有適用於目的地的 ODBC 驅動程式，請選取 .NET Framework Data Provider for ODBC。

針對某些目的地，您可能必須從 Microsoft 或協力廠商下載資料提供者。 如需您可以使用之資料目的地的資訊，請參閱[我可以使用哪些資料來源和目的地？](Import%20and%20Export%20Data%20with%20the%20SQL%20Server%20Import%20and%20Export%20Wizard.md\#wizardSources)。

## <a name="after-you-choose-a-destination"></a>選擇目的地之後
選擇目的地之後，[選擇目的地] 頁面屬性的其餘部分會有不同數目的選項，視您選擇的資料提供者而定。

下列各節列出一些經常使用之目的地的重要選項。 這裡並未列出 [目的地] 下拉式清單提供的所有目的地。 如需其他提供者的其他選項，請參閱提供者特定文件。

> [!TIP] 如果您的目的地需要連接字串，您可以在下列協力廠商網站上找到範例 - [The Connection Strings Reference](https://www.connectionstrings.com/)。  

## <a name="microsoft-sql-server"></a>Microsoft SQL Server 

如果您想要建立新的 SQL Server 資料庫作為目的地，請選取 SQL Server Native Client 或 Microsoft OLE DB Provider for SQL Server。 如果您選取 .NET Framework Data Provider for SQL Server，則無法使用此選項來建立新的資料庫。  

### <a name="connect-to-sql-server-with-sql-server-native-client-or-the-microsoft-ole-db-provider-for-sql-server"></a>使用 SQL Server Native Client 或 Microsoft OLE DB Provider for SQL Server 連接到 SQL Server  

SQL Server Native Client 和 Microsoft OLE DB Provider for SQL Server 會顯示一組相同的選項。 下列螢幕擷取畫面以 SQL Server Native Client 的選項為例。

![SQL 原生目的地](../../integration-services/import-export-data/media/sql-native-destination.png)

 **伺服器名稱**  
 輸入目的地伺服器的名稱或 IP 位址，或從清單中選擇伺服器。  
  
> [!NOTE] 如果您在具有多部伺服器的網路上，輸入伺服器名稱可能更容易。 如果您按一下下拉式清單，查詢網路中所有可用的伺服器可能需要很多時間，而且您的伺服器名稱可能不會列於結果中。  
 
 若要指定非標準的 TCP 連接埠，請在伺服器名稱或 IP 位址後輸入一個逗點，再輸入連接埠號碼。
 
 **使用 Windows 驗證**  
 指定精靈是否應使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證來登入資料庫。 建議使用 Windows 驗證。  
  
 **使用 SQL Server 驗證**  
 指定精靈是否應使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來登入資料庫。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，就必須提供使用者名稱和密碼。  
  
 **使用者名稱**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  
  
 **資料庫**  
 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之指定執行個體上的資料庫清單中選取。  
  
 **重新整理**  
 按一下 [重新整理] 來還原可用資料庫的清單。  
  
### <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>使用 .NET Framework Data Provider for SQL Server 連接到 SQL Server 

此頁面會呈現 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的選項群組清單。 此處列出重要的選項。 您不需要選取此提供者時所列出的其他選項，即可成功連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地資料庫。 

如需詳細資訊，請參閱 [.NET Framework Data Provider for SQL Server connection strings](https://www.connectionstrings.com/sqlconnection/)。

![SQL Server 目的地網路](../../integration-services/import-export-data/media/sql-server-destination-net.png)
  
 **目的地**  
 輸入目的地伺服器的名稱或 IP 位址，或從清單中選擇伺服器。  
  
> [!NOTE] 如果您在具有多部伺服器的網路上，輸入伺服器名稱可能更容易。 如果您按一下下拉式清單，查詢網路中所有可用的伺服器可能需要很多時間，而且您的伺服器名稱可能不會列於結果中。  
 
 若要指定非標準的 TCP 連接埠，請在伺服器名稱或 IP 位址後輸入一個逗點，再輸入連接埠號碼。
 
 **初始目錄**  
 輸入目的地資料庫的名稱，或從清單中選擇資料庫。  
  
 **整合式安全性**  
 指定 **True** 以使用 Windows 整合式驗證進行連接 (建議使用)，或指定 **False** 以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接。 如果您指定 **False**，則必須輸入使用者識別碼和密碼。 預設值為 **[False]**。  
  
 **使用者識別碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的使用者名稱。  
  
 **密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，請提供資料庫連接的密碼。  

## <a name="oracle"></a>Oracle

使用 .NET Framework Data Provider for Oracle 或 Microsoft OLE DB Provider for Oracle 連接到 Oracle。 .NET Framework Data Provider for Oracle 設定起來比較容易，如下列螢幕擷取畫面所示。

如需詳細資訊，請參閱 [.NET Framework Data Provider for Oracle connection strings](https://www.connectionstrings.com/net-framework-data-provider-for-oracle/) 或 [Microsoft OLE DB Provider for Oracle connection strings](https://www.connectionstrings.com/microsoft-ole-db-provider-for-oracle-msdaora/)。

![Oracle 目的地](../../integration-services/import-export-data/media/oracle-destination.png)

## <a name="odbc-destinations"></a>ODBC 目的地

若要將資料儲存至提供 ODBC 驅動程式的任何目的地，請選取 .NET Framework Data Provider for ODBC。

若要提供 ODBC 目的地的連接字串，請參閱您要使用之 ODBC 驅動程式的文件，或在下列位置尋找範例 - [The Connection Strings Reference](https://www.connectionstrings.com/)。 

下列螢幕擷取畫面以 SQL Server 的 ODBC 連接為例。 範例中使用的連接字串如下：

    Driver={SQL Server};Server=(local);Database=TestData;Trusted_Connection=Yes;

在 [ConnectionString] 欄位中輸入連接字串之後，精靈會剖析字串，並在清單的 [其他] 區段中，顯示個別屬性及其值。

![ODBC 連接 SQL 目的地](../../integration-services/import-export-data/media/odbc-connection-sql-destination.png)

 ## <a name="text-files-flat-files"></a>文字檔 (一般檔案)
 
![一般檔案目的地](../../integration-services/import-export-data/media/flat-file-destination.png)  

**檔案名稱**  
 指定儲存資料之檔案的路徑和檔案名稱。 或按一下 [瀏覽] 找出檔案。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出檔案。  
  
 **地區設定**  
 指定用來定義字元排序順序及日期和時間格式的地區設定識別碼 (LCID)。  
  
 **Unicode**  
 指出是否使用 Unicode。 如果使用 Unicode，您就不必指定字碼頁。  
  
 **字碼頁**  
 指定您要使用之語言的字碼頁。  
  
 **格式**  
 指出是要使用分隔符號、固定寬度或不齊右的格式。  
  
|Value|說明|  
|-----------|-----------------|  
|使用分隔符號|資料行是以分隔符號分隔。|  
|固定寬度|資料行具有固定寬度。|  
|不齊右|不齊右檔案就是除了最後一個資料行是由資料列分隔符號所分隔之外，其他所有資料行都有固定寬度的檔案。|  
  
 **文字限定詞**  
 輸入要使用的文字限定詞。 例如，您可以指定每一個文字資料行都加上引號。  
  
 **第一個資料列的資料行名稱**  
 指出是否在第一個資料列顯示資料行名稱。  
 
 ## <a name="microsoft-excel"></a>Microsoft Excel

>  **影片**：精靈的常見用法是將資料匯出至 Excel。 以下是來自 YouTube 的四分鐘影片，說明如何使用清楚簡單的指示來執行這項作業。 [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (使用 SQL Server 匯入和匯出精靈匯出至 Excel)。 (影片使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2012。)

下列螢幕擷取畫面顯示 Microsoft Excel 活頁簿的連接範例。

![Excel 目的地](../../integration-services/import-export-data/media/excel-destination.png) 
 
 **Excel 檔案路徑**  
 指定要匯出資料之目的地試算表的路徑和檔案名稱。 例如，本機電腦檔案為 **C:\\MyData.xlsx**，或網路共用檔案為 **\\\\Sales\\Database\\Northwind.xlsx**。 或按一下 [瀏覽]。   
  
 **瀏覽**  
 使用 [開啟] 對話方塊來找出試算表。  

> [!NOTE] 精靈無法開啟受密碼保護的 Excel 檔案。

 **Excel 版本**  
選取目的地活頁簿所使用的 Excel 版本。  

您可能必須下載並安裝其他檔案，才能連接到您選取的 Excel 版本。 請參閱本頁面的[取得您需要的 Excel 和 Access 下載](Choose%20a%20Data%20Source%20\%28SQL%20Server%20Import%20and%20Export%20Wizard%29.md\#officeDownloads)，以取得詳細資訊。

如果指定版本時發生問題，例如，因為有 Microsoft Office 365 而無法安裝 Access 2016 執行階段，請嘗試指定不同的版本，甚至是較舊的版本，例如 2013 而非 2016。

**第一個資料列有資料行名稱**  
此選項似乎對 Excel 目的地沒有影響。 如果目的地沒有資料行名稱，即使啟用此選項，驅動程式也不會輸出資料行名稱。 對內部而言，精靈會使用 F1、F2 等作為暫時的資料行標題。
 
## <a name="microsoft-access"></a>Microsoft Access  

下列螢幕擷取畫面顯示 Microsoft Access 資料庫的範例連接。

![Access 目的地](../../integration-services/import-export-data/media/access-destination.png)

 **檔案名稱**  
 指定要匯出資料之目的地資料庫檔案的路徑和檔案名稱。 例如，**C:\MyData.mdb, \\\Sales\Database\Northwind.mdb**。 或按一下 [瀏覽]。
 
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
若要使用 Azure Blob 目的地，您必須安裝 SSIS 的 Azure 功能套件。 如需詳細資訊，請參閱 [Azure Feature Pack for Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。  

>   [!NOTE] 為了確保 Azure 儲存體連線管理員及使用它的元件 (包括 Blob 目的地) 可同時連接到一般目的儲存體帳戶和 Blob 儲存體帳戶，請務必從[這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 如需這兩種儲存體帳戶類型的詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。

![Azure Blob 目的地](../../integration-services/import-export-data/media/azure-blob-destination.png)

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

## <a name="whats-next"></a>下一步  
 在您提供有關資料目的地及其連接方式的資訊之後，下一個頁面是 [指定資料表複製或查詢]。 在此頁面上，您可以指定要複製整個資料表或只複製特定資料列。 如需詳細資訊，請參閱[指定資料表複製或查詢](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)。  
