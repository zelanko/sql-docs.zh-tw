---
title: 連接選項 |Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e13ec1359e2072c92ffa06e218228730f323222
ms.sourcegitcommit: c1105ce638078d2c941cd656b34f78486e6b2d89
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/22/2019
ms.locfileid: "56676277"
---
# <a name="connection-options"></a>連線選項
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題列出關聯陣列中允許的選項 (在 SQLSRV 驅動程式中使用 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) 時) 或資料來源名稱 (dsn) 中允許的關鍵字 (在 PDO_SQLSRV 驅動程式中使用 [PDO::__construct](../../connect/php/pdo-construct.md) 時)。  

## <a name="table-of-connection-options"></a>連線選項表

|機碼|ReplTest1|描述|預設|  
|-------|---------|---------------|-----------|  
|AccessToken|String|Azure AD 存取權杖的 OAuth JSON 回應中擷取的位元組的字串。<br /><br />連接字串必須包含使用者識別碼、 密碼或驗證關鍵字。 如需詳細資訊，請參閱[連線使用 Azure Active Directory 驗證](../../connect/php/azure-active-directory.md)|未設定。|
|APP|String|指定在追蹤中使用的應用程式名稱。|未設定。|  
|ApplicationIntent|String|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為 ReadOnly 和 ReadWrite。<br /><br />如需詳細資訊[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]支援[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]，請參閱[支援高可用性、 災害復原](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|ReadWrite|  
|AttachDBFileName|String|指定伺服器所應附加的資料庫檔案。|未設定。|  
|驗證|下列字串之一：<br /><br />'SqlPassword'<br /><br />'ActiveDirectoryPassword'<br /><br />'ActiveDirectoryMsi'|指定驗證模式。<br /><br />如需詳細資訊，請參閱[連線使用 Azure Active Directory 驗證](../../connect/php/azure-active-directory.md)|未設定。|
|CharacterSet<br /><br />(PDO_SQLSRV 驅動程式不支援)|String|指定用來將資料傳送至伺服器的字元集。<br /><br />可能的值為 SQLSRV_ENC_CHAR 和 UTF-8。 如需詳細資訊，請參閱 [如何：使用內建的 UTF-8 支援傳送及接收 UTF-8 資料](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)。|SQLSRV_ENC_CHAR|  
|ColumnEncryption|[啟用] 或 [停用]|指定是否啟用了 Always Encrypted 功能。 |已停用|  
|ConnectionPooling|1 或 **true** 表示開啟連接共用。<br /><br />0 或 **false** 表示關閉連接共用。|指定要從連接集區指派連接 (1 或 **true**)，還是不要指派 (0 或 **false**)。<sup>1</sup>|**true** (1)|  
|ConnectRetryCount|介於 0 和 255 之間 （含） 之間的整數|若要重新建立放棄之前中斷的連線的嘗試次數上限。 根據預設，單一嘗試重新建立連線時中斷。 值 0 表示沒有重新連線將會嘗試。|1|  
|ConnectRetryInterval|介於 1 到 60 （含） 之間的整數|時間 （秒），嘗試重新建立連線。 應用程式會嘗試立即重新連線，一旦偵測連線中斷，而且會然後等到 ConnectRetryInterval 秒後再試一次。 如果 ConnectRetryCount 等於 0，則會忽略這個關鍵字。|1|  
|[資料庫]|String|指定要建立的連接使用中的資料庫名稱<sup>2</sup>。|使用登入的預設資料庫。|  
|DecimalPlaces<br /><br />(PDO_SQLSRV 驅動程式不支援)|介於 0 到 4 （含） 之間的整數|指定小數位數，格式化時提取貨幣值。<br /><br />此選項僅適用於 FormatDecimals 為 true。 將忽略任何負整數或值大於 4。|預設有效位數和小數位數|
|驅動程式|String|指定用來與 SQL Server 通訊的 Microsoft ODBC 驅動程式。<br /><br />可能的值為：<br />ODBC Driver 17 for SQL Server<br />ODBC Driver 13 for SQL Server<br />ODBC Driver 11 for SQL Server (僅 Windows)。|當未指定 Driver 關鍵字時，Microsoft Drivers for PHP for SQL Server 嘗試尋找支援的 Microsoft ODBC 驅動程式在系統中，最新的 ODBC 版本開始，依此類推。| 
|Encrypt|1 或 **true** 表示開啟加密。<br /><br />0 或 **false** 表示關閉加密。|指定要加密與 SQL Server 的通訊 (1 或 **true**)，還是不要加密 (0 或 **false**)<sup>3</sup>。|**false** (0)|  
|FormatDecimals<br /><br />(PDO_SQLSRV 驅動程式不支援)|1 或 **，則為 true**擷取十進位字串的格式。<br /><br />0 或**false**十進位的預設格式化行為。|指定是否要加入開頭為十進位字串適當時歸零，並可讓`DecimalPlaces`格式化 money 類型的選項。 如果保留，則為 false，則會使用傳回精確的有效位數，並省略前置字元小於 1 的值為零的預設行為。<br /><br />如需詳細資訊，請參閱 <<c0> [ 格式化為十進位字串和貨幣值](../../connect/php/formatting-decimals-sqlsrv-driver.md)。|**false** (0)|
|Failover_Partner|String|指定在主要伺服器無法使用時所要使用的伺服器和資料庫鏡像執行個體 (如果已啟用和設定)。<br /><br />搭配使用 Failover_Partner 與 MultiSubnetFailover 時有一些限制。 如需詳細資訊，請參閱 <<c0> [ 支援高可用性、 災害復原](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|未設定。|  
|KeyStoreAuthentication|**KeyVaultPassword**<br /><br />**KeyVaultClientSecret**|用於存取 Azure 金鑰保存庫的驗證方法。 控制 KeyStorePrincipalId 和 KeyStoreSecret 搭配使用何種認證。 如需詳細資訊，請參閱 <<c0> [ 使用 Azure Key Vault](../../connect/php/using-always-encrypted-php-drivers.md###using-azure-key-vault)。|未設定。|
|KeyStorePrincipalId|String|想要存取 Azure Key Vault 的帳戶識別碼。 <br /><br />如果 KeyStoreAuthentication **KeyVaultPassword**，這必須是 Azure Active Directory 使用者名稱。 <br /><br />如果 KeyStoreAuthentication **KeyVaultClientSecret**，這必須是應用程式用戶端識別碼。|未設定。|
|KeyStoreSecret|String|想要存取 Azure Key Vault 的帳戶的認證密碼。 <br /><br />如果 KeyStoreAuthentication **KeyVaultPassword**，這必須是 Azure Active Directory 密碼。 <br /><br />如果 KeyStoreAuthentication **KeyVaultClientSecret**，這必須是應用程式用戶端祕密。|未設定。|
|LoginTimeout|整數 (SQLSRV 驅動程式)<br /><br />字串 (PDO_SQLSRV 驅動程式)|指定將連接嘗試認定為失敗之前所等候的秒數。|不會逾時。|  
|MultipleActiveResultSets|1 或 **true** 會使用 Multiple Active Result Sets。<br /><br />0 或 **false** 會停用 Multiple Active Result Sets。|停用或明確啟用 Multiple Active Result Sets (MARS) 的支援。<br /><br />如需詳細資訊，請參閱[如何：停用 Multiple Active Result Set &#40;MARS&#41;](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)。|true (1)|  
|MultiSubnetFailover|String|在連接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 容錯移轉叢集執行個體時，一律指定 **multiSubnetFailover=yes**。 **multiSubnetFailover=yes** 會設定 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，以提供對 (目前) 動態伺服器更快速的偵測與連接。 可能的值為 [是] 和 [否]。<br /><br />如需詳細資訊[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]支援[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]，請參閱[支援高可用性、 災害復原](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|否|  
|PWD<br /><br />(PDO_SQLSRV 驅動程式不支援)|String|指定在使用 SQL Server 驗證進行連接時所要使用之使用者識別碼的相關密碼<sup>4</sup>。|未設定。|  
|QuotedId|1 或 **true** 會使用 SQL-92 規則。<br /><br />0 或 **false** 會使用傳統規則。|指定是對引號識別項使用 SQL-92 規則 (1 或 **true**)，還是使用傳統的 Transact-SQL 規則 (0 或 **false**)。|**true** (1)|  
|ReturnDatesAsStrings<br /><br />(PDO_SQLSRV 驅動程式不支援)|1 或 **true** 會以字串的形式傳回日期和時間類型。<br /><br />0 或 **false** 會以 PHP **DateTime** 類型的形式傳回日期和時間類型。|以字串或 PHP 類型的形式擷取日期和時間類型 (datetime、smalldatetime、date、time、datetime2 與 datetimeoffset)。 如需詳細資訊，請參閱[如何：使用 SQLSRV 驅動程式以字串的形式擷取日期和時間類型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)。 <br /><br />使用 PDO_SQLSRV 驅動程式時，日期是以字串傳回，除非另有指定。 如需詳細資訊，請參閱 <<c0> [ 如何： 擷取日期和時間類型做為 PHP DateTime 物件使用 PDO_SQLSRV 驅動程式](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md)。|**false**|
|可捲動|String|「緩衝處理」表示您需要用戶端 (緩衝) 資料指標，它可讓您快取記憶體中的整個結果集。 如需詳細資訊，請參閱[資料指標類型 &#40;SQLSRV 驅動程式&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)。|順向資料指標|  
|[伺服器]<br /><br />(SQLSRV 驅動程式不支援)|String|要連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。<br /><br />您也可以指定虛擬網路名稱，以連接到 AlwaysOn 可用性群組。 如需詳細資訊[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]支援[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]，請參閱[支援高可用性、 災害復原](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|伺服器是必要的關鍵字 (雖然它不一定是連接字串中的第一個關鍵字)。 如果未將伺服器名稱傳遞至關鍵字，會嘗試連接到本機執行個體。<br /><br />傳遞至伺服器的值可為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱，或是執行個體的 IP 位址。 您可以選擇性地指定連接埠號碼 (例如 `sqlsrv:server=(local),1033`)。<br /><br />從 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版開始，您也可以透過 `server=(localdb)\instancename`指定 LocalDB 執行個體。 如需詳細資訊，請參閱 < [LocalDB 的支援](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。|  
|TraceFile|String|為用於追蹤資料的檔案指定路徑。|未設定。|  
|TraceOn|1 或 **true** 會啟用追蹤。<br /><br />0 或 **false** 會停用追蹤。|指定對於要建立的連接是要啟用 ODBC 追蹤 (1 或 **true**)，還是加以停用 (0 或 **false**)。|**false** (0)|  
|TransactionIsolation|SQLSRV 驅動程式會使用下列值：<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />PDO_SQLSRV 驅動程式會使用下列值：<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|指定交易隔離等級。<br /><br />如需交易隔離的詳細資訊，請參閱 SQL Server 文件中的[設定交易隔離等級](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。|SQLSRV_TXN_READ_COMMITTED<br /><br />中的多個<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|TransparentNetworkIPResolution|[啟用] 或 [停用]|會影響與主機名稱，相關聯的連接順序，當第一個問題解決之後，主機名稱的 IP 沒有回應，而且有多個 Ip。<br /><br />它與 MultiSubnetFailover 提供不同的連接順序的互動。 如需詳細資訊，請參閱 <<c0> [ 透明網路 IP 解析](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)或是[使用無形網路 IP 解析](https://docs.microsoft.com/sql/connect/odbc/using-transparent-network-ip-resolution)。|已啟用|
|TrustServerCertificate|1 或 **true** 會信任憑證。<br /><br />0 或 **false** 會不信任憑證。|指定用戶端應信任 (1 或 **true**) 還是拒絕 (0 或 **false**) 自我簽署的伺服器憑證。|**false** (0)|  
|UID<br /><br />(PDO_SQLSRV 驅動程式不支援)|String|指定在使用 SQL Server 驗證進行連接時所要使用的使用者識別碼<sup>4</sup>。|未設定。|  
|WSID|String|指定用於追蹤之電腦的名稱。|未設定。|  

1. `ConnectionPooling`屬性不能啟用/停用連線集區在 Linux 和 mac。 請參閱[連接共用 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。

2. 所有在已建立的連接上執行的查詢，都會對 *Database* 屬性所指定的資料庫執行。 不過，如果使用者有適當的權限，則可以使用完整名稱來存取其他資料庫中的資料。 例如，如果 *master* 資料庫是使用 *Database* 連接屬性來設定，就仍然可以執行 Transact-SQL 查詢，以使用完整名稱存取 *AdventureWorks.HumanResources.Employee* 資料表。  

3. 啟用 [加密]  後可能會影響某些應用程式的效能，因為加密資料需要額外的計算負荷。  

4. 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，*UID* 和 *PWD* 屬性都必須設定。  

許多支援的索引鍵都是 ODBC 連接字串屬性。 如需 ODBC 連接字串的相關資訊，請參閱 [搭配 SQL Native Client 使用連接字串關鍵字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。

## <a name="see-also"></a>另請參閱  
[連線到伺服器](../../connect/php/connecting-to-the-server.md)  
