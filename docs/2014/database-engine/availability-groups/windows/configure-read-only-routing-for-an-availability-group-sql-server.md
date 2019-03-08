---
title: 設定可用性群組的唯讀路由 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a129386b5c88939d68f5d7f23a5fe2b4d8ce7cca
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579118"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>設定可用性群組的唯讀路由 (SQL Server)
  若要在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中將 AlwaysOn 可用性群組設定為支援唯讀路由，可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell。 *「唯讀路由」*(Read-Only Routing) 是指 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將合格的唯讀連接要求路由至可用之 AlwaysOn [可讀取的次要複本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) (亦即在以次要角色執行時，設定為允許唯讀工作負載的複本) 的功能。 若要支援唯讀路由，可用性群組必須具有[可用性群組接聽程式](../../listeners-client-connectivity-application-failover.md)。 唯讀用戶端必須將其連接要求導向至此接聽程式，且用戶端的連接字串必須將應用程式的意圖指定為「唯讀」。 換句話說必須是「讀取意圖的連接要求」。  
  
> [!NOTE]
>  如需如何設定可讀取之次要複本的相關資訊，請參閱 [設定可用性複本上的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)。  
> 
> 
> 
> [!NOTE]
>  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]不支援設定唯讀路由。  
  

  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   可用性群組必須擁有可用性群組接聽程式。 如需詳細資訊，請參閱 [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)。  
  
