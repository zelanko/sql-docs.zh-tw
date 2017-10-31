---
title: "SERVERPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SERVERPROPERTY_TSQL
- SERVERPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SERVERPROPERTY function
- server instance property information [SQL Server]
- IsHadrEnabled server property
- instances of SQL Server, property information
- server properties [SQL Server]
ms.assetid: 11e166fa-3dd2-42d8-ac4b-04f18c612c4a
caps.latest.revision: 128
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7060a8aaf668a69184503fa0995dd4f37085d5f1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="serverproperty-transact-sql"></a>SERVERPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回有關伺服器執行個體的屬性資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SERVERPROPERTY ( 'propertyname' )  
```  
  
## <a name="arguments"></a>引數  
 *屬性名稱*  
 這是包含要傳回伺服器之屬性資訊的運算式。 *propertyname*可以是下列值之一。  
  
|屬性|傳回的值|  
|--------------|---------------------|  
|BuildClrVersion|版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] common language runtime (CLR) 建立的執行個體時所用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|定序|伺服器預設定序的名稱。<br /><br /> NULL = 輸入無效，或發生錯誤。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|CollationID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序的識別碼。<br /><br /> 基底資料型別： **int**|  
|ComparisonStyle|Windows 的定序比較樣式。<br /><br /> 基底資料型別： **int**|  
|ComputerNamePhysicalNetBIOS|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體目前執行所在之本機電腦的 NetBIOS 名稱。<br /><br /> 如果是容錯移轉叢集中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 叢集執行個體，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體容錯移轉到容錯移轉叢集中的其他節點時，這個值會跟著改變。<br /><br /> 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的獨立執行個體中，這個值會維持不變，且會傳回與 MachineName 屬性相同的值。<br /><br /> **注意：**如果執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是在容錯移轉叢集，而且您想要取得容錯移轉叢集執行個體的名稱，請使用 MachineName 屬性。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|版本|已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體產品版本。 使用這個屬性的值決定功能和限制，例如[Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。 64 位元版的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將 (64 位元) 附加至版本中。<br /><br /> 傳回：<br /><br /> 'Enterprise Edition'<br /><br /> ‘Enterprise 版: 核心授權’<br /><br /> 'Enterprise Evaluation Edition'<br /><br /> 'Business Intelligence Edition'<br /><br /> 'Developer Edition'<br /><br /> 'Express Edition'<br /><br /> 'Express Edition with Advanced Services'<br /><br /> 'Standard Edition'<br /><br /> 'Web Edition'<br /><br /> ' SQL Azure' 表示[!INCLUDE[ssSDS](../../includes/sssds-md.md)]或[!INCLUDE[ssDW](../../includes/ssdw-md.md)]<br /><br /> 基底資料型別： **nvarchar （128)**|  
|EditionID|EditionID 表示安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體產品版本。 使用這個屬性的值決定功能和限制，例如[Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。<br /><br /> 1804890536 = Enterprise<br /><br /> 1872460670 = Enterprise 版: 核心授權<br /><br /> 610778273= Enterprise Evaluation<br /><br /> 284895786 = Business Intelligence<br /><br /> -2117995310 = Developer<br /><br /> -1592396055 = Express<br /><br /> -133711905 = Express with Advanced Services<br /><br /> -1534726760 = standard<br /><br /> 1293598313 = Web<br /><br /> 1674378470 = SQL Database 或 SQL 資料倉儲<br /><br /> 基底資料型別： **bigint**|  
|EngineEdition|安裝在伺服器上之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。<br /><br /> 1 = Personal 或 Desktop Engine (不適用於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中)。<br /><br /> 2 = Standard (Standard、Web 和 Business Intelligence 都會傳回這個值)。<br /><br /> 3 = Enterprise (Enterprise、Developer 和兩種 Enterprise 版本都會傳回這個項目)。<br /><br /> 4 = express (Express，都會傳回這個 Express with Tools 和 Express with Advanced Services)<br /><br /> 5 = [!INCLUDE[ssSDS](../../includes/sssds-md.md)]<br /><br /> 6 - [!INCLUDE[ssDW](../../includes/ssdw-md.md)]<br /><br /> 基底資料型別： **int**|  
|HadrManagerStatus|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指出 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 管理員是否已經啟動。<br /><br /> 0 = 未啟動，暫止通訊。<br /><br /> 1 = 已啟動且在執行中。<br /><br /> 2 = 未啟動且失敗。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。|  
|InstanceDefaultDataPath|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 執行個體資料檔的預設路徑名稱。|  
|InstanceDefaultLogPath|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 執行個體的記錄檔的預設路徑名稱。|  
|InstanceName|使用者所連接之執行個體的名稱。<br /><br /> 如果執行個體名稱是預設執行個體、輸入無效，或發生錯誤，便傳回 NULL。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|IsAdvancedAnalyticsInstalled|傳回 1，表示 Advanced Analytics 功能已在安裝期間安裝。0，表示未安裝進階分析。|  
|IsClustered|伺服器執行個體設定在容錯移轉叢集中。<br /><br /> 1 = 叢集。<br /><br /> 0 = 非叢集。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**|  
|IsFullTextInstalled|全文檢索和語意索引元件安裝在目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。<br /><br /> 1 = 已安裝全文檢索和語意索引元件。<br /><br /> 0 = 未安裝全文檢索和語意索引元件。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**|  
|IsHadrEnabled|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 在這個伺服器執行個體上已啟用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。<br /><br /> 0 = [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 功能已停用。<br /><br /> 1 = [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 功能已啟用。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**<br /><br /> 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體上建立及執行可用性複本，必須在此伺服器執行個體上啟用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。 如需詳細資訊，請參閱[啟用和停用 AlwaysOn 可用性群組 (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。<br /><br /> **注意：** IsHadrEnabled 屬性只與[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。 此伺服器屬性不影響其他高可用性或災害復原功能，例如資料庫鏡像或記錄傳送。|  
|IsIntegratedSecurityOnly|伺服器處於整合式安全性模式。<br /><br /> 1 = 整合式安全性 (Windows 驗證)<br /><br /> 0 = 非整合式安全性。 (Windows 驗證及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證)。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**|  
|IsLocalDB|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 伺服器是 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] LocalDB 的執行個體。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。|  
|IsPolybaseInstalled|**適用於**： [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 傳回的伺服器執行個體是否已安裝 PolyBase 功能。<br /><br /> 0 = 未安裝 PolyBase。<br /><br /> 1 = 已安裝 PolyBase。<br /><br /> 基底資料型別： **int**|  
|IsSingleUser|伺服器處於單一使用者模式。<br /><br /> 1 = 單一使用者。<br /><br /> 0 = 非單一使用者<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**|  
|IsXTPSupported|**適用於**: SQL Server ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br /> 伺服器支援 In-Memory OLTP。<br /><br /> 1= 伺服器支援 In-Memory OLTP。<br /><br /> 0= 伺服器不支援 In-Memory OLTP。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**|  
|LCID|Windows 的定序地區設定識別碼 (LCID)。<br /><br /> 基底資料型別： **int**|  
|LicenseType|未使用的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品未保留或維護的授權資訊。 一律傳回 DISABLED。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|MachineName|執行伺服器執行個體的 Windows 電腦名稱。<br /><br /> 如果是叢集執行個體，也就是在 Microsoft Cluster Service 虛擬伺服器上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，便會傳回虛擬伺服器名稱。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|NumLicenses|未使用的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品未保留或維護的授權資訊。 一律傳回 NULL。<br /><br /> 基底資料型別： **int**|  
|ProcessID|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的處理序識別碼。 在識別哪個 Sqlservr.exe 屬於這個執行個體時，ProcessID 非常有用。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。<br /><br /> 基底資料型別： **int**|  
|ProductBuild|**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]從 2015 年 10 月開始。<br /><br /> 組建編號。|  
|ProductBuildType|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 目前的組建的組建類型。<br /><br /> 傳回下列項目之一：<br /><br /> OD = 隨選安裝的版本特定的客戶。<br /><br /> GDR = 釋放透過 windows update 的一般發行版本。<br /><br /> NULL<br />= 不適用。|  
|ProductLevel|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的版本層級。<br /><br /> 傳回下列項目之一：<br /><br /> 'RTM' = 原始發行版本<br /><br /> 'SP*n*' = Service pack 版本<br /><br /> ' CTP*n*'，= Community Technology Preview 版本<br /><br /> 基底資料型別： **nvarchar （128)**|  
|ProductMajorVersion|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 主要的版本。|  
|ProductMinorVersion|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 次要的版本。|  
|ProductUpdateLevel|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 更新目前組建的層級。 CU 表示累計更新。<br /><br /> 傳回下列項目之一：<br /><br /> CU *n*  = 累計更新<br /><br /> NULL<br />= 不適用。|  
|ProductUpdateReference|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過從晚期 2015年的更新目前的版本。<br /><br /> 該發行的知識庫文件。|  
|ProductVersion|執行個體的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，形式的 '*major.minor.build.revision*'。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|ResourceLastUpdateDateTime|傳回資源資料庫上次更新的日期和時間。<br /><br /> 基底資料型別：**日期時間**|  
|ResourceVersion|傳回版本資源資料庫。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|ServerName|指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所關聯的 Windows 伺服器和執行個體資訊。<br /><br /> NULL = 輸入無效，或發生錯誤。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|SqlCharSet|定序識別碼中的 SQL 字元集識別碼。<br /><br /> 基底資料型別： **tinyint**|  
|SqlCharSetName|定序中的 SQL 字元集名稱。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|SqlSortOrder|定序中的 SQL 排序順序識別碼<br /><br /> 基底資料型別： **tinyint**|  
|SqlSortOrderName|定序中的 SQL 排序次序名稱。<br /><br /> 基底資料型別： **nvarchar （128)**|  
|FilestreamShareName|FILESTREAM 所使用之共用的名稱。<br /><br /> NULL = 輸入無效、發生錯誤或不適用。|  
|FilestreamConfiguredLevel|已設定的 FILESTREAM 存取層級。 如需詳細資訊，請參閱[filestream 存取層級](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)。|  
|FilestreamEffectiveLevel|有效的 FILESTREAM 存取層級。 如果此層級已變更而且執行個體重新啟動或電腦重新啟動已暫止，這個值就可能會與 FilestreamConfiguredLevel 不同。 如需詳細資訊，請參閱[filestream 存取層級](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)。|  
  
## <a name="return-types"></a>傳回類型  
 **sql_variant**  
  
## <a name="remarks"></a>備註  
  
### <a name="servername-property"></a>ServerName 屬性  
 `ServerName`屬性`SERVERPROPERTY`函式和[@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)傳回類似的資訊。 `ServerName` 屬性提供共同組成唯一伺服器執行個體的 Windows 伺服器和執行個體名稱。 [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)提供目前設定的本機伺服器名稱。  
  
 `ServerName`屬性和[@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)傳回相同的資訊，如果在安裝時的預設伺服器名稱未變更。 您可以執行下列作業來設定本機伺服器名稱：  
  
```  
EXEC sp_dropserver 'current_server_name';  
GO  
EXEC sp_addserver 'new_server_name', 'local';  
GO  
```  
  
 如果本機伺服器名稱已從預設的伺服器名稱變更在安裝期間， [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)傳回新的名稱。  
  
### <a name="version-properties"></a>Version 屬性  
 `SERVERPROPERTY`函式會傳回個別屬性，與相關聯的版本資訊而[@@VERSION ](../../t-sql/functions/version-transact-sql-configuration-functions.md)函式會將輸出結合成一個字串。 如果您的應用程式需要個別屬性字串，您可以使用`SERVERPROPERTY`函式傳回它們，而非剖析[@@VERSION ](../../t-sql/functions/version-transact-sql-configuration-functions.md)結果。  

## <a name="permissions"></a>Permissions

所有使用者都可以都查詢的伺服器屬性。 
  
## <a name="examples"></a>範例  
 下列範例會使用`SERVERPROPERTY`函式在`SELECT`陳述式來傳回目前執行個體的相關資訊[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。   
  
```  
SELECT  
  SERVERPROPERTY('MachineName') AS ComputerName,
  SERVERPROPERTY('ServerName') AS InstanceName,  
  SERVERPROPERTY('Edition') AS Edition,
  SERVERPROPERTY('ProductVersion') AS ProductVersion,  
  SERVERPROPERTY('ProductLevel') AS ProductLevel;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 的版本和元件](../../sql-server/editions-and-components-of-sql-server-2016.md)  
  
  

