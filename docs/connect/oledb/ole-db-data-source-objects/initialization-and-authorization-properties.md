---
title: 初始化和授權屬性 |Microsoft 文件
description: 初始化和授權屬性
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- authorization [OLE DB]
- properties [OLE DB]
- OLE DB Driver for SQL Server, initialization properties
- OLE DB Driver for SQL Server, authorization properties
- initialization properties [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6be9ab05f9f7a5c669e62f92c238be3d06dbf44d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="initialization-and-authorization-properties"></a>初始化和授權屬性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server OLE DB 驅動程式會解譯 OLE DB 初始化和授權屬性，如下所示：  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_AUTH_CACHE_AUTHINFO|SQL Server OLE DB 驅動程式不會快取驗證資訊。<br /><br /> SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_ENCRYPT_PASSWORD|SQL Server OLE DB 驅動程式會使用標準[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安全性機制來隱藏密碼。<br /><br /> SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_INTEGRATED|如果 DBPROP_AUTH_INTEGRATED 設定為 NULL 指標、 null 字串或 'SSPI' VT_BSTR 值，SQL Server OLE DB 驅動程式會使用 Windows 驗證模式來授權使用者存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]DBPROP_INIT_DATASOURCE 和 DBPROP 所指定的資料庫_INIT_CATALOG 屬性。<br /><br /> 如果設定為 VT_EMPTY (預設值)，則會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入和密碼是在 DBPROP_AUTH_USERID 和 DBPROP_AUTH_PASSWORD 屬性中指定的。|  
|DBPROP_AUTH_MASK_PASSWORD|SQL Server OLE DB 驅動程式會使用標準[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安全性機制來隱藏密碼。<br /><br /> SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_PASSWORD|指派給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入的密碼。 選取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證來授權對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的存取時，會使用此屬性。|  
|DBPROP_AUTH_PERSIST_ENCRYPTED|SQL Server OLE DB 驅動程式不會加密保存時的驗證資訊。<br /><br /> SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|SQL Server OLE DB 驅動程式保存驗證值，如果要求若要這樣做，包括密碼的映像。 不提供任何加密。|  
|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入。 選取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證來授權對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的存取時，會使用此屬性。|  
|DBPROP_INIT_ASYNCH|SQL Server OLE DB 驅動程式支援非同步初始化。<br /><br /> 設定 DBPROPVAL_ASYNCH_INITIALIZE 位元前，於 DBPROP_INIT_ASYNCH 屬性會導致**idbinitialize:: Initialize**變成非封鎖的呼叫。 如需詳細資訊，請參閱[執行非同步作業](../../oledb/features/performing-asynchronous-operations.md)。|  
|DBPROP_INIT_CATALOG|所連接之現有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的名稱。|  
|DBPROP_INIT_DATASOURCE|執行的執行個體的伺服器網路名稱[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如果有多個執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]才能連接到特定的執行個體的電腦上，執行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]DBPROP_INIT_DATASOURCE 值會指定為 *\\\ServerName\InstanceName*。 逸出序列\\\ 用於反斜線本身。|  
|DBPROP_INIT_GENERALTIMEOUT|表示要求 (而非資料來源初始化和命令執行) 逾時前的秒數。值為 0 表示無限逾時。透過網路連線或者在分散或交易情況下工作的提供者可以支援此屬性，在出現長時間執行的要求時，通知編列的元件逾時。 資料來源初始化和命令執行的逾時仍然個別受到 DBPROP_INIT_TIMEOUT 和 DBPROP_COMMANDTIMEOUT 的管理。<br /><br /> DBPROP_INIT_GENERALTIMEOUT 是唯讀的而且如果嘗試將它設定*dwstatus*就會傳回錯誤的使用者。|  
|DBPROP_INIT_HWND|來自呼叫應用程式的 Windows 控制代碼。 在允許提示初始化屬性時顯示的初始化對話方塊需要有效的視窗控制代碼。|  
|DBPROP_INIT_IMPERSONATION_LEVEL|SQL Server OLE DB 驅動程式不支援模擬層級調整。<br /><br /> SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_LCID|SQL Server OLE DB 驅動程式會驗證地區設定識別碼，並會傳回錯誤，或未安裝在用戶端上不支援的地區設定識別碼。|  
|DBPROP_INIT_LOCATION|SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_MODE|SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_PROMPT|SQL Server OLE DB 驅動程式支援資料來源初始化的所有提示模式。 SQL Server OLE DB 驅動程式會使用 DBPROMPT_NOPROMPT 做為其預設設定的屬性。|  
|DBPROP_INIT_PROTECTION_LEVEL|SQL Server OLE DB 驅動程式不支援保護層級的執行個體的連接上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。<br /><br /> SQL Server OLE DB 驅動程式會在嘗試設定屬性值，傳回 DB_S_ERRORSOCCURRED。 *DwStatus* DBPROP 結構的成員表示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_PROVIDERSTRING|請參閱本主題稍後的 SQL Server 字串，OLE DB 驅動程式。|  
|DBPROP_INIT_TIMEOUT|SQL Server OLE DB 驅動程式會將錯誤傳回初始化如果連接執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]不能指定的秒數內建立。|  
  
 在提供者特有的屬性集 DBPROPSET_SQLSERVERDBINIT 中，SQL Server OLE DB 驅動程式會定義這些額外的初始化屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_AUTH_OLD_PASSWORD|類型：VT_BSTR<br /><br /> R/W：寫入<br /><br /> 預設值：VT_EMPTY<br /><br /> 描述：目前或過期的密碼。 如需詳細資訊，請參閱[變更密碼以程式設計方式](../../oledb/features/changing-passwords-programmatically.md)。|  
