---
title: 連線選項
description: 此主題列出了 SQLSRV 驅動程式中 sqlsrv_connect 關聯陣列中允許的選項，或資料來源名稱 PDO_SQLSRV 驅動程式中允許的關鍵字。
ms.custom: ''
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 98f6899c1bfc7652c4a2facee95cf5fd62e4e521
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632958"
---
# <a name="connection-options"></a>連線選項
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題列出關聯陣列中允許的選項 (在 SQLSRV 驅動程式中使用 [sqlsrv_connect](sqlsrv-connect.md) 時) 或資料來源名稱 (dsn) 中允許的關鍵字 (在 PDO_SQLSRV 驅動程式中使用 [PDO::__construct](pdo-construct.md) 時)。  

## <a name="table-of-connection-options"></a>連線選項表

|Key|值|描述|預設|  
|-------|---------|---------------|-----------|  
|AccessToken|String|從 OAuth JSON 回應中擷取之 Azure AD 存取權杖的位元組字串。<br /><br />連接字串不能包含使用者識別碼、密碼或 `Authentication` 關鍵字。 如需詳細資訊，請參閱[使用 Azure Active Directory 驗證進行連線](azure-active-directory.md)|未設定。|
|APP|String|指定在追蹤中使用的應用程式名稱。|未設定。|  
|ApplicationIntent|String|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為 **ReadOnly** 和 **ReadWrite**。<br /><br />如需適用於 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 之 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支援的詳細資訊，請參閱[高可用性與災害復原的支援](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|讀寫|
|AttachDBFileName|String|指定伺服器所應附加的資料庫檔案。|未設定。|
|驗證|下列其中一個字串：<br /><br />**SqlPassword**<br /><br />**ActiveDirectoryPassword**<br /><br />**ActiveDirectoryMsi**|指定驗證模式。<br /><br />如需詳細資訊，請參閱[使用 Azure Active Directory 驗證進行連線](azure-active-directory.md)|未設定。|
|CharacterSet<br /><br />(PDO_SQLSRV 驅動程式不支援)|String|指定用來將資料傳送至伺服器的字元集。<br /><br />可能的值為 SQLSRV_ENC_CHAR 和 UTF-8。 如需詳細資訊，請參閱[如何：使用內建的 UTF-8 支援傳送及擷取 UTF-8 資料](how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)。|SQLSRV_ENC_CHAR|  
|ColumnEncryption|下列其中一個字串：<br /><br />**已啟用**<br /><br />**Disabled**<br /><br />針對證明記憶體保護區識別證明通訊協定和 URL 的字串|指定是否啟用 Always Encrypted 功能。 如果已指定證明通訊協定和 URL，具有安全記憶體保護區的 Always Encrypted 便會啟用，前提是已滿足[這裡](always-encrypted-secure-enclaves.md)所述的其他需求。|已停用|  
|ConnectionPooling|1 或 **true** 表示開啟連接共用。<br /><br />0 或 **false** 表示關閉連接共用。|指定要從連接集區指派連接 (1 或 **true**)，還是不要指派 (0 或 **false**)。<sup>1</sup>|**true** (1)|  
|ConnectRetryCount|介於 0 和 255 (含) 之間的整數|在放棄之前，重新建立已中斷連線的嘗試次數上限。 根據預設，系統會在連線中斷時嘗試重新建立一次。 值為 0 表示不會嘗試重新連線。|1|  
|ConnectRetryInterval|介於 1 和 60 (含) 之間的整數|重新建立連線嘗試的間隔時間 (以秒為單位)。 應用程式會在偵測到連線中斷時立即嘗試重新連線，然後等候 `ConnectRetryInterval` 秒後再試一次。 如果 `ConnectRetryCount` 等於 0，便會忽略此關鍵字。|1|  
|資料庫|String|指定要建立的連接使用中的資料庫名稱<sup>2</sup>。|使用登入的預設資料庫。|  
|DecimalPlaces<br /><br />(PDO_SQLSRV 驅動程式不支援)|介於 0 和 4 (含) 之間的整數|指定將擷取的貨幣值格式化時的小數位數。<br /><br />此選項只有當 `FormatDecimals` 為 true 時才能運作。 將忽略任何大於 4 的負整數或值。|預設精確度和小數位數|
|驅動程式|String|指定用來與 SQL Server 通訊的 Microsoft ODBC 驅動程式。<br /><br />可能的值包括：<br />ODBC Driver 17 for SQL Server<br />ODBC Driver 13 for SQL Server<br />ODBC Driver 11 for SQL Server (僅限 Windows)。|未指定 Driver 關鍵字時，Microsoft Drivers for PHP for SQL Server 會嘗試在系統中尋找支援的 Microsoft ODBC 驅動程式，並從最新版本的 ODBC 開始，依此類推。| 
|Encrypt|1 或 **true** 表示開啟加密。<br /><br />0 或 **false** 表示關閉加密。|指定要加密與 SQL Server 的通訊 (1 或 **true**)，還是不要加密 (0 或 **false**)<sup>3</sup>。|**false** (0)|  
|Failover_Partner|String|指定在主要伺服器無法使用時所要使用的伺服器和資料庫鏡像執行個體 (如果已啟用和設定)。<br /><br />搭配 `MultiSubnetFailover` 使用 `Failover_Partner` 具有一些限制。 如需詳細資訊，請參閱[對於高可用性、災害復原的支援](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。<br /><br />在 Linux 或 macOS 上不支援此選項，因為 Linux 或 macOS 上的 ODBC 驅動程式不支援資料庫鏡像。 請改為使用 Always On 可用性群組，並設定 `MultiSubnetFailover` 與 `TransparentNetworkIPResolution` 選項。|未設定。|
|FormatDecimals<br /><br />(PDO_SQLSRV 驅動程式不支援)|1 或 **true** 以格式化已擷取的十進位字串。<br /><br />0 或 **false** 以使用預設的十進位格式化行為。|指定是否要在適當時於十進位字串中新增前置零，並啟用 `DecimalPlaces` 選項來將貨幣類型格式化。 如果保留 False，則使用傳回精確的有效位數，並針對小於 1 的值省略前置零的預設行為。<br /><br />如需詳細資訊，請參閱[將十進位字串及貨幣值格式化](formatting-decimals-sqlsrv-driver.md)。|**false** (0)|
|KeyStoreAuthentication|**KeyVaultPassword**<br /><br />**KeyVaultClientSecret**|存取 Azure Key Vault 的驗證方法。 控制要搭配 `KeyStorePrincipalId` 和 `KeyStoreSecret` 使用哪種認證。 如需詳細資訊，請參閱[使用 Azure Key Vault](using-always-encrypted-php-drivers.md#using-azure-key-vault)。|未設定。|
|KeyStorePrincipalId|String|嘗試存取 Azure Key Vault 之帳戶的識別碼。 <br /><br />如果 `KeyStoreAuthentication` 是 **KeyVaultPassword**，這必須是 Azure Active Directory 使用者名稱。 <br /><br />如果 `KeyStoreAuthentication` 是 **KeyVaultClientSecret**，這必須是應用程式用戶端識別碼。|未設定。|
|KeyStoreSecret|String|嘗試存取 Azure Key Vault 之帳戶的認證祕密。 <br /><br />如果 `KeyStoreAuthentication` 是 **KeyVaultPassword**，這必須是 Azure Active Directory 密碼。 <br /><br />如果 `KeyStoreAuthentication` 是 **KeyVaultClientSecret**，這必須是應用程式用戶端祕密。|未設定。|
|Language|String|指定由伺服器傳回的訊息語言。 可用的語言已列於 `sys.syslanguages` 資料表中。 <br /><br />此選項並不會影響驅動程式本身所使用的語言，因為其目前僅以英文提供，而且其並不會影響底層 ODBC 驅動程式的語言 (其語言是由安裝在用戶端系統上的當地語系化版本所決定)。 因此，變更此設定可能會導致訊息以不同的語言傳回，取決於其是來自 PHP 驅動程式、ODBC 驅動程式或 SQL Server。|預設值為在 SQL Server 中設定的語言。|
|LoginTimeout|整數 (SQLSRV 驅動程式)<br /><br />字串 (PDO_SQLSRV 驅動程式)|指定將連接嘗試認定為失敗之前所等候的秒數。|不會逾時。|  
|MultipleActiveResultSets|1 或 **true** 會使用 Multiple Active Result Sets。<br /><br />0 或 **false** 會停用 Multiple Active Result Sets。|停用或明確啟用 Multiple Active Result Set (MARS) 的支援。<br /><br />如需詳細資訊，請參閱[如何：停用 Multiple Active Result Set &#40;MARS&#41;](how-to-disable-multiple-active-resultsets-mars.md)。|true (1)|  
|MultiSubnetFailover|String|在連接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 容錯移轉叢集執行個體時，永遠指定 `multiSubnetFailover=yes`。 `multiSubnetFailover=yes` 會設定 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，以提供對 (目前) 使用中伺服器更快速的偵測與連線。 可能的值為 [是] 和 [否]。<br /><br />如需適用於 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 之 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支援的詳細資訊，請參閱[高可用性與災害復原的支援](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|否|  
|PWD<br /><br />(PDO_SQLSRV 驅動程式不支援)|String|指定在使用 SQL Server 驗證進行連接時所要使用之使用者識別碼的相關密碼<sup>4</sup>。|未設定。|  
|QuotedId|1 或 **true** 會使用 SQL-92 規則。<br /><br />0 或 **false** 會使用傳統規則。|指定是對引號識別項使用 SQL-92 規則 (1 或 **true**)，還是使用傳統的 Transact-SQL 規則 (0 或 **false**)。|**true** (1)|  
|ReturnDatesAsStrings<br /><br />(PDO_SQLSRV 驅動程式不支援)|1 或 **true** 會以字串的形式傳回日期和時間類型。<br /><br />0 或 **false** 會以 PHP **DateTime** 類型的形式傳回日期和時間類型。|以字串或 PHP 類型的形式擷取日期和時間類型 (datetime、smalldatetime、date、time、datetime2 與 datetimeoffset)。 如需詳細資訊，請參閱[如何：使用 SQLSRV 驅動程式以字串形式擷取日期和時間類型](how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)。 <br /><br />使用 PDO_SQLSRV 驅動程式時，除非另外指定，否則會以字串的形式傳回日期。 如需詳細資訊，請參閱[如何：使用 PDO_SQLSRV 驅動程式以 PHP DateTime 物件形式擷取日期和時間類型](how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|**false**|
|可捲動|String|「緩衝處理」表示您需要用戶端 (緩衝) 資料指標，它可讓您快取記憶體中的整個結果集。 如需詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式&#41;](cursor-types-sqlsrv-driver.md)。|順向資料指標|  
|伺服器<br /><br />(SQLSRV 驅動程式不支援)|String|要連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。<br /><br />您也可以指定虛擬網路名稱，以連接到 AlwaysOn 可用性群組。 如需適用於 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 之 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支援的詳細資訊，請參閱[高可用性與災害復原的支援](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|伺服器是必要的關鍵字 (雖然它不一定是連接字串中的第一個關鍵字)。 如果未將伺服器名稱傳遞至關鍵字，會嘗試連接到本機執行個體。<br /><br />傳遞至伺服器的值可為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱，或是執行個體的 IP 位址。 您可以選擇性地指定連接埠號碼 (例如 `sqlsrv:server=(local),1033`)。<br /><br />從 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版開始，您也可以透過 `server=(localdb)\instancename`指定 LocalDB 執行個體。 如需詳細資訊，請參閱[支援 LocalDB](php-driver-for-sql-server-support-for-localdb.md)。|  
|TraceFile|String|為用於追蹤資料的檔案指定路徑。|未設定。|  
|TraceOn|1 或 **true** 會啟用追蹤。<br /><br />0 或 **false** 會停用追蹤。|指定對於要建立的連接是要啟用 ODBC 追蹤 (1 或 **true**)，還是加以停用 (0 或 **false**)。|**false** (0)|  
|TransactionIsolation|SQLSRV 驅動程式會使用下列值：<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />PDO_SQLSRV 驅動程式會使用下列值：<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|指定交易隔離等級。<br /><br />如需交易隔離的詳細資訊，請參閱 SQL Server 文件中的[設定交易隔離等級](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。|SQLSRV_TXN_READ_COMMITTED<br /><br />或<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|[啟用]  或 [停用] |在第一個解析的主機名稱 IP 沒有回應，且該主機名稱有多個相關聯的 IP 時影響連線順序。<br /><br />其會與 `MultiSubnetFailover` 互動以提供不同的連線順序。 如需詳細資訊，請參閱[透明網路 IP 解析](php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)或[使用透明網路 IP 解析](../odbc/using-transparent-network-ip-resolution.md) \(部分機器翻譯\)。|啟用|
|TrustServerCertificate|1 或 **true** 會信任憑證。<br /><br />0 或 **false** 會不信任憑證。|指定用戶端應信任 (1 或 **true**) 還是拒絕 (0 或 **false**) 自我簽署的伺服器憑證。|**false** (0)|  
|UID<br /><br />(PDO_SQLSRV 驅動程式不支援)|String|指定在使用 SQL Server 驗證進行連接時所要使用的使用者識別碼<sup>4</sup>。|未設定。|  
|WSID|String|指定用於追蹤之電腦的名稱。|未設定。|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. `ConnectionPooling` 屬性無法用來啟用/停用 Linux 和 macOS 上的連線共用。 請參閱[連接共用 (Microsoft Drivers for PHP for SQL Server)](connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。

2. 在已建立的連線上執行的所有查詢，都會針對 `Database` 屬性所指定的資料庫執行。 不過，如果使用者有適當的權限，則可以使用完整名稱來存取其他資料庫中的資料。 例如，如果 *master* 資料庫是搭配 `Database` 連線屬性設定，仍然可能透過使用完整名稱來執行存取 *AdventureWorks.HumanResources.Employee* 資料表的 Transact-SQL 查詢。  

3. 啟用 `Encryption` 可能會影響某些應用程式的效能，因為將資料加密會產生額外的計算負荷。  

4. 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連線時，必須同時設定 `UID` 和 `PWD` 屬性。  

許多支援的索引鍵都是 ODBC 連接字串屬性。 如需 ODBC 連接字串的資訊，請參閱[搭配 SQL Native Client 使用連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。

## <a name="see-also"></a>另請參閱  
[連線到伺服器](connecting-to-the-server.md)  
