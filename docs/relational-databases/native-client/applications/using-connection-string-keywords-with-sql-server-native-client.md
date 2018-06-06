---
title: 搭配 SQL Server Native Client 使用連接字串關鍵字 |Microsoft 文件
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
caps.latest.revision: 81
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c30c279eb6c32d4c602ed8d6f27d91035001e6a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>搭配 SQL Server Native Client 使用連接字串關鍵字
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  某些 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client API 會使用連接字串來指定連接屬性。 連接字串是關鍵字和關聯值的清單，每一個關鍵字都會識別特定的連接屬性。  
  
> **注意：** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 允許模稜兩可，為了維持回溯相容性的連接字串中 （例如，某些關鍵字可能會指定一次以上，而位置為基礎的解析可能會允許衝突的關鍵字或優先順序）。 未來的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本可能不允許模稜兩可的連接字串。 當修改應用程式，以便使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 來移除對於模稜兩可之連接字串的任何相依性時，這就是很好的作法。  
  
 下列章節描述當使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 當做資料提供者時，可以搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和 ActiveX Data Objects (ADO) 使用的關鍵字。  
  
## <a name="odbc-driver-connection-string-keywords"></a>ODBC 驅動程式連接字串關鍵字  
 ODBC 應用程式使用連接字串做為參數[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)和[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)函式。  
  
 ODBC 使用的連接字串具有以下語法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 可以選擇用大括號括住屬性值，這樣是很好的作法。 如此可在屬性值包含非英數字元時避免問題發生。 值中的第一個右大括號應該會結束該值，所以值不能包含右大括號字元。  
  
 下表描述可搭配 ODBC 連接字串使用的關鍵字。  
  
