---
title: 用戶端連接中的服務主體名稱 (SPN) 支援 | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, SPNs
- ODBC, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
ms.assetid: 96598c69-ce9a-4090-aacb-d546591e8af7
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 415e1a46734eeed97457a6235a0d9912b17e232b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745270"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>用戶端連接中的服務主要名稱 (SPN) 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，已經擴充服務主體名稱 (SPN) 的支援以便跨所有通訊協定進行相互驗證。 在舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，只有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的預設 SPN 使用 Active Directory 註冊時，Kerberos 才能透過 TCP 支援 SPN。  
  
 驗證通訊協定會使用 SPN 來決定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體所執行的帳戶。 如果已知執行個體帳戶，可以透過用戶端和伺服器使用 Kerberos 驗證提供相互驗證。 如果未知執行個體帳戶，會使用僅透過伺服器提供用戶端驗證的 NTLM 驗證。 目前， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會執行驗證查閱，從執行個體名稱和網路連接屬性衍生 SPN。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體將會嘗試在啟動時註冊 SPN，或者也可以手動進行註冊。 不過，如果對於嘗試註冊 SPN 的帳戶沒有足夠的存取權限，註冊將會失敗。  
  
 網域和電腦帳戶會自動在 Active Directory 中註冊。 這些帳戶可以當做 SPN 使用，或者系統管理員可以定義自己的 SPN。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會允許用戶端直接指定要使用的 SPN，使安全驗證更容易管理而且更可靠。  
  
> [!NOTE]  
>  用戶端應用程式所指定的 SPN 僅能在建立與 Windows 整合式安全性的連接時使用。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** 是一種診斷工具，可幫助排除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]發生的 Kerberos 相關連接問題。 如需詳細資訊，請參閱 [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046)。  
  
 如需有關 Kerberos 的詳細資訊，請參閱下列文件：  
  