|SSPROP_INIT_APPNAME|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：用戶端應用程式名稱。|  
|SSPROP_INIT_AUTOTRANSLATE|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述：OEM/ANSI 字元轉換。<br /><br /> VARIANT_TRUE: SQL Server OLE DB 驅動程式會轉譯傳送用戶端與伺服器之間透過 Unicode 進行轉換中的字碼頁，在用戶端與伺服器之間的比對擴充字元問題降到最低的 ANSI 字元字串：<br /><br /> 用戶端 DBTYPE_STR 資料傳送至執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**， **varchar**，或**文字**從字元轉換成 Unicode 使用用戶端的 ANSI 字碼頁 (ACP)，然後從 Unicode 字元使用伺服器的 ACP 轉換變數、 參數或資料行。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**char**， **varchar**，或**文字**傳送到用戶端 DBTYPE_STR 變數的資料是從字元轉換成 Unicode 使用伺服器的 ACP，然後再轉換成字元使用用戶端的 ACP Unicode 從。<br /><br /> 適用於 SQL Server 這些轉換會在用戶端上執行的 OLE DB 驅動程式。 但是在伺服器上使用的相同 ACP 必須也可以在用戶端上使用。<br /><br /> 這些設定對於進行下列傳輸時所發生的轉換沒有作用：<br /><br /> Unicode DBTYPE_WSTR 用戶端資料傳送至**char**， **varchar**，或**文字**在伺服器上。<br /><br /> **char**， **varchar**，或**文字**伺服器傳送到用戶端上之 Unicode DBTYPE_WSTR 變數的資料。<br /><br /> 傳送至 Unicode 的 ANSI DBTYPE_STR 用戶端資料**nchar**， **nvarchar**，或**ntext**在伺服器上。<br /><br /> Unicode **char**， **varchar**，或**文字**伺服器傳送到用戶端上之 ANSI DBTYPE_STR 變數的資料。<br /><br /> VARIANT_FALSE: SQL Server OLE DB 驅動程式不會執行字元轉譯。<br /><br /> SQL Server OLE DB 驅動程式不會轉譯傳送到用戶端 ANSI 字元 DBTYPE_STR 資料**char**， **varchar**，或**文字**變數、 參數或資料行伺服器。 上執行任何轉譯**char**， **varchar**，或**文字**從伺服器傳送至用戶端 DBTYPE_STR 變數的資料。<br /><br /> 如果用戶端和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體使用不同的 ACP，可能會將擴充字元解譯錯誤。|  
|SSPROP_INIT_CURRENTLANGUAGE|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言名稱。 識別系統訊息選取與格式所使用的語言。 此語言必須安裝在執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的電腦上，否則資料初始化會失敗。|  
|SSPROP_INIT_DATATYPECOMPATIBILITY|類型：VT_UI2<br /><br /> R/W：讀取/寫入<br /><br /> 預設值： 0<br /><br /> 描述：允許 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 ActiveX Data Object (ADO) 應用程式之間的資料類型相容性。 如果使用預設值 0，資料類型處理會預設為提供者所使用的資料類型。 如果使用值 80，資料類型處理僅會使用 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 資料類型。 如需詳細資訊，請參閱[使用 ADO 與 OLE DB 驅動程式的 SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。|  
|SSPROP_INIT_ENCRYPT|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：若要加密通過網路的資料，SSPROP_INIT_ENCRYPT 屬性會設定為 VARIANT_TRUE。<br /><br /> 如果 [啟用通訊協定加密] 開啟，不管 SSPROP_INIT_ENCRYPT 的設定為何，永遠會進行加密。 如果關閉此設定，而且 SSPROP_INIT_ENCRYPT 設定為 VARIANT_TRUE，則會進行加密。<br /><br /> 如果關閉 [啟用通訊協定加密]，而且 SSPROP_INIT_ENCRYPT 設定為 VARIANT_FALSE，則不會進行加密。|  
|SSPROP_INIT_FAILOVERPARTNER|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：指定要進行資料庫鏡像之容錯移轉夥伴的名稱。 這是初始化屬性，而且僅能在初始化之前設定。 初始化之後，它會傳回容錯移轉夥伴，如果有的話，則會由主要伺服器傳回。<br /><br /> 這可讓智慧型應用程式快取最近決定的備份伺服器，但是此類應用程式應該會注意到此資訊只會在第一次建立 (如果緩衝，則重設) 連接時更新，而且在長期連接後會變成過期。<br /><br /> 建立連接後，應用程式可以查詢此屬性來判斷容錯移轉夥伴的識別。 如果主要伺服器沒有容錯移轉夥伴，此屬性將會傳回空字串。 如需詳細資訊，請參閱[Using Database Mirroring](../../oledb/features/using-database-mirroring.md)。|  
|SSPROP_INIT_FILENAME|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：指定可附加資料庫的主要檔案名稱。 此資料庫會附加，而且變成連接的預設資料庫。 若要使用 SSPROP_INIT_FILENAME，您必須將資料庫的名稱指定為初始化屬性 DBPROP_INIT_CATALOG 的值。 如果資料庫名稱不存在，則會尋找在 SSPROP_INIT_FILENAME 中指定的主要檔案名稱，並以 DBPROP_INIT_CATALOG 中指定的名稱附加該資料庫。 如果該資料庫先前已附加，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它。|  
|SSPROP_INIT_MARSCONNECTION|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：指定是否要針對連接啟用 Multiple Active Result Sets (MARS)。 在連接到資料庫之前，必須將此選項設定為 True。 如需詳細資訊，請參閱[使用 Multiple Active Result Set &#40;MARS &#41;](../../oledb/features/using-multiple-active-result-sets-mars.md).|  
|SSPROP_INIT_NETWORKADDRESS|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：DBPROP_INIT_DATASOURCE 屬性所指定的執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之伺服器的網路位址。|  
|SSPROP_INIT_NETWORKLIBRARY|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體進行通訊所使用之網路程式庫 (DLL) 的名稱。 名稱不得包含路徑或 .dll 副檔名。<br /><br /> 預設值可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端組態公用程式自訂。<br /><br /> 注意： 只有 TCP 和具名管道支援這個屬性。 如果您搭配前置詞使用此屬性，結尾有雙前置詞時，會導致錯誤，因為此屬性用來在內部產生前置詞。|  
|SSPROP_INIT_PACKETSIZE|類型：VT_I4<br /><br /> R/W：讀取/寫入<br /><br /> 描述：網路封包大小 (以位元組為單位)。 封包大小屬性值必須介於 512 和 32,767 之間。 預設 OLE DB 驅動程式的 SQL Server 網路封包大小為 4096。|  
|SSPROP_INIT_TAGCOLUMNCOLLATION|類型：BOOL<br /><br /> R/W：寫入<br /><br /> 預設值：FALSE<br /><br /> 描述：使用伺服器端資料指標時，這會在資料庫更新期間使用。 此屬性會使用從伺服器 (而非用戶端的字碼頁) 取得的定序資訊標記資料。 目前只有分散式查詢處理使用此屬性，因為它知道目的地資料的定序，而且會正確轉換該定序。|  
|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|類型：VT_BOOL<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：用於啟用或停用伺服器憑證驗證。 此屬性是讀取/寫入的，但是在建立連接後嘗試設定該屬性將會導致錯誤。<br /><br /> 如果將用戶端設定為需要憑證驗證，則會忽略此屬性。 不過，即使沒有將用戶端設定為需要加密，而且在用戶端上沒有提供任何憑證，應用程式還是可以將該屬性與 SSPROP_INIT_ENCRYPT 一起使用來確保伺服器的連接經過加密。<br /><br /> 用戶端應用程式可以在開啟連接之後查詢此屬性，以便判斷使用中的實際加密和驗證設定。<br /><br /> 注意： 使用加密沒有憑證驗證會提供部分保護以對抗封包探測，但無法防止攔截的攻擊。 它只會允許加密傳送到伺服器的登入和資料，而不會驗證伺服器憑證。<br /><br /> 如需詳細資訊，請參閱[使用加密而不需驗證](../../oledb/features/using-encryption-without-validation.md)。|  
|SSPROP_INIT_USEPROCFORPREP|類型：VT_I4<br /><br /> R/W：讀取/寫入<br /><br /> 預設值：SSPROPVAL_USEPROCFORPREP_ON<br /><br /> 描述：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預存程序用途。 定義使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]暫存預存程序來支援**m**介面。 只有在連接到 SQL Server 6.5 時，此屬性才有意義。 更新的版本會忽略此屬性。<br /><br /> SSPROPVAL_USEPROCFORPREP_OFF：準備命令時，不會建立暫存預存程序。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON：準備命令時，會建立暫存預存程序。 釋出工作階段時，會卸除暫存預存程序。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON_DROP：準備命令時，會建立暫存預存程序。 與已取消準備命令時，會卸除程序**icommandprepare:: Unprepare**，當新的命令指定的命令物件與**icommandtext:: Setcommandtext**，或釋放命令的所有應用程式參考。|  
|SSPROP_INIT_WSID|類型：VT_BSTR<br /><br /> R/W：讀取/寫入<br /><br /> 描述：識別工作站的字串。|  
  
 在提供者特有的屬性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，SQL Server OLE DB 驅動程式會定義額外的屬性。請參閱[資料來源資訊屬性](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)如需詳細資訊。  
  
## <a name="the-ole-db-driver-for-sql-server-string"></a>SQL Server 字串 OLE DB 驅動程式  
 SQL Server OLE DB 驅動程式可辨識在提供者字串屬性值中類似 ODBC 的語法。 建立 OLE DB 資料來源的連接時，提供者字串屬性會當做 OLE DB 初始化屬性 DBPROP_INIT_PROVIDERSTRING 的值提供。 此屬性會將實作連接所需的 OLE DB 提供者專屬連接資料指定給 OLE DB 資料來源。 在字串內，這些元素會使用分號分隔。 字串中的最終元素必須以分號結束。 每個元素都由一個關鍵字、一個等號字元，以及初始化時傳遞的值所組成。 例如：  
  
```  
Server=MyServer;UID=MyUserName;  
```  
  
 使用 OLE DB 驅動程式的 SQL Server，取用者從不需要使用提供者字串屬性。 取用者可以將透過 OLE DB 或 OLE DB 驅動程式的 SQL Server 特有的初始化屬性反映提供者字串中的任何初始化屬性。  
  
 如需 SQL Server OLE DB 驅動程式提供的關鍵字的清單，請參閱[搭配 OLE DB 驅動程式的 SQL Server 中使用連接字串關鍵字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料來源物件 &#40; OLE DB &#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
