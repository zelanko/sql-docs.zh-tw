---
title: "JDBC 驅動程式支援的高可用性、 災害復原 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 27b51025180a1c9a2463c49401589ab459e7ecaf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>JDBC 驅動程式對於高可用性、災害復原的支援
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主題討論[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援高可用性、 災害復原[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。 如需有關 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的詳細資訊，請參閱《 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 線上叢書》。  
  
 在 4.0 版開始[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，您可以指定的可用性群組接聽程式 （高可用性、 災害復原） 可用性群組 (AG) 連接屬性中的。 如果[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]應用程式連接到容錯移轉的 AlwaysOn 資料庫，則原始連接會中斷應用程式必須開啟新連接，才能在容錯移轉之後繼續工作。 下列[連接屬性](../../connect/jdbc/setting-the-connection-properties.md)中已加入[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
指定 multiSubnetFailover = true，連接到可用性群組或容錯移轉叢集執行個體的可用性群組接聽程式時。 請注意， **multiSubnetFailover**預設為 false。 使用**applicationIntent**宣告的應用程式工作負載類型。 請參閱下列各節以取得詳細資料。
 
從 Microsoft JDBC Driver 6.0 版的 SQL Server，新的連接屬性**則 transparentNetworkIPResolution** (TNIR) 加入透明連接到 Alwayson 可用性群組或有伺服器相關聯的多個 IP 位址。 當**則 transparentNetworkIPResolution**為 true，此驅動程式會嘗試連接到第一個可用的 IP 位址。 如果第一次嘗試失敗，驅動程式會嘗試連接到所有 IP 位址，以平行方式，直到逾時過期，當其中一個成功捨棄任何暫止的連接嘗試。   

請注意：
* 則 transparentNetworkIPResolution 預設為 true
* 如果 multiSubnetFailover 為 true，則會忽略則 transparentNetworkIPResolution
* 如果使用資料庫鏡像，則會忽略則 transparentNetworkIPResolution
* 如果有超過 64 個 IP 位址，則會忽略則 transparentNetworkIPResolution
* 則 transparentNetworkIPResolution 為 true，當第一次連接嘗試就會使用 500 毫秒的逾時值。 其餘的連接嘗試遵循相同的邏輯與 multiSubnetFailover 功能。 

> [!NOTE]  
如果您是使用 Microsoft JDBC Driver 4.2 （或較低） for SQL Server，而且**multiSubnetFailover**為 false，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]嘗試連線到第一個 IP 位址。 如果[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]無法建立連線，以第一個 IP 位址，則連接會失敗。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不會嘗試連接到與伺服器相關聯的任何後續 IP 位址。 

  
> [!NOTE]  
>  增加連接逾時並實作連接重試邏輯可提高應用程式連接到可用性群組的機率。 此外，因為連接可能會由於可用性群組容錯移轉而失敗，所以您應該實作連接重試邏輯，並重試失敗的連接，直到重新連接為止。  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接  
 請務必指定**multiSubnetFailover = true**連接到可用性群組接聽程式時[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]可用性群組或[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]容錯移轉叢集執行個體。 **multiSubnetFailover**啟用更快速的容錯移轉的所有可用性群組和容錯移轉叢集執行個體中的[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]並大幅縮短單一和多重子網路 AlwaysOn 拓撲的容錯移轉時間。 在多重子網路容錯移轉期間，用戶端會平行嘗試連接。 子網路容錯移轉期間[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]會積極重試 TCP 連接。  
  
 **MultiSubnetFailover**連接屬性表示部署應用程式的可用性群組或容錯移轉叢集執行個體以及[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]會嘗試連接到主要資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體來嘗試連接到所有 IP 位址。 當**MultiSubnetFailover = true**指定連接，用戶端重試 TCP 連接的速度比作業系統的預設 TCP 重新傳輸間隔快。 這種方式可在容錯移轉 AlwaysOn 可用性群組或 AlwaysOn 容錯移轉叢集執行個體之後更快重新連線，且同時適用於單一和多重子網路可用性群組和容錯移轉叢集執行個體。  
  
 如需有關中連接字串關鍵字[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 指定**multiSubnetFailover = true**當連接到的項目以外的可用性群組接聽程式或容錯移轉叢集執行個體可能會導致負面效能影響，並不支援。  
  
 如果未安裝安全性管理員，則 Java Virtual Machine 會在一段有限期間快取虛擬 IP 位址 (VIP)，這在預設情況下是由您的 JDK 實作以及 Java 屬性 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 所定義。 如果已安裝 JDK 安全性管理員，則 Java Virtual Machine 將會快取 VIP，而且預設不會重新整理快取。 您應該針對 Java Virtual Machine 快取將「存留時間」(networkaddress.cache.ttl) 設定為一天。 如果您未將預設值變更為一天 (或一天左右)，則當加入或更新 VIP 時，將不會從 Java Virtual Machine 快取中清除舊的值。 如需有關 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 的詳細資訊，請參閱[http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)。  
  
 請使用下列指導方針，連接到可用性群組或容錯移轉叢集執行個體中的伺服器：  
  
-   如果驅動程式會產生錯誤**instanceName**連接屬性用在相同的連接字串中**multiSubnetFailover**連接屬性。 這反映以下事實：可用性群組中並未使用 SQL Browser。 不過，如果**portNumber**也指定連接屬性，則驅動程式將會忽略**instanceName**並用**portNumber**。  
  
-   使用**multiSubnetFailover**連接屬性連接到單一子網路或多重子網路時，則會提高兩者的效能。  
  
-   若要連接到可用性群組，在連接字串中指定可用性群組的可用性群組接聽程式做為伺服器。 例如，jdbc:sqlserver://VNN1。  
  
-   連接到設定超過 64 個 IP 位址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體會導致連接失敗。  
  
-   使用的應用程式的行為**multiSubnetFailover**連接屬性不會影響基礎的驗證類型：[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]驗證、 Kerberos 驗證或 Windows 驗證。  
  
-   增加的值**loginTimeout**來容納容錯移轉時間並減少應用程式連接重試次數。  
  
-   不支援分散式交易。  
  
 如果唯讀路由不在作用中，在下列狀況下，連接到可用性群組中的次要複本位置將會失敗：  
  
1.  如果未設定次要複本位置接受連接。  
  
2.  如果應用程式使用**applicationIntent = ReadWrite** （討論如下） 和次要複本位置設定為唯讀存取。  
  
 如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 **ApplicationIntent=ReadOnly**，則連接會失敗。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>從資料庫鏡像升級到使用多子重網路叢集  
 如果您升級[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]目前使用資料庫鏡像的多重子網路案例的應用程式，您應該移除**failoverPartner**連接屬性並將它取代為**multiSubnetFailover**設**true** ，並以可用性群組接聽程式取代連接字串中的伺服器名稱。 如果連接字串使用**failoverPartner**和**multiSubnetFailover = true**，驅動程式會產生錯誤。 不過，如果連接字串使用**failoverPartner**和**multiSubnetFailover = false** (或**ApplicationIntent = ReadWrite**)，應用程式將會使用資料庫鏡像。  
  
 如果在 AG 的主要資料庫上使用資料庫鏡像，而且驅動程式會傳回錯誤**multiSubnetFailover = true**用於連接至可用性群組而不是主要資料庫的連接字串接聽程式。  
  
## <a name="specifying-application-intent"></a>指定應用程式意圖  
 當**applicationIntent = ReadOnly**，用戶端會連線到啟用 AlwaysOn 的資料庫時要求唯讀工作負載。 伺服器會在連接時及 USE 資料庫陳述式期間強制施行此意圖，但是只限於啟用 AlwaysOn 的資料庫。  
  
 **ApplicationIntent**關鍵字不適用於舊版唯讀資料庫。  
  
 資料庫可以允許或不允許 AlwaysOn 目標資料庫上的讀取工作負載 (作法是使用 **PRIMARY_ROLE** 和 **SECONDARY_ROLE**[!INCLUDE[tsql](../../includes/tsql_md.md)] 陳述式的 **ALLOW_CONNECTIONS** 子句。)  
  
 **ApplicationIntent**關鍵字用於啟用唯讀路由。  
  
## <a name="read-only-routing"></a>唯讀路由  
 唯讀路由功能可確保資料庫之唯讀複本的可用性。 若要啟用唯讀路由：  
  
1.  您必須連接到 AlwaysOn 可用性群組的可用性群組接聽程式。  
  
2.  **ApplicationIntent**連接字串關鍵字必須設為**ReadOnly**。  
  
3.  可用性群組必須由資料庫管理員設定為啟用唯讀路由。  
  
 使用唯讀路由的多個連接可能不會連接至相同的唯讀複本。 資料庫同步處理的變更或伺服器路由組態的變更，可能會導致用戶端連接至不同的唯讀複本。 若要確保所有唯讀要求連接至相同的唯讀複本，請勿將傳遞的可用性群組接聽程式或虛擬 IP 位址來**serverName**連接字串關鍵字。 請改為指定唯讀執行個體的名稱。  
  
 唯讀路由所花的時間可能會比連接到主要複本所花的時間更長，因為唯讀路由會先連接到主要複本，然後尋找最佳可用的可讀次要複本。 因此，您應該增加登入逾時。  
  
## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>支援 multiSubnetFailover 和 applicationIntent 的新方法  
 以下方法讓您以程式設計方式存取**multiSubnetFailover**， **applicationIntent**和**則 transparentNetworkIPResolution**連接字串關鍵字：  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 **GetMultiSubnetFailover**， **setMultiSubnetFailover**， **getApplicationIntent**， **setApplicationIntent**， **getTransparentNetworkIPResolution**和**setTransparentNetworkIPResolution**方法也會新增至[SQLServerDataSource 類別](../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource 類別](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，和[SQLServerXADataSource 類別](../../connect/jdbc/reference/sqlserverxadatasource-class.md)。  
  
## <a name="ssl-certificate-validation"></a>SSL 憑證驗證  
 可用性群組是由多個實體伺服器所組成。 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]新增支援**主體替代名稱**讓多個主機可以與相同的憑證相關聯的 SSL 憑證中。 如需有關 SSL 的詳細資訊，請參閱[了解 SSL 支援](../../connect/jdbc/understanding-ssl-support.md)。  
  
## <a name="see-also"></a>另請參閱  
 [連接到 SQL Server JDBC 驅動程式](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)  
  
  