|關鍵字|Description|  
|-------------|-----------------|  
|**Addr**|"Address" 的同義字。|  
|**位址**|執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之伺服器的網路位址。 **位址**通常是伺服器的網路名稱，但可以是其他名稱，例如管道、 IP 位址或 TCP/IP 通訊埠和通訊端位址。<br /><br /> 若您指定 IP 位址，請確定在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員中已啟用 TCP/IP 或具名管道通訊協定。<br /><br /> 值**位址**傳遞給的值的優先順序高於**伺服器**時使用的 ODBC 連接字串中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端。 也請注意，`Address=;`會連線到伺服器中指定**伺服器**關鍵字，而`Address= ;, Address=.;`， `Address=localhost;`，和`Address=(local);`all 導致本機伺服器的連接。<br /><br /> 完整語法**位址**關鍵字如下所示：<br /><br /> [*通訊協定 ***:**]* 位址 *[* *，* * * 連接埠&#124;\pipe\pipename*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** (共用記憶體) 或 **np** (具名管道)。 如需通訊協定的詳細資訊，請參閱[Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md)。<br /><br /> 如果沒有*通訊協定*和**網路**指定關鍵字，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端將使用中指定的通訊協定順序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *連接埠*是連接、 指定的伺服器上的連接埠。 根據預設，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用通訊埠 1433。|  
|**AnsiNPW**|如果為 "yes"，此驅動程式就會使用 ANSI 定義的行為來處理 NULL 比較、字元資料填補、警告和 NULL 串連。 當為 "no" 時，將不會公開 ANSI 定義的行為。 如需有關 ANSI NPW 行為的詳細資訊，請參閱[ISO 選項的作用](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)。|  
|**應用程式**|名稱的應用程式呼叫[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) （選擇性）。 如果指定，這個值會儲存在**master.dbo.sysprocesses**資料行**sys.sysprocesses** ，傳回[sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)和[APP_NAME](../../../t-sql/functions/app-name-transact-sql.md)函式。|  
|**ApplicationIntent**|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。 預設值是**ReadWrite**。  例如：<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> 如需有關[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[SQL Server 原生用戶端支援高可用性、 災害復原](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。|  
|**AttachDBFileName**|可附加資料庫的主要檔案名稱。 包含完整路徑，而且會使用 C 字元字串變數逸出任何 \ 字元：<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> 此資料庫會附加，而且變成連接的預設資料庫。 若要使用**AttachDBFileName**您也必須指定資料庫名稱在[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) DATABASE 參數或 SQL_COPT_CURRENT_CATALOG 連接屬性。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它，它會使用附加的資料庫當做連接的預設值。|  
|**AutoTranslate**|當為 "yes" 時，如果要轉譯用戶端與伺服器之間傳送的 ANSI 字元字串，則會透過 Unicode 來進行轉換，好讓用戶端與伺服器之字碼頁之間的比對擴充字元問題減至最少。<br /><br /> 用戶端 SQL_C_CHAR 資料傳送至[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**， **varchar**，或**文字**變數、 參數或資料行是從字元轉換成 Unicode 使用用戶端的 ANSI 字碼頁 (ACP)，則從 Unicode 字元使用伺服器的 ACP 轉換。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**char**， **varchar**，或**文字**傳送到用戶端的 SQL_C_CHAR 變數的資料是從字元轉換成 Unicode 使用伺服器的 ACP，則從 Unicode 字元使用用戶端的 ACP 轉換。<br /><br /> 這些轉換會由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式在用戶端上執行。 這會要求在伺服器上使用的相同 ANSI 字碼頁 (ACP) 必須也可以在用戶端上使用。<br /><br /> 這些設定對於進行下列傳輸時所發生的轉換沒有作用：<br /><br /> \* Unicode SQL_C_WCHAR 用戶端資料傳送至**char**， **varchar**，或**文字**在伺服器上。<br /><br /> \* **char**， **varchar**，或**文字**伺服器傳送到用戶端上之 Unicode SQL_C_WCHAR 變數的資料。<br /><br /> \* 傳送至 Unicode 的 ANSI SQL_C_CHAR 用戶端資料**nchar**， **nvarchar**，或**ntext**在伺服器上。<br /><br /> \* Unicode **nchar**， **nvarchar**，或**ntext**伺服器傳送到用戶端上之 ANSI SQL_C_CHAR 變數的資料。<br /><br /> 當為 "no" 時，不會執行字元轉譯。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式不會轉譯傳送到用戶端 ANSI 字元 SQL_C_CHAR 資料**char**， **varchar**，或**文字**變數、 參數或在伺服器上的資料行。 上執行任何轉譯**char**， **varchar**，或**文字**從伺服器傳送至用戶端的 SQL_C_CHAR 變數的資料。<br /><br /> 如果用戶端和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用不同的 ACP，可能會將擴充字元解譯錯誤。|  
|**資料庫**|用於連接的預設 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫名稱。 如果**資料庫**未指定，會使用登入所定義的預設資料庫。 ODBC 資料來源中的預設資料庫會覆寫針對此登入所定義的預設資料庫。 資料庫必須是現有的資料庫，除非**AttachDBFileName**同時指定。 如果**AttachDBFileName**同時指定，會附加它所指向的主要檔案，並指定所指定的資料庫名稱**資料庫**。|  
|**驅動程式**|所傳回的驅動程式名稱[SQLDrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的關鍵字值是 "{SQL Server Native Client 11.0}"。 **伺服器**關鍵字是必要項，如果**驅動程式**指定和**DriverCompletion**設定為 SQL_DRIVER_NOPROMPT。<br /><br /> 如需驅動程式名稱的詳細資訊，請參閱[使用 SQL Server Native Client 標頭和程式庫檔案](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md)。|  
|**DSN**|現有 ODBC 使用者或系統資料來源的名稱。 這個關鍵字會覆寫任何可能在中指定的值**伺服器**，**網路**，和**位址**關鍵字。|  
|**Encrypt**|指定當透過網路傳送資料以前，是否應該先加密資料。 可能的值為 "yes" 和 "no"。 預設值為 "no"。|  
|**後援**|這個關鍵字已被取代，而且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會忽略它的設定。|  
|**Failover_Partner**|當無法連接主要伺服器時，所要使用的容錯移轉夥伴伺服器名稱。|  
|**FailoverPartnerSPN**|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。|  
|**FileDSN**|現有 ODBC 檔案資料來源的名稱。|  
|**語言**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言名稱 (選擇性)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可以儲存多種語言的訊息**sysmessages**。 如果連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用多種語言**語言**指定哪些訊息組合可用來連接。|  
|**MARS_Connection**|啟用或停用連接上的 Multiple Active Result Sets (MARS)。 可辨識的值為 "yes" 和 "no"。 預設值是 "no"。|  
|**MultiSubnetFailover**|請務必指定**multiSubnetFailover = Yes**連接到可用性群組接聽程式時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性群組或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]容錯移轉叢集執行個體。 **multiSubnetFailover = Yes**設定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 來提供更快速偵測與連接 （目前） 作用中的伺服器。 可能的值為 [是] 和 [否]。 預設值是**否**。 例如：<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 如需有關[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[SQL Server 原生用戶端支援高可用性、 災害復原](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。|  
|**net**|"Network" 的同義字。|  
|**網路**|有效值為**dbnmpntw** （具名管道） 和**dbmssocn** (TCP/IP)。<br /><br /> 它是指定這兩個值錯誤**網路**關鍵字和通訊協定前置詞上**伺服器**關鍵字。|  
|**PWD**|指定於 UID 參數中之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入帳戶的密碼。 **PWD**不需要指定如果登入具有 NULL 密碼或使用 Windows 驗證 (`Trusted_Connection = yes`)。|  
|**QueryLog_On**|當為 "yes" 時，連接上會啟用長時間執行之查詢資料的記錄。 當為 "no" 時，不會記錄長時間執行的查詢資料。|  
|**QueryLogFile**|用來記錄長時間執行之查詢資料的檔案完整路徑或檔案名稱。|  
|**QueryLogTime**|數字字元字串，可指定用來記錄長時間執行之查詢的臨界值 (以毫秒為單位)。 在指定的時間內未得到回應的任何查詢都會寫入長時間執行的查詢記錄檔中。|  
|**QuotedId**|當為 "yes" 時，連接的 QUOTED_IDENTIFIERS 會設定為 ON，而且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用 ISO 規則，不論 SQL 陳述式中是否使用引號。 當設定為 no 時，連接的 QUOTED_IDENTIFIERS 會設定為 OFF， 然後 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會遵循 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 傳統規則，不論 SQL 陳述式中是否使用引號。 如需詳細資訊，請參閱[ISO 選項的作用](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md)。|  
|**地區**|當設定為 "yes" 時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式將貨幣、日期和時間資料轉換成字元資料時，會使用用戶端設定。 轉換僅限單向；此驅動程式無法辨識非 ODBC 標準格式的日期字串或貨幣值；例如，INSERT 或 UPDATE 陳述式中使用的參數。 當設定為 "no" 時，此驅動程式會使用 ODBC 標準字串來表示轉換成字元資料的貨幣、日期和時間資料。|  
|**SaveFile**|如果連接成功，要用來儲存目前連接之屬性的 ODBC 資料來源檔案名稱。|  
|**Server**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。 此值必須是網路上的伺服器名稱、IP 位址，或是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員別名的名稱。<br /><br /> **位址**關鍵字會覆寫**伺服器**關鍵字。<br /><br /> 您可藉由指定下列其中一個項目，連接到本機伺服器上的預設執行個體：<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> 如需有關 LocalDB 支援的詳細資訊，請參閱[SQL Server 原生用戶端支援 LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)。<br /><br /> 若要指定的具名執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，附加 **\\ ***InstanceName*。<br /><br />如果未不指定任何伺服器，會連接到本機電腦上預設執行個體。<br /><br />如果您指定的 IP 位址，請確定中已啟用 TCP/IP 或具名的管道通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br />完整語法**伺服器**關鍵字如下：<br /> <br /> **Server =**[* 通訊協定***:**]*伺服器*[**，* * * 連接埠*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** (共用記憶體) 或 **np** (具名管道)。<br /><br /> 下列是指定具名管道的範例：<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 此程式碼行指定具名管道通訊協定、本機電腦上的具名管道 (`\\.\pipe`)、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱 (`MSSQL$MYINST01`) 以及具名管道的預設名稱 (`sql/query`)。<br /><br /> 如果沒有*通訊協定*和**網路**指定關鍵字，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端將使用中指定的通訊協定順序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *連接埠*是連接、 指定的伺服器上的連接埠。 根據預設，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用通訊埠 1433。<br /><br /> 傳遞給的值開頭的空格會被忽略**伺服器**時使用的 ODBC 連接字串中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端。|  
|**ServerSPN**|伺服器的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用驅動程式產生的預設 SPN。|  
|**StatsLog_On**|當設定為 "yes" 時，會啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式效能資料的擷取。 當設定為 "no" 時，連接上無法取得 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式效能資料。|  
|**StatsLogFile**|用來記錄 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式效能統計資料之檔案的完整路徑和檔案名稱。|  
|**Trusted_Connection**|當為 "yes" 時，會指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式使用 Windows 驗證模式進行登入驗證。 否則會指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者名稱和密碼進行登入驗證，而且必須指定 UID 和 PWD 密碼。|  
|**TrustServerCertificate**|當搭配**加密**，啟用使用自我簽署的伺服器憑證加密。|  
|**UID**|有效的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入帳戶。 使用 Windows 驗證時不需要指定 UID。|  
|**UseProcForPrepare**|這個關鍵字已被取代，而且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會忽略它的設定。|  
|**WSID**|工作站識別碼。 一般而言，這是應用程式所在之電腦的網路名稱 (選擇性)。 如果指定，這個值會儲存在**master.dbo.sysprocesses**資料行**hostname** ，傳回[sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)和[HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md)函式。|  
  
> **注意：**地區轉換設定適用於貨幣、 數值、 日期和時間資料型別。 此轉換設定只適用於輸出轉換，而且只有當貨幣、數值、日期或時間值轉換為字元字串時，才能看到。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式會針對目前的使用者使用地區設定的登錄設定。 驅動程式不接受目前的執行緒地區設定，如果應用程式會設定它後連線，例如，呼叫**SetThreadLocale**。  
  
 變更資料來源的地區行為可能會導致應用程式失敗。 剖析日期字串並預期日期字串如 ODBC 定義之方式顯示的應用程式，可能會受到變更此值的負面影響。  
  
## <a name="ole-db-provider-connection-string-keywords"></a>OLE DB 提供者連接字串關鍵字  
 OLE DB 應用程式有兩種方法可初始化資料來源物件：  
  
-   **Idbinitialize:: Initialize**  
  
-   **Idatainitialize:: Getdatasource**  
  
 在第一個案例中，提供者字串可用來初始化連接屬性，其方式是在 DBPROPSET_DBINIT 屬性集中設定 DBPROP_INIT_PROVIDERSTRING 屬性。 在第二個案例中，初始化字串可以傳遞至**idatainitialize:: Getdatasource**方法來初始化連接屬性。 這兩個方法都會初始化相同的 OLE DB 連接屬性，但是會使用不同的關鍵字集合。 所使用的關鍵字集**idatainitialize:: Getdatasource**最少是初始化屬性群組內的屬性描述。  
  
 如果任何提供者字串設定所包含的對應 OLE DB 屬性設定為預設值或明確設定為某個值，OLE DB 屬性值將在提供者字串中覆寫此設定。  
  
 在提供者字串中透過 DBPROP_INIT_PROVIDERSTRING 值所設定的布林屬性是使用 "yes" 和 "no" 的值所設定。 在初始化字串中使用設定的布林屬性**idatainitialize:: Getdatasource**都使用值"true"和"false"設定。  
  
 使用應用程式**idatainitialize:: Getdatasource**也可以使用所用的關鍵字**idbinitialize:: Initialize**但只適用於沒有預設值的屬性。 如果應用程式同時使用**idatainitialize:: Getdatasource**關鍵字和**idbinitialize:: Initialize**在初始化字串關鍵字**idatainitialize:: Getdatasource**使用關鍵字設定。 強烈建議應用程式不使用**idbinitialize:: Initialize**中的關鍵字**您**連接字串，因為這種行為可能不會保留在未來的版本。  
  
> [!NOTE]  
>  連接字串傳遞**idatainitialize:: Getdatasource**轉換成屬性並加以套用透過**idbproperties:: Setproperties**。 如果元件服務中找到屬性描述中的**idbproperties:: Getpropertyinfo**，將會當做獨立屬性來套用這個屬性。 否則，它將會透過 DBPROP_PROVIDERSTRING 屬性來套用。 例如，如果您指定連接字串**資料來源 = server1;Server = server2**，**資料來源**會設定為屬性，但**伺服器**將會進入提供者字串。  
  
 如果您指定相同提供者特有之屬性的多個執行個體，將會使用第一個屬性的值。  
  
 使用 OLE DB 應用程式使用 dbprop_init_providerstring，其使用的連接字串**idbinitialize:: Initialize**具有下列語法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 可以選擇用大括號括住屬性值，這樣是很好的作法。 如此可在屬性值包含非英數字元時避免問題發生。 值中的第一個右大括號應該會結束該值，所以值不能包含右大括號字元。  
  
 連接字串關鍵字 = 符號後面的空格字元應該解譯為常值，即使該值括在引號內也是如此。  
  
 下表描述可搭配 DBPROP_INIT_PROVIDERSTRING 使用的關鍵字。  
  
|關鍵字|初始化屬性|Description|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|"Address" 的同義字。|  
|**位址**|SSPROP_INIT_NETWORKADDRESS|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的網路位址。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**位址**ODBC 關鍵字，本主題稍後的。|  
|**應用程式**|SSPROP_INIT_APPNAME|識別應用程式的字串。|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。<br /><br /> 預設值是**ReadWrite**。 如需有關[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[SQL Server 原生用戶端支援高可用性、 災害復原](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|可附加資料庫的主要檔案名稱，包括完整路徑名稱。 若要使用**AttachDBFileName**，您也必須使用提供者字串 Database 關鍵字指定資料庫名稱。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它 (它會使用附加的資料庫當做連接的預設值)。|  
|**自動轉譯**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" 的同義字。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|設定 OEM/ANSI 字元轉譯。 可辨識的值為 "yes" 和 "no"。|  
|**資料庫**|DBPROP_INIT_CATALOG|資料庫名稱。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的資料類型處理模式。 認得的值為 "0" (代表提供者資料類型) 和 "80" (代表 SQL Server 2000 資料類型)。|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|指定當透過網路傳送資料以前，是否應該先加密資料。 可能的值為 "yes" 和 "no"。 預設值為 "no"。|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|用於資料庫鏡像的容錯移轉伺服器名稱。|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|**語言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言。|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|當伺服器為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本時，啟用或停用連接上的 Multiple Active Result Sets (MARS)。 可能的值為 "yes" 和 "no"。 預設值為 "no"。|  
|**net**|SSPROP_INIT_NETWORKLIBRARY|"Network" 的同義字。|  
|**網路**|SSPROP_INIT_NETWORKLIBRARY|用來建立組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之連接的網路程式庫。|  
|**網路程式庫**|SSPROP_INIT_NETWORKLIBRARY|"Network" 的同義字。|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|網路封包大小。 預設值為 4096。|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受的值為 "yes" 和 "no" 字串。 當為 "no" 時，不允許使用資料來源物件來保存敏感性驗證資訊。|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入密碼。|  
|**Server**|DBPROP_INIT_DATASOURCE|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。<br /><br /> 如果沒有指定，就會連接至本機電腦上的預設執行個體。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**伺服器**ODBC 關鍵字，本主題中的。|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|伺服器的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|**逾時**|DBPROP_INIT_TIMEOUT|等候資料來源初始化完成的時間量 (以秒為單位)。|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|當為 "yes" 時，會指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者使用 Windows 驗證模式進行登入驗證。 否則會指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者名稱和密碼進行登入驗證，而且必須指定 UID 和 PWD 密碼。|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受的值為 "yes" 和 "no" 字串。 預設值為 "no"，這表示將會驗證伺服器憑證。|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入名稱。|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|這個關鍵字已被取代，而且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會忽略它的設定。|  
|**WSID**|SSPROP_INIT_WSID|工作站識別碼。|  
  
 使用 OLE DB 應用程式使用的連接字串**idatainitialize:: Getdatasource**具有下列語法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 屬性的使用必須符合其範圍內所允許的語法。  例如， **WSID**使用大括號 (**{}**) 引號字元和**應用程式名稱**會使用單引號 (**'**) 或double (**"**) 引號字元。 只有字串屬性可以加上引號。 嘗試將整數或列舉屬性加上引號將會產生「連接字串沒有符合 OLE DB 規格」錯誤。  
  
 您可以選擇用單引號或雙引號括住屬性值，這樣是很好的作法。 如此可在值包含非英數字元時避免問題發生。 使用的引號字元也可出現在值當中，但前提必須是雙引號字元。  
  
 連接字串關鍵字 = 符號後面的空格字元應該解譯為常值，即使該值括在引號內也是如此。  
  
 如果連接字串具有下表所列的多個屬性，將會使用最後一個屬性的值。  
  
 下表描述可搭配使用的關鍵字**idatainitialize:: Getdatasource**:  
  
|關鍵字|初始化屬性|Description|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|識別應用程式的字串。|  
|**應用程式意圖**|SSPROP_INIT_APPLICATIONINTENT|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。<br /><br /> 預設值是**ReadWrite**。 如需有關[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[SQL Server 原生用戶端支援高可用性、 災害復原](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。|  
|**自動轉譯**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" 的同義字。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|設定 OEM/ANSI 字元轉譯。 認得的值為 "true" 和 "false"。|  
|**連接逾時**|DBPROP_INIT_TIMEOUT|等候資料來源初始化完成的時間量 (以秒為單位)。|  
|**目前的語言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言名稱。|  
|**資料來源**|DBPROP_INIT_DATASOURCE|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。<br /><br /> 如果沒有指定，就會連接至本機電腦上的預設執行個體。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**伺服器**ODBC 關鍵字，本主題稍後的。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的資料類型處理模式。 認得的值為 "0" (代表提供者資料類型) 和 "80" (代表 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 資料類型)。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用於資料庫鏡像的容錯移轉伺服器名稱。|  
|**容錯移轉夥伴 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|**初始目錄**|DBPROP_INIT_CATALOG|資料庫名稱。|  
|**初始檔案名稱**|SSPROP_INIT_FILENAME|可附加資料庫的主要檔案名稱，包括完整路徑名稱。 若要使用**AttachDBFileName**，您也必須使用提供者字串 DATABASE 關鍵字指定資料庫名稱。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它 (它會使用附加的資料庫當做連接的預設值)。|  
|**整合式安全性**|DBPROP_AUTH_INTEGRATED|接受 "SSPI" 值進行 Windows 驗證。|  
|**MARS 連接**|SSPROP_INIT_MARSCONNECTION|啟用或停用連接上的 Multiple Active Result Sets (MARS)。 認得的值為 "true" 和 "false"。 預設值為 "false"。|  
|**網路位址**|SSPROP_INIT_NETWORKADDRESS|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的網路位址。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**位址**ODBC 關鍵字，本主題稍後的。|  
|**網路程式庫**|SSPROP_INIT_NETWORKLIBRARY|用來建立組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之連接的網路程式庫。|  
|**封包大小**|SSPROP_INIT_PACKETSIZE|網路封包大小。 預設值為 4096。|  
|**密碼**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入密碼。|  
|**保存安全性資訊**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受的值為 "true" 和 "false" 字串。 當為 "false" 時，不允許使用資料來源物件來保存敏感性驗證資訊。|  
|**提供者**||如果是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，這應該是 "SQLNCLI11"。|  
|**伺服器的 SPN**|SSPROP_INIT_SERVERSPN|伺服器的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|**信任伺服器憑證**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受的值為 "true" 和 "false" 字串。 預設值為 "false"，這表示將會驗證伺服器憑證。|  
|**使用加密資料**|SSPROP_INIT_ENCRYPT|指定當透過網路傳送資料以前，是否應該先加密資料。 可能的值為 "true" 和 "false"。 預設值為 "false"。|  
|**使用者識別碼**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入名稱。|  
|**工作站識別碼**|SSPROP_INIT_WSID|工作站識別碼。|  
  
 **請注意**在連接字串中，"Old Password"屬性會設定 SSPROP_AUTH_OLD_PASSWORD，這是不是透過提供者字串屬性目前的 （可能已過期） 密碼。  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ActiveX Data Objects (ADO) 連接字串關鍵字  
 ADO 應用程式會設定**ConnectionString**屬性**ADODBConnection**物件或為參數，以提供連接字串**開啟**方法**ADODBConnection**物件。  
  
 ADO 應用程式也可以使用 OLE DB 所用的關鍵字**idbinitialize:: Initialize**方法，但只適用於沒有預設值的屬性。 如果應用程式使用 ADO 關鍵字和**idbinitialize:: Initialize**會使用 ADO 關鍵字設定初始化字串中的關鍵字。 強烈建議您只讓應用程式使用 ADO 連接字串關鍵字。  
  
 ADO 使用的連接字串具有以下語法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 可以選擇用雙引號括住屬性值，這樣是很好的作法。 如此可在值包含非英數字元時避免問題發生。 屬性值不能包含雙引號。  
  
 下表描述可搭配 ADO 連接字串使用的關鍵字：  
  
|關鍵字|初始化屬性|Description|  
|-------------|-----------------------------|-----------------|  
|**應用程式意圖**|SSPROP_INIT_APPLICATIONINTENT|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。<br /><br /> 預設值是**ReadWrite**。 如需有關[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[SQL Server 原生用戶端支援高可用性、 災害復原](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。|  
|**Application Name**|SSPROP_INIT_APPNAME|識別應用程式的字串。|  
|**自動轉譯**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" 的同義字。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|設定 OEM/ANSI 字元轉譯。 認得的值為 "true" 和 "false"。|  
|**連接逾時**|DBPROP_INIT_TIMEOUT|等候資料來源初始化完成的時間量 (以秒為單位)。|  
|**目前的語言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言名稱。|  
|**資料來源**|DBPROP_INIT_DATASOURCE|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。<br /><br /> 如果沒有指定，就會連接至本機電腦上的預設執行個體。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**伺服器**ODBC 關鍵字，本主題中的。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定即將使用之資料類型處理的模式。 認得的值為 "0" (代表提供者資料類型) 和 "80" (代表 SQL Server 2000 資料類型)。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用於資料庫鏡像的容錯移轉伺服器名稱。|  
|**容錯移轉夥伴 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|**初始目錄**|DBPROP_INIT_CATALOG|資料庫名稱。|  
|**初始檔案名稱**|SSPROP_INIT_FILENAME|可附加資料庫的主要檔案名稱，包括完整路徑名稱。 若要使用**AttachDBFileName**，您也必須使用提供者字串 DATABASE 關鍵字指定資料庫名稱。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它 (它會使用附加的資料庫當做連接的預設值)。|  
|**整合式安全性**|DBPROP_AUTH_INTEGRATED|接受 "SSPI" 值進行 Windows 驗證。|  
|**MARS 連接**|SSPROP_INIT_MARSCONNECTION|當伺服器為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本時，啟用或停用連接上的 Multiple Active Result Sets (MARS)。 認得的值為 "true" 和 "false"。預設值是 "false"。|  
|**網路位址**|SSPROP_INIT_NETWORKADDRESS|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的網路位址。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**位址**ODBC 關鍵字，本主題中的。|  
|**網路程式庫**|SSPROP_INIT_NETWORKLIBRARY|用來建立組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之連接的網路程式庫。|  
|**封包大小**|SSPROP_INIT_PACKETSIZE|網路封包大小。 預設值為 4096。|  
|**密碼**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入密碼。|  
|**保存安全性資訊**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受的值為 "true" 和 "false" 字串。 如果為 "false"，表示不允許資料來源物件保存機密的驗證資訊。|  
|**提供者**||如果是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，這應該是 "SQLNCLI11"。|  
|**伺服器的 SPN**|SSPROP_INIT_SERVERSPN|伺服器的 SPN。 預設值為空字串。 空字串會讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|**信任伺服器憑證**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受的值為 "true" 和 "false" 字串。 預設值為 "false"，這表示將會驗證伺服器憑證。|  
|**使用加密資料**|SSPROP_INIT_ENCRYPT|指定當透過網路傳送資料以前，是否應該先加密資料。 可能的值為 "true" 和 "false"。 預設值為 "false"。|  
|**使用者識別碼**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入名稱。|  
|**工作站識別碼**|SSPROP_INIT_WSID|工作站識別碼。|  
  
 **請注意**在連接字串中，"Old Password"屬性會設定 SSPROP_AUTH_OLD_PASSWORD，這是不是透過提供者字串屬性目前的 （可能已過期） 密碼。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建立應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