-   一或多個可用性複本必須設定為接受次要角色的唯讀 (也就是要[可讀取次要複本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn %20Availability %20groups\).md))。 如需詳細資訊，請參閱 [設定可用性複本上的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
-   您必須連接到裝載目前主要複本的伺服器執行個體。  
  
###  <a name="RORReplicaProperties"></a> 您必須設定哪些複本屬性，才能支援唯讀路由？  
  
-   每一個要支援唯讀路由之可讀取的次要複本，皆必須指定 *「唯讀路由 URL」*(Read-Only Routing URL)。 只有在本機複本以次要角色執行時，此 URL 才會生效。 如有必要，您必須各自指定每個複本的唯讀路由 URL。 每個唯讀路由 URL 可用於將讀取意圖的連接要求路由至特定可讀取的次要複本。 一般而言，每個可讀取的次要複本都有一個指派的唯讀路由 URL。  
  
     如需計算可用性複本之唯讀路由 URL 的相關資訊，請參閱[計算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)。  
  
-   如果要支援唯讀路由的可用性複本為主要複本時，則必須指定 *「唯讀路由清單」*(Read-Only Routing List)。 只有本機複本以主要角色執行時，給定的唯讀路由清單才會生效。 如有必要，您必須各自指定每個複本的這份清單。 一般而言，每份唯讀路由清單皆會包含每一個唯讀路由 URL，並在清單結尾提供本機複本的 URL。  
  
    > [!NOTE]  
    >  讀取意圖的連接要求會路由至目前之主要複本的唯讀路由清單上，第一個可用之可讀取的次要複本。 沒有負載平衡。  
  
> [!NOTE]  
>  如需可用性群組接聽程式的相關資訊，以及唯讀路由的詳細資訊，請參閱 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
  
|工作|Permissions|  
|----------|-----------------|  
|若要在建立可用性群組時設定複本|需要 **系統管理員 (sysadmin)** 固定伺服器角色的成員資格，以及 CREATE AVAILABILITY GROUP 伺服器權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
|若要修改可用性複本|需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要設定唯讀路由**  
  
> [!NOTE]  
>  如需程式碼範例，請參閱本節稍後的 [範例 (Transact-SQL)](#TsqlExample)。  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  如果您要針對新的可用性群組指定複本，請使用 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式。 如果您要加入或修改現有可用性群組的複本，請使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式。  
  
    -   若要設定次要角色的唯讀路由，請在 ADD REPLICA 或 MODIFY REPLICA WITH 子句中指定 SECONDARY_ROLE 選項，如下所示：  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://*`system-address`*:*`port`*')**  
  
         唯讀路由 URL 的參數如下：  
  
         *system-address*  
         這是明確識別目的地電腦系統的字串，例如系統名稱、完整網域名稱或 IP 位址。  
  
         *port*  
         這是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體之 Database Engine 所使用的通訊埠編號。  
  
         例如：   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         在 MODIFY REPLICA 子句中，ALLOW_CONNECTIONS 是選擇性的 (如果複本已經設定為允許唯讀連接的話)。  
  
         如需詳細資訊，請參閱 [計算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)。  
  
    -   若要設定主要角色的唯讀路由，請在 ADD REPLICA 或 MODIFY REPLICA WITH 子句中指定 PRIMARY_ROLE 選項，如下所示：  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **=('*`server`*'** [ **,**...*n* ] **))**  
  
         其中， *server* 會識別裝載可用性群組中唯讀次要複本的伺服器執行個體。  
  
         例如：   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  您必須先設定唯讀路由 URL，然後再設定唯讀路由清單。  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 下列範例會將現有可用性群組 `AG1` 的兩個可用性複本修改成支援唯讀路由 (如果其中一個複本目前擁有主要角色的話)。 為了識別裝載可用性複本的伺服器執行個體，此範例會指定執行個體名稱：`COMPUTER01` 和 `COMPUTER02`。  
  
```  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO  
  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要設定唯讀路由**  
  
> [!NOTE]  
>  如需程式碼範例，請參閱本節稍後的 [範例 (PowerShell)](#PSExample)。  
  
1.  將預設值 (`cd`) 設定為裝載主要複本的伺服器執行個體。  
  
2.  將可用性複本加入至可用性群組時，請使用 `New-SqlAvailabilityReplica` 指令程式。 修改現有的可用性複本時，請使用 `Set-SqlAvailabilityReplica` 指令程式。 相關參數如下所示：  
  
    -   若要設定次要角色的唯讀路由，請指定**ReadonlyRoutingConnectionUrl"*`url`*"** 參數。  
  
         其中， *url* 是路由至複本進行唯讀連接時要使用的連接性完整網域名稱 (FQDN) 和通訊埠。 例如：  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         如需詳細資訊，請參閱 [計算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)。  
  
    -   若要設定主要角色的連接存取，請指定**ReadonlyRoutingList"*`server`*」** [ **，**...*n* ]，其中*server*識別裝載可用性群組中的唯讀次要複本的伺服器執行個體。 例如：  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  您必須先設定複本的唯讀路由 URL，然後再設定其唯讀路由清單。  
  
    > [!NOTE]  
    >  若要檢視指令程式的語法，請在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 環境中使用 `Get-Help` 指令程式。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
###  <a name="PSExample"></a> 範例 (PowerShell)  
 下列範例會將可用性群組中的主要複本和一個次要複本設定為唯讀路由。 首先，此範例會將唯讀路由 URL 指派給每個複本。 然後，它會設定主要複本的唯讀路由清單。 在連接字串中設定 "ReadOnly" 屬性的連接將會重新導向至次要複本。 如果這個次要複本無法讀取 (由 `ConnectionModeInSecondaryRole` 設定決定)，連接將會導向回到主要複本。  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> 後續操作：設定唯讀路由之後  
 一旦目前的主要複本和可讀取的次要複本都設定為支援兩種角色的唯讀路由之後，可讀取的次要複本就可以從經由可用性群組接聽程式連接的用戶端接收讀取意圖連接要求。  
  
> [!TIP]  
>  使用時[bcp 公用程式](../../../tools/bcp-utility.md)或是[sqlcmd 公用程式](../../../tools/sqlcmd-utility.md)，您可以指定唯讀存取任何已啟用的次要複本進行唯讀存取，藉由指定`-K ReadOnly`切換。  
  
###  <a name="ConnStringReqsRecs"></a> 用戶端連接字串的需求和建議  
 若要讓用戶端應用程式使用唯讀路由，其連接字串必須滿足下列需求：  
  
-   使用 TCP 通訊協定。  
  
-   將應用程式意圖屬性 (Attribute)/屬性 (Property) 設定成唯讀。  
  
-   參考設定為支援唯讀路由之可用性群組的接聽程式。  
  
-   參考該可用性群組中的資料庫。  
  
 此外，我們建議連接字串要啟用多重子網路容錯移轉，以便針對每個子網路上的每個複本支援平行用戶端執行緒。 這樣做可在容錯移轉之後盡量縮短用戶端重新連接時間。  
  
 連接字串的語法主要取決於應用程式所使用的 SQL Server 提供者。 下列 .NET Framework Data Provider 4.0.2 for SQL Server 範例連接字串說明了針對唯讀路由運作時必要且建議的連接字串部分。  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 如需唯讀應用程式意圖和唯讀路由的詳細資訊，請參閱 [可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)。  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>如果唯讀路由未正確運作  
 如需針對唯讀路由組態進行疑難排解的相關資訊，請參閱 [唯讀路由未正確運作](troubleshoot-always-on-availability-groups-configuration-sql-server.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要檢視唯讀路由組態**  
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) (**read_only_routing_url** 資料行)  
  
 **若要設定用戶端連接存取**  
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [設定可用性複本的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
 **若要在應用程式中使用連接字串**  
  
-   [高可用性/災害復原的 SQL Server Native Client 支援](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   **部落格：**  
  
     [計算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程師部落格](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮書：**  
  
     [Microsoft 的 SQL Server 2012 白皮書](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客戶諮詢團隊白皮書](http://sqlcat.com/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用中次要：可讀取次要複本 （AlwaysOn 可用性群組）](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [關於可用性複本的用戶端連線存取 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [可用性群組接聽程式、用戶端連線及應用程式容錯移轉 &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
  
  
