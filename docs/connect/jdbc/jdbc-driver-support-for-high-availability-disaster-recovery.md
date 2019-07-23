---
title: 高可用性與災害復原的 JDBC 驅動程式支援 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 322a22c2236898876ae2fd5e942a1ad3617c1959
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956387"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>JDBC 驅動程式對於高可用性、災害復原的支援
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主題討論 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 對於高可用性、災害復原的支援 -- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。 如需有關 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的詳細資訊，請參閱《 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 線上叢書》。  
  
 從 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 版開始，您可以在連線屬性中指定 (高可用性、災害復原) 可用性群組 (AG) 的可用性群組接聽程式。 如果 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 應用程式連線到容錯移轉的 AlwaysOn 資料庫，原始連線會中斷，應用程式必須開啟新的連線，才能在容錯移轉後繼續工作。 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 中已新增下列[連線屬性](../../connect/jdbc/setting-the-connection-properties.md)：  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
在連線到可用性群組的可用性群組接聽程式或容錯移轉叢集執行個體時，指定 multiSubnetFailover=true。 請注意, **multiSubnetFailover**預設為 false。 使用**applicationIntent**來宣告應用程式工作負載類型。 如需詳細資訊, 請參閱下列各節。
 
從適用于 SQL Server 的 Microsoft JDBC Driver 版本6.0 開始, 會加入新的連線屬性**transparentNetworkIPResolution** (TNIR), 以透明連線到 Always On 可用性群組或具有多個 IP 位址的伺服器與. 當**transparentNetworkIPResolution**為 true 時, 驅動程式會嘗試連接到第一個可用的 IP 位址。 如果第一次嘗試失敗, 驅動程式會嘗試以平行方式連接到所有 IP 位址, 直到超時時間到期為止, 當其中一個作業成功時, 就會捨棄任何暫止的連接嘗試。   

請注意:
* transparentNetworkIPResolution 預設為 true
* 如果 multiSubnetFailover 為 true, 則會忽略 transparentNetworkIPResolution
* 如果使用資料庫鏡像, 則會忽略 transparentNetworkIPResolution
* 如果有超過64個 IP 位址, 則會忽略 transparentNetworkIPResolution
* 當 transparentNetworkIPResolution 為 true 時, 第一次連接嘗試會使用500毫秒的超時值。 其餘的連接嘗試會遵循與 multiSubnetFailover 功能相同的邏輯。 

> [!NOTE]
> 如果您使用 Microsoft JDBC Driver 4.2 (或更低版本) 進行 SQL Server, 而且如果**multiSubnetFailover**為 false [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] , 則會嘗試連接到第一個 IP 位址。 如果 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 無法建立與第一個 IP 位址的連線，則連線會失敗。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 將不會嘗試連線到與伺服器建立關聯的任何後續 IP 位址。 
> 
> 
> [!NOTE]
>  增加連接逾時並實作連接重試邏輯可提高應用程式連接到可用性群組的機率。 此外，因為連接可能會由於可用性群組容錯移轉而失敗，所以您應該實作連接重試邏輯，並重試失敗的連接，直到重新連接為止。  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接  
 在連線到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 容錯移轉叢集執行個體時，一律指定 **multiSubnetFailover=true**。 對於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中的所有可用性群組和容錯移轉叢集執行個體，**multiSubnetFailover** 可促進更快的容錯移轉，並大幅縮短單一和多重子網路 AlwaysOn 拓撲的容錯移轉時間。 在多重子網路容錯移轉期間，用戶端會平行嘗試連接。 在子網路容錯移轉期間，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會積極重試 TCP 連線。  
  
 **multiSubnetFailover** 連線屬性表示正在可用性群組或容錯移轉叢集執行個體中部署應用程式，而且 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會嘗試連線到所有 IP 位址，以嘗試連線到主要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的資料庫。 為連線指定 **MultiSubnetFailover=true** 時，用戶端會以比作業系統預設 TCP 重新傳輸間隔更快的速度，重試 TCP 連線嘗試。 這種方式可在容錯移轉 AlwaysOn 可用性群組或 AlwaysOn 容錯移轉叢集執行個體之後更快重新連線，且同時適用於單一和多重子網路可用性群組和容錯移轉叢集執行個體。  
  
 如需中[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]連接字串關鍵字的詳細資訊, 請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 當連線到可用性群組接聽程式或容錯移轉叢集執行個體以外的某個項目時，指定 **multiSubnetFailover=true** 會導致降低效能，所以不支援此方式。  
  
 如果未安裝安全性管理員，則 Java Virtual Machine 會在一段有限期間快取虛擬 IP 位址 (VIP)，這在預設情況下是由您的 JDK 實作以及 Java 屬性 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 所定義。 如果已安裝 JDK 安全性管理員，則 Java Virtual Machine 將會快取 VIP，而且預設不會重新整理快取。 您應該針對 Java Virtual Machine 快取將「存留時間」(networkaddress.cache.ttl) 設定為一天。 如果您未將預設值變更為一天 (或一天左右)，則當新增或更新 VIP 時，將不會從「JAVA 虛擬機器」快取中清除舊的值。 如需 networkaddress.cache.ttl 和 networkaddress.cache.ttl 的詳細資訊, 請參閱[https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html](https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)。  
  
 請使用下列指導方針，連接到可用性群組或容錯移轉叢集執行個體中的伺服器：  
  
