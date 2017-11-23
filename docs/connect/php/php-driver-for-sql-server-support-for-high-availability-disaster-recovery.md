---
title: "PHP Driver for SQL Server 高可用性、 災害復原 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a4777aa2ffac5b3932815dee65eb237337d95784
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="php-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>PHP Driver for SQL Server 對於高可用性、災害復原的支援
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的高可用性、 災害復原 （3.0 版中新增） 的支援[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。  [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 中加入 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 支援。 如需有關 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 線上叢書》。  
  
3.0 版[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，您可以指定的可用性群組接聽程式 （高可用性、 災害復原） 可用性群組 (AG) 連接屬性中的。 如果[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]應用程式連接到容錯移轉的 AlwaysOn 資料庫，則原始連接會中斷應用程式必須開啟新連接，才能在容錯移轉之後繼續工作。  
  
如果您未連接到可用性群組接聽程式，而且多個 IP 位址是主機名稱相關聯[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]會循序逐一查看所有與 DNS 項目相關聯的 IP 位址。 如果 DNS 伺服器所傳回的第一個 IP 位址未繫結至任何網路介面卡 (NIC)，這項作業可能會很費時。 當連接到可用性群組接聽程式，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]建立對所有 IP 位址的平行處理，如果某個連接嘗試連接的嘗試成功，驅動程式就會捨棄任何暫止的連接嘗試。  
  
> [!NOTE]  
> 增加連接逾時並實作連接重試邏輯可提高應用程式連接到可用性群組的機率。 此外，因為連接可能會由於可用性群組容錯移轉而失敗，所以您應該實作連接重試邏輯，並重試失敗的連接，直到重新連接為止。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接  
**MultiSubnetFailover**連接屬性表示部署應用程式的可用性群組或容錯移轉叢集執行個體以及[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]會嘗試連接到主要資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體來嘗試連接到所有 IP 位址。 當**MultiSubnetFailover = true**指定連接，用戶端重試 TCP 連接的速度比作業系統的預設 TCP 重新傳輸間隔快。 這種方式可在容錯移轉 AlwaysOn 可用性群組或 AlwaysOn 容錯移轉叢集執行個體之後更快重新連線，且同時適用於單一和多重子網路可用性群組和容錯移轉叢集執行個體。  
  
請務必指定**MultiSubnetFailover = True**連接到 SQL Server 2012 可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體時。 **MultiSubnetFailover** 對於 SQL Server 2012 中的所有可用性群組和容錯移轉叢集執行個體可促進更快的容錯移轉，並大幅縮短單一和多重子網路 AlwaysOn 拓撲的容錯移轉時間。 在多重子網路容錯移轉期間，用戶端會平行嘗試連接。 子網路容錯移轉期間[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]會積極重試 TCP 連接。  
  
如需有關中連接字串關鍵字[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，請參閱[連接選項](../../connect/php/connection-options.md)。  
  
指定**MultiSubnetFailover = true**當連接到的項目以外的可用性群組接聽程式或容錯移轉叢集執行個體可能會導致負面效能影響，並不支援。  
  
請使用下列指導方針，連接到可用性群組中的伺服器：  
  
-   如果在連接到單一子網路或多重子網路時使用 **MultiSubnetFailover** 連接屬性，則會提高兩者的效能。  
  
-   若要連接到可用性群組，在連接字串中指定可用性群組的可用性群組接聽程式做為伺服器。  
  
-   連接到設定超過 64 個 IP 位址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體會導致連接失敗。  
  
-   根據驗證的類型，使用 **MultiSubnetFailover** 連接屬性之應用程式的行為不會受到影響：[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證、Kerberos 驗證或 Windows 驗證。  
  
-   增加的值**loginTimeout**來容納容錯移轉時間並減少應用程式連接重試次數。  
  
-   不支援分散式交易。  
  
如果唯讀路由不在作用中，在下列狀況下，連接到可用性群組中的次要複本位置將會失敗：  
  
1.  如果未設定次要複本位置接受連接。  
  
2.  如果應用程式使用 **ApplicationIntent=ReadWrite**，而且已針對唯讀存取設定次要複本位置。  
  
如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 **ApplicationIntent=ReadOnly**，則連接會失敗。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>從資料庫鏡像升級到使用多子重網路叢集  
如果連接字串中有 **MultiSubnetFailover** 和 **Failover_Partner** 連接關鍵字，則會發生連接錯誤。 如果使用 **MultiSubnetFailover** 而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 傳回容錯移轉夥伴回應，指出它是資料庫鏡像配對的一部分，也會發生錯誤。  
  
如果您升級[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]目前使用資料庫鏡像的多重子網路案例的應用程式，您應該移除**Failover_Partner**連接屬性並將它取代為**MultiSubnetFailover**設**是**和可用性群組接聽程式取代連接字串中的伺服器名稱。 如果連接字串使用**Failover_Partner**和**MultiSubnetFailover = true**，驅動程式會產生錯誤。 不過，如果連接字串使用**Failover_Partner**和**MultiSubnetFailover = false** (或**ApplicationIntent = ReadWrite**)，應用程式將會使用資料庫鏡像。  
  
如果在 AG 的主要資料庫上使用資料庫鏡像，而且驅動程式會傳回錯誤**MultiSubnetFailover = true**用於連接至可用性群組而不是主要資料庫的連接字串接聽程式。  
  
## <a name="specifying-application-intent"></a>指定應用程式意圖  
當 **ApplicationIntent=ReadOnly** 時，用戶端在連接到啟用 AlwaysOn 的資料庫時會要求讀取工作負載。 伺服器會在連接時和在 USE 資料庫陳述式期間，只針對啟用 AlwaysOn 的資料庫強制執行此意圖。  
  
**ApplicationIntent** 關鍵字不適用於舊版唯讀資料庫。  
  
資料庫可以允許或不允許 AlwaysOn 目標資料庫上的讀取工作負載 (作法是使用 **PRIMARY_ROLE** 和 **SECONDARY_ROLE**[!INCLUDE[tsql](../../includes/tsql_md.md)] 陳述式的 **ALLOW_CONNECTIONS** 子句。)  
  
**ApplicationIntent** 關鍵字用於啟用唯讀路由。  
  
## <a name="read-only-routing"></a>唯讀路由  
唯讀路由是可確保資料庫的唯讀複本之可用性的功能。 若要啟用唯讀路由：  
  
1.  您必須連接到 AlwaysOn 可用性群組的可用性群組接聽程式。  
  
2.  **ApplicationIntent** 連接字串關鍵字必須設為 **ReadOnly**。  
  
3.  可用性群組必須由資料庫管理員設定為啟用唯讀路由。  
  
使用唯讀路由的多個連接可能不會連接至相同的唯讀複本。 資料庫同步處理的變更或伺服器路由組態的變更，可能會導致用戶端連接至不同的唯讀複本。 若要確保所有唯讀要求連接至相同的唯讀複本，請勿將可用性群組接聽程式傳遞給 **Server** 連接字串關鍵字。 請改為指定唯讀執行個體的名稱。  
  
唯讀路由可能比連接到主要複本的時間更長，因為唯讀路由先連接到主要複本，再尋找最佳的可讀取次要複本。 因此，您應該增加登入逾時。  
  
## <a name="see-also"></a>請參閱＜  
[連接到伺服器](../../connect/php/connecting-to-the-server.md)  
  
