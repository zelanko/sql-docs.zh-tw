---
title: 使用 OLE DB 驅動程式中的連接字串關鍵字，適用於 SQL Server |Microsoft 文件
description: 使用 OLE DB 驅動程式中的連接字串關鍵字，適用於 SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 40aeb07deacbc5e1341f3d38abf5595986cedd48
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612243"
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>使用 OLE DB 驅動程式中的連接字串關鍵字，適用於 SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server Api 有些 OLE DB 驅動程式會使用連接字串來指定連接屬性。 連接字串是關鍵字和關聯值的清單，每一個關鍵字都會識別特定的連接屬性。  
  
> **注意：** OLE DB 驅動程式的 SQL Server 允許模稜兩可，為了維持回溯相容性的連接字串中 (例如，某些關鍵字可能會指定一次以上，而位置為基礎的解析可能會允許衝突的關鍵字或優先順序）。 OLE DB 驅動程式的 SQL Server 的未來版本可能不允許模稜兩可的連接字串。 修改用來消除連接字串模稜兩可的相依性的 OLE DB 驅動程式的 SQL Server 的應用程式時，它會是很好的作法。  
  
 下列章節說明可以搭配 OLE DB 驅動程式的 SQL Server 和 ActiveX Data Objects (ADO) 使用的 SQL Server 的 OLE DB 驅動程式做為資料提供者時的關鍵字。  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB 驅動程式連接字串關鍵字  
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
  
|關鍵字|初始化屬性|描述|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|"Address" 的同義字。|  
|**位址**|SSPROP_INIT_NETWORKADDRESS|執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之伺服器的網路位址。 **位址**通常是伺服器的網路名稱，但可以是其他名稱，例如管道、 IP 位址或 TCP/IP 通訊埠和通訊端位址。<br /><br /> 若您指定 IP 位址，請確定在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員中已啟用 TCP/IP 或具名管道通訊協定。<br /><br /> 值**位址**傳遞給的值的優先順序高於**伺服器**時使用的 SQL Server 的 OLE DB 驅動程式的連接字串中。 也請注意，`Address=;`會連線到伺服器中指定**伺服器**關鍵字，而`Address= ;, Address=.;`， `Address=localhost;`，和`Address=(local);`all 導致本機伺服器的連接。<br /><br /> 完整語法**位址**關鍵字如下所示：<br /><br /> [*通訊協定 ***:**]* 位址 *[* *，* * * 連接埠&#124;\pipe\pipename*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** (共用記憶體) 或 **np** (具名管道)。 如需通訊協定的詳細資訊，請參閱[Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md)。<br /><br /> 如果沒有*通訊協定*和**網路**指定關鍵字，OLE DB 驅動程式的 SQL Server 將使用中指定的通訊協定順序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *連接埠*是連接、 指定的伺服器上的連接埠。 根據預設，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用通訊埠 1433。|   
|**應用程式**|SSPROP_INIT_APPNAME|識別應用程式的字串。|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。<br /><br /> 預設值是**ReadWrite**。 如需 OLE DB 驅動程式的 SQL Server 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[OLE DB 驅動程式的高可用性、 災害復原的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|可附加資料庫的主要檔案名稱，包括完整路徑名稱。 若要使用**AttachDBFileName**，您也必須使用提供者字串 Database 關鍵字指定資料庫名稱。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它 (它會使用附加的資料庫當做連接的預設值)。|  
|**自動轉譯**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" 的同義字。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|設定 OEM/ANSI 字元轉譯。 可辨識的值為 "yes" 和 "no"。|  
|**[資料庫備份]**|DBPROP_INIT_CATALOG|資料庫名稱。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的資料類型處理模式。 認得的值為 "0" (代表提供者資料類型) 和 "80" (代表 SQL Server 2000 資料類型)。|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|指定當透過網路傳送資料以前，是否應該先加密資料。 可能的值為 "yes" 和 "no"。 預設值為 "no"。|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|用於資料庫鏡像的容錯移轉伺服器名稱。|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 OLE DB 驅動程式的 SQL Server 使用預設值，提供者產生的 SPN。|  
|**語言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言。|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|當伺服器為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本時，啟用或停用連接上的 Multiple Active Result Sets (MARS)。 可能的值為 "yes" 和 "no"。 預設值為 "no"。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|請務必指定**MultiSubnetFailover = Yes**連接到可用性群組接聽程式時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性群組或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]容錯移轉叢集執行個體。 **MultiSubnetFailover = Yes**設定 OLE DB 驅動程式提供更快速偵測與連接 （目前） 使用中伺服器的 SQL server。 可能的值為 [是] 和 [否]。 預設值是**否**。 例如：<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 如需 OLE DB 驅動程式的 SQL Server 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[OLE DB 驅動程式的高可用性、 災害復原的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**net**|SSPROP_INIT_NETWORKLIBRARY|"Network" 的同義字。|  
|**網路**|SSPROP_INIT_NETWORKLIBRARY|用來建立組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之連接的網路程式庫。|  
|**網路程式庫**|SSPROP_INIT_NETWORKLIBRARY|"Network" 的同義字。|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|網路封包大小。 預設值為 4096。|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受的值為 "yes" 和 "no" 字串。 當為 "no" 時，不允許使用資料來源物件來保存敏感性驗證資訊。|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入密碼。|  
|**Server**|DBPROP_INIT_DATASOURCE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。 此值必須是網路上的伺服器名稱、IP 位址，或是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員別名的名稱。<br /><br /> 如果沒有指定，就會連接至本機電腦上的預設執行個體。<br /><br /> **位址**關鍵字會覆寫**伺服器**關鍵字。<br /><br /> 您可藉由指定下列其中一個項目，連接到本機伺服器上的預設執行個體：<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> 如需有關 LocalDB 支援的詳細資訊，請參閱[OLE DB 驅動程式為 localdb 的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)。<br /><br /> 若要指定的具名執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，附加 **\\ ***InstanceName *。<br /><br />如果未不指定任何伺服器，會連接到本機電腦上預設執行個體。<br /><br />如果您指定的 IP 位址，請確定中已啟用 TCP/IP 或具名的管道通訊協定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br />完整語法**伺服器**關鍵字如下：<br /> <br /> **Server =**[* 通訊協定***:**]*伺服器*[**，* * * 連接埠*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** (共用記憶體) 或 **np** (具名管道)。<br /><br /> 下列是指定具名管道的範例：<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 此程式碼行指定具名管道通訊協定、本機電腦上的具名管道 (`\\.\pipe`)、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱 (`MSSQL$MYINST01`) 以及具名管道的預設名稱 (`sql/query`)。<br /><br /> 如果沒有*通訊協定*和**網路**指定關鍵字，OLE DB 驅動程式的 SQL Server 將使用中指定的通訊協定順序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *連接埠*是連接、 指定的伺服器上的連接埠。 根據預設，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會使用通訊埠 1433。<br /><br /> 傳遞給的值開頭的空格會被忽略**伺服器**時使用的 SQL Server 的 OLE DB 驅動程式的連接字串中。|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|伺服器的 SPN。 預設值為空字串。 空字串會讓 OLE DB 驅動程式的 SQL Server 使用預設值，提供者產生的 SPN。|  
|**逾時**|DBPROP_INIT_TIMEOUT|等候資料來源初始化完成的時間量 (以秒為單位)。|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|當"yes"時，會指示 SQL Server 使用 Windows 驗證模式進行登入驗證，OLE DB 驅動程式。 否則會指示 SQL Server 以使用 OLE DB 驅動程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]必須指定使用者名稱和密碼登入驗證，以及 UID 和 PWD 關鍵字。|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受的值為 "yes" 和 "no" 字串。 預設值為 "no"，這表示將會驗證伺服器憑證。|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入名稱。|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|這個關鍵字已被取代，而且它的設定會忽略 OLE DB 驅動程式適用於 SQL Server。|  
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
  
|關鍵字|初始化屬性|描述|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|識別應用程式的字串。|  
|**應用程式意圖**|SSPROP_INIT_APPLICATIONINTENT|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。<br /><br /> 預設值是**ReadWrite**。 如需 OLE DB 驅動程式的 SQL Server 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[OLE DB 驅動程式的高可用性、 災害復原的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**自動轉譯**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" 的同義字。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|設定 OEM/ANSI 字元轉譯。 認得的值為 "true" 和 "false"。|  
|**連接逾時**|DBPROP_INIT_TIMEOUT|等候資料來源初始化完成的時間量 (以秒為單位)。|  
|**目前的語言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言名稱。|  
|**資料來源**|DBPROP_INIT_DATASOURCE|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。<br /><br /> 如果沒有指定，就會連接至本機電腦上的預設執行個體。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**伺服器**關鍵字，本主題中的。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的資料類型處理模式。 認得的值為 "0" (代表提供者資料類型) 和 "80" (代表 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 資料類型)。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用於資料庫鏡像的容錯移轉伺服器名稱。|  
|**容錯移轉夥伴 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 OLE DB 驅動程式的 SQL Server 使用預設值，提供者產生的 SPN。|  
|**初始目錄**|DBPROP_INIT_CATALOG|資料庫名稱。|  
|**初始檔案名稱**|SSPROP_INIT_FILENAME|可附加資料庫的主要檔案名稱，包括完整路徑名稱。 若要使用**AttachDBFileName**，您也必須使用提供者字串 DATABASE 關鍵字指定資料庫名稱。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它 (它會使用附加的資料庫當做連接的預設值)。|  
|**整合式安全性**|DBPROP_AUTH_INTEGRATED|接受 "SSPI" 值進行 Windows 驗證。|  
|**MARS 連接**|SSPROP_INIT_MARSCONNECTION|啟用或停用連接上的 Multiple Active Result Sets (MARS)。 認得的值為 "true" 和 "false"。 預設值為 "false"。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|請務必指定**MultiSubnetFailover = True**連接到可用性群組接聽程式時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性群組或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]容錯移轉叢集執行個體。 **MultiSubnetFailover = True**設定 OLE DB 驅動程式提供更快速偵測與連接 （目前） 使用中伺服器的 SQL server。 可能的值為 **True** 和 **False**。 預設值為 **False**。 例如：<br /><br /> `MultiSubnetFailover=True`<br /><br /> 如需 OLE DB 驅動程式的 SQL Server 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[OLE DB 驅動程式的高可用性、 災害復原的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**網路位址**|SSPROP_INIT_NETWORKADDRESS|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的網路位址。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**位址**關鍵字，本主題中的。|  
|**網路程式庫**|SSPROP_INIT_NETWORKLIBRARY|用來建立組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之連接的網路程式庫。|  
|**封包大小**|SSPROP_INIT_PACKETSIZE|網路封包大小。 預設值為 4096。|  
|**密碼**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入密碼。|  
|**保存安全性資訊**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受的值為 "true" 和 "false" 字串。 當為 "false" 時，不允許使用資料來源物件來保存敏感性驗證資訊。|  
|**提供者**||OLE DB driver for SQL Server，這應該是"MSOLEDBSQL"。|  
|**伺服器的 SPN**|SSPROP_INIT_SERVERSPN|伺服器的 SPN。 預設值為空字串。 空字串會讓 OLE DB 驅動程式的 SQL Server 使用預設值，提供者產生的 SPN。|  
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
  
|關鍵字|初始化屬性|描述|  
|-------------|-----------------------------|-----------------|  
|**應用程式意圖**|SSPROP_INIT_APPLICATIONINTENT|宣告連接到伺服器時的應用程式工作負載類型。 可能的值為**ReadOnly**和**ReadWrite**。<br /><br /> 預設值是**ReadWrite**。 如需 OLE DB 驅動程式的 SQL Server 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[OLE DB 驅動程式的高可用性、 災害復原的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**Application Name**|SSPROP_INIT_APPNAME|識別應用程式的字串。|  
|**自動轉譯**|SSPROP_INIT_AUTOTRANSLATE|"AutoTranslate" 的同義字。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|設定 OEM/ANSI 字元轉譯。 認得的值為 "true" 和 "false"。|  
|**連接逾時**|DBPROP_INIT_TIMEOUT|等候資料來源初始化完成的時間量 (以秒為單位)。|  
|**目前的語言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 語言名稱。|  
|**資料來源**|DBPROP_INIT_DATASOURCE|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。<br /><br /> 如果沒有指定，就會連接至本機電腦上的預設執行個體。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**伺服器**關鍵字，本主題中的。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定即將使用之資料類型處理的模式。 認得的值為 "0" (代表提供者資料類型) 和 "80" (代表 SQL Server 2000 資料類型)。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用於資料庫鏡像的容錯移轉伺服器名稱。|  
|**容錯移轉夥伴 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|容錯移轉夥伴的 SPN。 預設值為空字串。 空字串會讓 OLE DB 驅動程式的 SQL Server 使用預設值，提供者產生的 SPN。|  
|**初始目錄**|DBPROP_INIT_CATALOG|資料庫名稱。|  
|**初始檔案名稱**|SSPROP_INIT_FILENAME|可附加資料庫的主要檔案名稱，包括完整路徑名稱。 若要使用**AttachDBFileName**，您也必須使用提供者字串 DATABASE 關鍵字指定資料庫名稱。 如果之前已附加資料庫，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會重新附加它 (它會使用附加的資料庫當做連接的預設值)。|  
|**整合式安全性**|DBPROP_AUTH_INTEGRATED|接受 "SSPI" 值進行 Windows 驗證。|  
|**MARS 連接**|SSPROP_INIT_MARSCONNECTION|當伺服器為 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本時，啟用或停用連接上的 Multiple Active Result Sets (MARS)。 認得的值為 "true" 和 "false"。預設值是 "false"。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|請務必指定**MultiSubnetFailover = True**連接到可用性群組接聽程式時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性群組或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]容錯移轉叢集執行個體。 **MultiSubnetFailover = True**設定 OLE DB 驅動程式提供更快速偵測與連接 （目前） 使用中伺服器的 SQL server。 可能的值為 **True** 和 **False**。 預設值為 **False**。 例如：<br /><br /> `MultiSubnetFailover=True`<br /><br /> 如需 OLE DB 驅動程式的 SQL Server 支援[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，請參閱[OLE DB 驅動程式的高可用性、 災害復原的 SQL Server 支援](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**網路位址**|SSPROP_INIT_NETWORKADDRESS|組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的網路位址。<br /><br /> 如需有關有效位址語法的詳細資訊，請參閱的描述**位址**關鍵字，本主題中的。|  
|**網路程式庫**|SSPROP_INIT_NETWORKLIBRARY|用來建立組織中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之連接的網路程式庫。|  
|**封包大小**|SSPROP_INIT_PACKETSIZE|網路封包大小。 預設值為 4096。|  
|**密碼**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入密碼。|  
|**保存安全性資訊**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受的值為 "true" 和 "false" 字串。 如果為 "false"，表示不允許資料來源物件保存機密的驗證資訊。|  
|**提供者**||OLE DB driver for SQL Server，這應該是"MSOLEDBSQL"。|  
|**伺服器的 SPN**|SSPROP_INIT_SERVERSPN|伺服器的 SPN。 預設值為空字串。 空字串會讓 OLE DB 驅動程式的 SQL Server 使用預設值，提供者產生的 SPN。|  
|**信任伺服器憑證**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受的值為 "true" 和 "false" 字串。 預設值為 "false"，這表示將會驗證伺服器憑證。|  
|**使用加密資料**|SSPROP_INIT_ENCRYPT|指定當透過網路傳送資料以前，是否應該先加密資料。 可能的值為 "true" 和 "false"。 預設值為 "false"。|  
|**使用者識別碼**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入名稱。|  
|**工作站識別碼**|SSPROP_INIT_WSID|工作站識別碼。|  
  
 **請注意**在連接字串中，"Old Password"屬性會設定 SSPROP_AUTH_OLD_PASSWORD，這是不是透過提供者字串屬性目前的 （可能已過期） 密碼。  
  
## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