-   如果**instanceName**連接屬性是在與**multiSubnetFailover**連接屬性相同的連接字串中使用, 驅動程式將會產生錯誤。 這反映以下事實：可用性群組中並未使用 SQL Browser。 不過, 如果也指定了**portNumber**連接屬性, 驅動程式將會忽略**InstanceName**並使用**portNumber**。  
  
-   如果在連線到單一子網路或多重子網路時使用 **multiSubnetFailover** 連線屬性，則會提高兩者的效能。  
  
-   若要連接到可用性群組，在連接字串中指定可用性群組的可用性群組接聽程式做為伺服器。 例如，jdbc:sqlserver://VNN1。  
  
-   連接到設定超過 64 個 IP 位址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會導致連接失敗。  
  
-   根據驗證的類型，使用 **multiSubnetFailover** 連線屬性的應用程式其行為不會受到影響：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證、Kerberos 驗證或 Windows 驗證。  
  
-   提高 **loginTimeout** 的值來配合容錯移轉時間，並減少應用程式連線重試次數。  
  
-   不支援分散式交易。  
  
 如果唯讀路由不在作用中，在下列狀況下，連接到可用性群組中的次要複本位置將會失敗：  
  
1.  如果未設定次要複本位置接受連接。  
  
2.  如果應用程式使用 **applicationIntent=ReadWrite**，而且已針對唯讀存取設定次要複本位置。  
  
 如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 **ApplicationIntent=ReadOnly**，則連接會失敗。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>從資料庫鏡像升級到使用多子重網路叢集  
 如果您將目前使用資料庫鏡像的 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 應用程式升級為多重子網路案例，則應移除 **failoverPartner** 連線屬性，並取代成設定為 **true** 的 **multiSubnetFailover**，然後將連接字串中的伺服器名稱取代為可用性群組接聽程式。 如果連接字串使用 **failoverPartner** 和 **multiSubnetFailover=true**，驅動程式會產生錯誤。 不過，如果連接字串使用 **failoverPartner** 和 **multiSubnetFailover=false** (或 **ApplicationIntent=ReadWrite**)，應用程式會使用資料庫鏡像。  
  
 如果在可用性群組中的主要資料庫上使用資料庫鏡像，而且如果在連線到主要資料庫 (而不是可用性群組接聽程式) 的連接字串中使用 **multiSubnetFailover=true**，驅動程式會傳回錯誤。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>支援 multiSubnetFailover 和 applicationIntent 的新方法  
 下列方法可讓您以程式設計方式存取**multiSubnetFailover**、 **applicationIntent**和**transparentNetworkIPResolution**連接字串關鍵字:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 **GetMultiSubnetFailover**、 **setMultiSubnetFailover**、 **getApplicationIntent**、 **setApplicationIntent**、 **getTransparentNetworkIPResolution**和**setTransparentNetworkIPResolution**方法為也會新增至[SQLServerDataSource 類別](../../connect/jdbc/reference/sqlserverdatasource-class.md)、 [SQLServerConnectionPoolDataSource 類別](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)和[SQLServerXADataSource 類別](../../connect/jdbc/reference/sqlserverxadatasource-class.md)。  
  
## <a name="ssl-certificate-validation"></a>SSL 憑證驗證  
 可用性群組是由多個實體伺服器所組成。 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 已在 SSL 憑證中新增 **Subject Alternate Name** 的支援，好讓多個主機可以與相同憑證建立關聯。 如需 SSL 的詳細資訊, 請參閱[瞭解 Ssl 支援](../../connect/jdbc/understanding-ssl-support.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 JDBC 驅動程式連線到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