-   [Kerberos Technical Supplement for Windows](https://go.microsoft.com/fwlink/?LinkId=101449) (適用於 Windows 的 Kerberos 技術補充)  
  
-   [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>使用量  
 下表描述用戶端應用程式可允許安全驗證的常見案例。  
  
|狀況|描述|  
|--------------|-----------------|  
|舊版應用程式不會指定 SPN。|此相容性案例保證對於針對舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]開發的應用程式沒有行為上的變更。 如果沒有指定 SPN，應用程式會依賴所產生的 SPN，而且不會知道所使用的驗證方法。|  
|使用目前版本 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的用戶端應用程式會將連接字串中的 SPN 指定為網域使用者或電腦帳戶、執行個體專屬的 SPN，或使用者定義的字串。|**ServerSPN** 關鍵字可以在提供者、初始化或連接字串中使用，以執行下列操作：<br /><br /> -指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體用於連接的帳戶。 這會簡化 Kerberos 驗證的存取。 如果有 Kerberos 金鑰發行中心 (KDC)，而且有指定正確的帳戶，則可能使用 Kerberos 驗證而非 NTLM。 KDC 通常位於與網域控制站相同的電腦上。<br /><br /> -指定 SPN 來查閱 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的服務帳戶。 對於每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，系統會產生可用於此目的的兩個預設 SPN。 不過，系統不保證這些金鑰存在於 Active Directory 中，因此在此情況下，不保證使用 Kerberos 驗證。<br /><br /> -指定將用於查閱 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之服務帳戶的 SPN。 這可以是對應到服務帳戶的任何使用者定義字串。 在此情況下，必須在 KDC 中手動註冊金鑰，而且必須滿足使用者定義 SPN 的規則。<br /><br /> **FailoverPartnerSPN** 關鍵字可用於指定容錯移轉夥伴伺服器的 SPN。 帳戶的範圍與 Active Directory 金鑰值與您針對主體伺服器指定的值相同。|  
|ODBC 應用程式會將 SPN 指定為主體伺服器或容錯移轉夥伴伺服器的連接屬性。|連接屬性 **SQL_COPT_SS_SERVER_SPN** 可用於指定連接到主體伺服器的 SPN。<br /><br /> 連接屬性 **SQL_COPT_SS_FAILOVER_PARTNER_SPN** 可用於指定容錯移轉夥伴伺服器的 SPN。|  
|OLE DB 應用程式會將 SPN 指定為主體伺服器或容錯移轉夥伴伺服器的資料來源初始化屬性。|**SSPROP_INIT_SERVER_SPN** 屬性集中的連接屬性 **DBPROPSET_SQLSERVERDBINIT** 可用於指定連接的 SPN。<br /><br /> **SSPROP_INIT_FAILOVER_PARTNER_SPN** 中的連接屬性 **DBPROPSET_SQLSERVERDBINIT** 可用於指定容錯移轉夥伴伺服器的 SPN。|  
|使用者會在 ODBC 資料來源名稱 (DSN) 中指定伺服器或容錯移轉夥伴伺服器的 SPN。|SPN 可以在 ODBC DSN 中，透過 DSN 設定對話方塊指定。|  
|使用者會在 OLE DB 的 **[資料連結]** 或 **[登入]** 對話方塊中指定伺服器或容錯移轉夥伴伺服器的 SPN。|SPN 可以在 **[資料連結]** 或 **[登入]** 對話方塊中指定。 **[登入]** 對話方塊可以搭配 ODBC 或 OLE DB 使用。|  
|ODBC 應用程式會決定用於建立連接的驗證方法。|當連接成功開啟時，應用程式可以查詢連接屬性 **SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD** 來決定所使用的驗證方法。 這些值將包含 (但不限於) **NTLM** 和 **Kerberos**。|  
|OLE DB 應用程式會決定用於建立連接的驗證方法。|當連接成功開啟時，應用程式可以查詢 **SSPROP_AUTHENTICATION_METHOD** 屬性集中的連接屬性 **DBPROPSET_SQLSERVERDATASOURCEINFO** 來決定所使用的驗證方法。 這些值將包含 (但不限於) **NTLM** 和 **Kerberos**。|  
  
## <a name="failover"></a>容錯移轉  
 SPN 不會儲存在容錯移轉快取中，因此無法在連接之間傳遞。 在連接字串或連接屬性中指定時，SPN 將會用於主體和夥伴的所有連接嘗試。  
  
## <a name="connection-pooling"></a>連接共用  
 應用程式應該注意，在部分並非所有連接字串中指定 SPN 可能會造成集區片段。  
  
 應用程式可以用程式設計方式將 SPN 指定為連接屬性，而非指定連接字串關鍵字。 這可以協助管理連接集區片段。  
  
 應用程式應該注意，設定對應的連接屬性可以覆寫連接字串中的 SPN，但是連接共用所使用的連接字串將會因為共用用途而使用連接字串值。  
  
## <a name="down-level-server-behavior"></a>下層伺服器行為  
 新的連接行為會由用戶端實作，因此，該行為對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本而言不是專屬的。  
  
## <a name="linked-servers-and-delegation"></a>連結的伺服器與委派  
 建立連結的伺服器時，可以使用 [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 的 **@provstr** 參數來指定伺服器和容錯移轉夥伴 SPN。 此做法的優點與在用戶端連接字串中指定 SPN 相同：它是簡單且更可靠地建立使用 Kerberos 驗證的連接。  
  
 利用連結的伺服器委派需要 Kerberos 驗證。  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>應用程式指定之 SPN 的管理層面  
 選擇要在應用程式中 (透過連接字串) 指定 SPN，還是以程式設計方式，透過連接屬性 (而非依賴預設提供者產生的 SPN) 指定 SPN 時，請考慮下列因素：  
  
-   安全性：指定的 SPN 會洩漏受到保護的資訊嗎？  
  
-   可靠性：若要啟用的預設 Spn，在其中的服務帳戶使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體執行必須有足夠的權限，才能更新 KDC 上的 Active Directory。  
  
-   便利性與位置透明度：如何將應用程式的 Spn 會受到影響，如果其資料庫移到不同[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體嗎？ 如果您使用資料庫鏡像，這樣會同時套用到主體伺服器及其容錯移轉夥伴。 如果伺服器變更意指必須變更 SPN，這會如何影響應用程式？ 將會管理任何變更嗎？  
  
## <a name="specifying-the-spn"></a>指定 SPN  
 您可以在對話方塊和程式碼中指定 SPN。 本節討論如何指定 SPN。  
  
 SPN 的最大長度為 260 個字元。  
  
 SPN 在連接字串或連接屬性中所使用的語法如下所示：  
  
|語法|描述|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|使用 TCP 以外的通訊協定時，此為提供者針對預設執行個體所產生的預設 SPN。<br /><br /> *fqdn* 是完整的網域名稱。|  
|MSSQLSvc/*fqdn*:*port*|使用 TCP 時，此為提供者產生的預設 SPN。<br /><br /> *port* 是 TCP 通訊埠編號。|  
|MSSQLSvc/*fqdn*:*InstanceName*|使用 TCP 以外的通訊協定時，此為提供者針對具名執行個體所產生的預設 SPN。<br /><br /> *InstanceName* 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體名稱。|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|對應到 Windows 自動註冊之內建電腦帳戶的 SPN。|  
|*Username*@*Domain*|網域帳戶的直接規格。<br /><br /> *Username* 是 Windows 使用者帳戶名稱。<br /><br /> *Domain* 是 Windows 網域名稱或完整的網域名稱。|  
|*MachineName*$@*Domain*|電腦帳戶的直接規格。<br /><br /> (如果您所連接的伺服器是以 LOCAL SYSTEM 或 NETWORK SERVICE 帳戶執行，若要取得 Kerberos 驗證， **ServerSPN** 可以是 *MachineName*$@*Domain* 格式)。|  
|*KDCKey*/*MachineName*|使用者指定的 SPN。<br /><br /> *KDCKey* 是符合 KDC 金鑰規則的英數字串。|  
  
## <a name="odbc-and-ole-db-syntax-supporting-spns"></a>支援 SPN 的 ODBC 和 OLE DB 語法  
 如需語法專屬的資訊，請參閱下列主題：  
  
-   [服務主體名稱&#40;Spn&#41;用戶端連接中&#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [用戶端連接 &#40;OLE DB&#41; 中的服務主體名稱 &#40;SPN&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 如需有關示範這項功能之範例應用程式的詳細資訊，請參閱 [SQL Server 資料可程式性範例](https://msftdpprodsamples.codeplex.com/)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
[註冊 Kerberos 連接的服務主體名稱](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
