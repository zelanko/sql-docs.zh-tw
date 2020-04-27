---
title: SQLXML 4.0 SP1 的新功能&#39;Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- SQLNCLI, SQLXML
- what's new [SQLXML]
- SQLXML, what's new
- migrating SQLXML applications
- redistributing SQLXML
- SQL Server Native Client, SQLXML
- side-by-side installations [SQLXML]
ms.assetid: 48f7720b-1705-402d-93ce-097ff1737877
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ca2bc726b0bf017ec4b3dd0451313d60ef57696
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012135"
---
# <a name="what39s-new-in-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 的新功能&#39;
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 SP1 包含不同的更新和增強功能。 本主題摘要說明更新並提供詳細資訊的連結 (如果有的話)。 SQLXML 4.0 SP1 會提供其他的增強功能以支援 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中導入的新資料類型。 本主題包含下列主旨：  
  
-   安裝 SQLXML 4.0 SP1  
  
-   並存安裝問題  
  
-   SQLXML 4.0 和 MSXML  
  
-   轉散發 SQLXML 4.0  
  
-   Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的支援  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所導入資料類型的支援  
  
-   SQLXML 4.0 的 XML 大量載入變更  
  
-   SQLXML 4.0 的登錄機碼變更  
  
-   移轉問題  
  
## <a name="installing-sqlxml-40-sp1"></a>安裝 SQLXML 4.0 SP1  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前的版本中，SQLXML 4.0 隨附於 SQL Server 而且是所有 SQL Server 版本 (SQL Server Express 除外) 之預設安裝的一部分。 不過，從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，SQL Server 已不再包含最新版的 SQLXML (SQLXML 4.0 SP1)。 若要安裝 SQLXML 4.0 SP1，請從[sqlxml 4.0 sp1 的安裝位置](https://www.microsoft.com/download/details.aspx?id=30403)下載。  
  
 SQLXML 4.0 SP1 檔案也會安裝於下列位置：  
  
 `%PROGRAMFILES%\SQLXML 4.0\`  
  
> [!NOTE]  
>  所有適當的 SQLXML 4.0 登錄設定都會在安裝程序時進行。  
  
 若要允許 32 位元 SQLXML 應用程式在 64 位元 Windows 作業系統上的 Windows on Windows (WOW64) 下執行，請執行 64 位元 SQLXML 4.0 SP1 封裝 (名稱為 sqlxml4.msi)，您可以在下載中心取得該封裝。  
  
#### <a name="uninstalling-sqlxml-40-sp1"></a>解除安裝 SQLXML 4.0 SP1  
 共用登錄機碼存在於 SQLXML 3.0 SP3、SQLXML 4.0 及 SQLXML 4.0 SP1 之間。 如果包含 SQLXML 3.0 SP3 的相同電腦上已解除安裝 SQLXML 更新版本，您可能需要重新安裝 SQLXML 3.0 SP3。  
  
## <a name="side-by-side-installation-issues"></a>並存安裝問題  
 SQLXML 4.0 的安裝程序不會移除舊版 SQLXML 所安裝的檔案。 因此，您的電腦上可能有數個不同版本之 SQLXML 安裝的 DLL。 您可以並行執行這些安裝。 SQLXML 4.0 會同時包含與版本無關和與版本相關的 PROGID。 所有的實際執行應用程式都應該使用與版本相關的 PROGID。  
  
## <a name="sqlxml-40-sp1-and-msxml"></a>SQLXML 4.0 SP1 和 MSXML  
 SQLXML 4.0 不會安裝 MSXML。 SQLXML 4.0 會使用 MSXML 6.0，這會安裝為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本安裝的一部分。  
  
## <a name="redistributing-sqlxml-40-sp1"></a>轉散發 SQLXML 4.0 SP1  
 您可以使用可轉散發安裝程式套件散發 SQLXML 4.0 SP1。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱＜撰寫適用於 Visual Studio 2005 的自訂啟動載入器封裝＞和＜加入自訂的必要條件＞。  
  
 如果應用程式的目標使用平台與當初開發時的平台不同，您可以從 Microsoft 下載中心下載 x64、Itanium 和 x86 版本的 sqlncli.msi。  
  
 MSXML 6.0 (msxml6.msi) 也有個別的轉散發安裝程式。 您可以在下列位置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝光碟片上找到這些程式：  
  
 `%CD%\Setup\`  
  
 這些安裝檔案可以用於直接從光碟片安裝 MSXML 6.0， 也可以用於搭配您自訂的應用程式隨意同時轉散發 MSXML 6.0 和 SQLXML 4.0 SP1。  
  
 如果您要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 當做應用程式的資料提供者，則也需要轉散發該程式。 如需詳細資訊，請參閱 [安裝 SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md)。  
  
## <a name="support-for-sql-server-native-client"></a>SQL Server Native Client 的支援  
 SQLXML 4.0 同時支援 SQLOLEDB 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 提供者。 建議您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相同版本的 native client 提供者， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client 的開發目的是要支援伺服器隨附的任何新資料類型，例如中`Date, Time` `DateTime2` `dateTimeOffset` [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]的、和資料類型，以及[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client 所支援的。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入的資料存取技術。 此項技術將 SQLOLEDB Provider 與 SQLODBC Driver 合而為一，成為原生的動態連結程式庫 (DLL)，同時也提供了獨立而有別於 Microsoft Data Access Components (MDAC) 的新功能。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 可用於建立新的應用程式，或者加強需要利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所導入功能 (不受 MDAC 中的 SQLOLEDB 和 SQLODBC 以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 支援) 的現有應用程式。 例如，用戶端的 SQLXML 功能 (例如 FOR XML) 需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 才能使用 `xml` 資料類型。 如需詳細資訊，請參閱[用戶端 XML 格式 &#40;SQLXML 4.0&#41;](formatting/client-side-xml-formatting-sqlxml-4-0.md)、[使用 ADO 執行 SQLXML 4.0 查詢](using-ado-to-execute-sqlxml-4-0-queries.md)，以及[SQL Server Native Client 程式設計](../native-client/sql-server-native-client-programming.md)。  
  
> [!NOTE]  
>  SQLXML 4.0 並非完全與 SQLXML 3.0 回溯相容。 因為某些錯誤修正和其他的功能性變更 (特別是 SQLXML ISAPI 支援的移除)，您無法將 IIS 虛擬目錄用於 SQLXML 4.0。 雖然大部分的應用程式都可以在稍加修改後執行，但在將這些應用程式放入使用 SQLXML 4.0 的生產環境之前，必須先加以測試。  
  
## <a name="support-for-data-types-introduced-in-sql-server-2005-and-sql-server-2008"></a>支援 SQL Server 2005 及 SQL Server 2008 中導入的資料類型  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]引進了`xml`資料類型，而 SQLXML 4.0 支援`xml`資料類型。 如需詳細資訊，請參閱[SQLXML 4.0 中的 Xml 資料類型支援](xml-data-type-support-in-sqlxml-4-0.md)。  
  
 如需如何在對應 XML 檢視、大量載入 XML 或執行 XML Updategram 時使用 SQLXML 中的 `xml` 資料類型的範例，請參閱下列主題所提供的範例。  
  
-   [XSD 元素和屬性對資料表和資料行的預設對應](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
-   [使用 XML Updategram 插入資料](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
  
-   [大量載入 XML 文件的範例](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]引進了`Date, Time`、 `DateTime2`和**DateTimeOffset**資料類型。 搭配 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中隨附的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client OLE DB 提供者 (SQLNCLI11) 使用時，SQLXML 4.0 SP1 會將這四個新的資料類型啟用成內建的純量類型。  
  
## <a name="xml-bulk-load-changes-for-sqlxml-40-sp1"></a>SQLXML 4.0 SP1 的 XML 大量載入變更  
  
-   對於 SQLXML 4.0，SchemaGen 溢位欄位是使用`xml`資料類型建立的。 如需詳細資訊，請參閱[SQL SERVER XML 大量載入物件模型](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md)。  
  
-   如果您先前已經建立了 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 應用程式而您想要使用 SQLXML 4.0，則必須使用 Xblkld4.dll 的參考來重新編譯應用程式。  
  
-   對於 Visual Basic Scripting Edition 應用程式，則必須註冊您要使用的 DLL。 在下列範例中，如果您指定與版本無關的 PROGID，則應用程式會相依於最後註冊的 DLL：  
  
    ```  
    set objBulkLoad = CreateObject("SQLXMLBulkLoad.SQLXMLBulkLoad")   
    ```  
  
    > [!NOTE]  
    >  與版本相關的 PROGID 是 SQLXMLBulkLoad.SQLXMLBulkLoad.4.0。  
  
## <a name="registry-key-changes-for-sqlxml-40"></a>SQLXML 4.0 的登錄機碼變更  
 在 SQLXML 4.0 中，登錄機碼已從舊版變更為下列項目：  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\SchemaCacheSize  
  
 如果您想要這些機碼在 SQLXML 4.0 中生效，就必須變更設定。  
  
 此外，SQLXML 4.0 還導入了下列的登錄機碼：  
  
-   `HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\ReportErrorsWithSQLInfo`  
  
     根據預設，SQLXML 4.0 會傳回 OLE DB 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所提供的原生錯誤資訊，而不是高層級的 SQLXML 錯誤 (舊版 SQLXML 才會提供此類錯誤)。 如果您不要這項行為，則 DWORD 類型的這個登錄機碼值必須設定為 0 (值設值為 1)。  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\FORXML_GenerateGUIDBraces  
  
     根據預設，SQLXML 會傳回 SQL Server GUID 值，但沒有外面的大括號。 如果您想要以大括弧傳回 GUID 值（例如，{*某個 guid*}），則此登錄機碼的值必須設定為1（預設值為0）。  
  
-   HKEY_LOCAL_MACHINE\Software\Microsoft\MSSQLServer\Client\SQLXML4\SQL2000CompatMode  
  
     根據預設，當 XML 剖析器載入資料時，空格會根據 XML 1.0 規則而正規化。 這會導致資料中的某些空白字元遺失。 因此，資料的文字表示法在剖析之後可能不會相同，雖然資料在語意上是相同的。  
  
     導入這個機碼的原因，是讓您可以選擇保有資料中的空白字元。 如果加入這個登錄機碼並將其值設定為 0，則 XML 中的空白字元 (LF、CR 和索引標籤) 會編碼傳回 (如果使用屬性值)。 如果使用元素值，則只有 CR 會編碼傳回。  
  
     例如：  
  
    ```  
    CREATE TABLE T( Col1 int, Col2 nvarchar(100));  
    GO  
    -- Insert data with tab, line feed and carriage return).  
    INSERT INTO T VALUES (1, 'This is a tab    . This is a line feed and CR   
     more text');  
    GO  
    -- Test this query (without the registry key).  
    SELECT * FROM T   
    FOR XML AUTO;  
    -- This is the result (no encoding of special characters).  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
    -- Now add registry key with value 0 and execute the query again.  
    -- Note the encoding for carriage return, line-feed and tab in the attribute value.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
      <T Col1="1"   
         Col2="This is a tab    . This is a line feed and CR   
     more text"/>  
    </r>  
  
    -- Update the query and specify ELEMENTS directive  
    SELECT * FROM T  
    FOR XML AUTO, ELEMENTS  
    -- Only the carriage return is returned encoded.  
    <?xml version="1.0" encoding="utf-8" ?>  
    <r>  
       <T>  
          <Col1>1</Col1>  
          <Col2>This is a tab    . This is a line feed and CR   
     more text</Col2>  
       </T>  
    </r>  
    ```  
  
## <a name="migration-issues"></a>移轉問題  
 下列問題可能會影響舊版 SQLXML 應用程式到 SQLXML 4.0 的移轉。  
  
### <a name="ado-and-sqlxml-40-queries"></a>ADO 和 SQLXML 4.0 查詢  
 在舊版的 SQLXML 中，支援使用 IIS 虛擬目錄和 SQLXML ISAPI 篩選來執行以 URL 為基礎的查詢。 對於使用 SQLXML 4.0 的應用程式，已不再提供這項支援。  
  
 反而可以利用在 Microsoft Data Access Components (MDAC) 2.6 和更新版本中初次導入的 ActiveX Data Objects (ADO) 的 SQL XML 延伸模組來執行 SQLXML 查詢、範本和 Updategram。  
  
 如需詳細資訊，請參閱[使用 ADO 執行 SQLXML 4.0 查詢](using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="supportability-for-sqlxml-30-isapi-and-data-types-introduced-in-sql-server-2005"></a>SQL Server 2005 所導入之 SQLXML 3.0 ISAPI 和資料類型的可支援性  
 因為 ISAPI 支援已從 SQLXML 4.0 中移除，所以如果您的方案需要[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]所導入的增強型資料類型功能（例如[xml 資料類型](/sql/t-sql/xml/xml-transact-sql)或[使用者定義資料類型（udt）](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)和 Web 型存取），您就必須使用另一個解決方案，例如[SQLXML managed 類別](../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)或其他類型的 HTTP 處理常式（例如 SQL Server 2005 的原生 xml Web service）。  
  
 或者，如果您不需要這些類型延伸模組，可以繼續使用 SQLXML 3.0 來連接[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]安裝。 SQLXML 3.0 ISAPI 支援可以用於這些較新的版本，但並不能支援或辨識 `xml` 中導入的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料類型或 UDT 類型支援。  
  
### <a name="xml-bulk-load-security-changes-for-temporary-files"></a>暫存檔案的 XML 大量載入安全性變更  
 對於 SQLXML 4.0 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，XML 大量載入檔案權限會授與執行大量載入作業的使用者。 讀取和寫入權限則是繼承自檔案系統。 在舊版的 SQLXML 和 SQL Server 中，在 SQLXML 下進行 XML 大量載入會建立暫存檔，這些暫存檔並未受到保護，可由任何人讀取。  
  
### <a name="migration-issues-for-client-side-for-xml"></a>用戶端 FOR XML 的移轉問題  
 由於執行引擎的變更，如果在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]下[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]執行 for XML 查詢，可能會在基表的中繼資料中傳回不同的值。 發生這種情況時，FOR XML 查詢結果的用戶端格式設定會依照用來執行查詢的版本而有不同的輸出。  
  
 如果使用 SQLXML 3.0 在用戶端上對 `xml` 資料類型資料行執行 FOR XML 查詢，則結果中的資料會以完全實體化的字串傳回。 在 SQLXML 4.0 中，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) 是指定為提供者，則資料會傳回為 XML。  
  
  
