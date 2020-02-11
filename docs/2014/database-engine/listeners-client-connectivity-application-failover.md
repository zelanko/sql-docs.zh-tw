---
title: 可用性群組接聽程式、用戶端連接和應用程式容錯移轉（SQL Server） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5ee2879bc0ef94d8abee20032c83a74d00696ef2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797835"
---
# <a name="availability-group-listeners-client-connectivity-and-application-failover-sql-server"></a>可用性群組接聽程式、用戶端連接及應用程式容錯移轉 (SQL Server)
  此主題包含有關 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 用戶端連接和應用程式容錯移轉功能的考量資訊。  
  
> [!NOTE]  
>  對於大多數的一般接聽程式組態，您只需要使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式或 PowerShell 指令程式，就可以建立第一個可用性群組接聽程式。 如需詳細資訊，請參閱本主題稍後的 [相關工作](#RelatedTasks)。  
  
 
  
##  <a name="AGlisteners"></a> 可用性群組接聽程式  
 您可以透過建立可用性群組接聽程式，將用戶端連接提供給給定可用性群組的資料庫。 可用性群組接聽程式是用戶端可連接的虛擬網路名稱 (VNN)，以便存取 AlwaysOn 可用性群組之主要或次要複本中的資料庫。 可用性群組接聽程式讓用戶端不需要知道用戶端所連接的 SQL Server 實體執行個體名稱，即可連接至可用性複本。  不需要修改用戶端連接字串，即可連接到目前主要複本的目前位置。  
  
 可用性群組接聽程式是由網域名稱系統 (DNS) 接聽程式名稱、接聽程式通訊埠指定和一個或多個 IP 位址所組成。 可用性群組接聽程式只支援 TCP 通訊協定。  接聽程式的 DNS 名稱在網域中和在 NetBIOS 中必須是唯一的。  當您建立新的可用性群組接聽程式時，它會成為叢集中具有相關虛擬網路名稱 (VNN)、虛擬 IP (VIP)，以及可用性群組相依性的資源。 用戶端使用 DNS 將 VNN 解析為多個 IP 位址，然後嘗試連接到每個位址，直到連接要求成功為止，或直到連接要求逾時為止。  
  
 如果一或多個[可讀取的次要複本](availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)設定為唯讀路由，主要複本的讀取意圖用戶端連接會重新導向至可讀取的次要複本。 此外，如果主要複本在某個 SQL Server 執行個體上離線，而且在另一個 SQL Server 執行個體上新的主要複本變為上線，可用性群組接聽程式會將用戶端連接到新的主要複本。  
  
 如需可用性群組接聽程式的詳細資訊，請參閱 [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
 
  
###  <a name="AGlConfig"></a> 可用性群組接聽程式組態  
 可用性群組接聽程式是由下列所定義：  
  
 唯一的 DNS 名稱  
 這也稱為虛擬網路名稱 (VNN)。 套用 DNS 主機名稱的 Active Directory 命名規則。 如需詳細資訊，請參閱 [Active Directory 中的電腦、網域、站台及 OU 的命名慣例](https://support.microsoft.com/kb/909264) 知識庫文件。  
  
 一個或多個虛擬 IP 位址 (VIP)  
 為可用性群組可容錯移轉的一個或多個目標子網路設定 VIP。  
  
 IP 位址組態  
 對於給定的可用性群組接聽程式而言，此 IP 位址會使用動態主機設定通訊協定 (DHCP) 或一個或多個靜態 IP 位址。  
  
-   動態主機設定通訊協定 (DHCP)  
  
     如果可用性群組位於單一子網路，您可以設定所有的可用性群組接聽程式 IP 位址使用 DHCP。 如果是實際執行之前的環境，DHCP 會針對不需要災害復原至另一個子網路上的遠端網站的可用性群組提供簡單設定。 但是，您不應該在實際執行環境中搭配可用性群組接聽程式使用 DHCP。 這是因為在停機時，如果 DHCP IP 租用過期，則需要額外的時間來重新註冊與接聽程式 DNS 名稱相關聯的新 DHCP IP 位址。 額外的時間將會造成用戶端連接失敗。  
  
-   靜態 IP 位址  
  
     在實際執行環境中，我們建議可用性群組接聽程式使用靜態 IP 位址。 此外，在可用性群組橫跨多重子網路網域的多個子網路時，可用性群組接聽程式必須使用靜態 IP 位址。  
  
 可用性群組接聽程式不支援混合網路組態和跨子網路的 DHCP。 這是因為當發生容錯移轉時，動態 IP 可能會過期或釋出，而威脅整體高可用性。  
  
###  <a name="SelectListenerPort"></a> 選取可用性群組接聽程式通訊埠  
 當您設定可用性群組接聽程式時，必須指定通訊埠。  您可以將預設通訊埠設定為 1433，以便提供用戶端連接字串的簡易性。 如果使用 1433，則不需要在連接字串中指定通訊埠編號。   此外，因為每個可用性群組接聽程式都有個別的虛擬網路名稱，所以單一 WSFC 上設定的每個可用性群組接聽程式都可以設定為參考相同的預設通訊埠 1433。  
  
 您也可以指定非標準接聽程式通訊埠，但這表示每當連接到可用性群組接聽程式時，您也需要在連接字串中明確指定目標通訊埠。  此外，也需要在防火牆上開啟非標準通訊埠的權限。  
  
 如果您將預設通訊埠 1433 用於可用性群組接聽程式 VNN，仍然需要確定叢集節點上沒有其他服務正在使用此通訊埠，否則會導致通訊埠衝突。  
  
 如果其中一個 SQL Server 執行個體已經透過執行個體接聽程式在 TCP 通訊埠 1433 上接聽，而且在電腦上沒有其他服務 (包括其他 SQL Server 執行個體) 正在通訊埠 1433 上接聽，就不會導致與可用性群組接聽程式通訊埠相衝突。  這是因為可用性群組接聽程式可在同一個服務處理序內共用相同的 TCP 通訊埠。  但是不應該將多個 SQL Server (並存) 執行個體設定為在相同通訊埠上接聽。  
  
##  <a name="ConnectToPrimary"></a> 使用接聽程式連接到主要複本  
 若要使用可用性群組接聽程式，連接到主要複本進行讀寫存取，連接字串要指定可用性群組接聽程式 DNS 名稱。  如果可用性群組主要複本變更為新複本，使用可用性群組接聽程式網路名稱的現有連接會中斷連接。  然後對可用性群組接聽程式的新連接會被導向至新的主要複本。 ADO.NET 提供者 (System.Data.SqlClient) 的基本連接字串範例如下：  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;IntegratedSecurity=SSPI  
```  
  
 您仍然可以選擇直接參考主要或次要複本的 SQL Server 執行個體名稱，而不使用可用性群組接聽程式名稱，不過如果選擇這樣做，便無法享有新連接自動導向至目前主要複本的好處。  此外，也無法享有唯讀路由的好處。  
  
##  <a name="ConnectToSecondary"></a> 使用接聽程式連接到唯讀次要複本 (唯讀路由)  
 「唯讀路由」  是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的功能，可將對可用性群組接聽程式的內送連接路由至設為允許唯讀工作負載的次要複本。 只有在下列條件成立時，參考可用性群組接聽程式名稱的內送連接才會自動路由至唯讀複本：  
  
-   至少一個次要複本設定為唯讀存取，而且每個唯讀次要複本和主要複本都設定為支援唯讀路由。 如需詳細資訊，請參閱本節稍後的 [若要將可用性複本設定為唯讀路由](#ConfigureARsForROR)。  
  
-   連接字串參考可用性群組接聽程式，而且內送連接的應用程式意圖設定為唯讀，例如，透過在 ODBC 或 OLEDB 連接字串或連接屬性 (attribute) 或屬性 (property) 中使用 **Application Intent=ReadOnly** 關鍵字。 如需詳細資訊，請參閱本節稍後的 [唯讀應用程式意圖和唯讀路由](#ReadOnlyAppIntent)。  
  
###  <a name="ConfigureARsForROR"></a> 若要將可用性複本設定為唯讀路由  
 資料庫管理員必須設定可用性複本，如下所示：  
  
1.  針對每個要設定為可讀取次要複本的可用性複本，資料庫管理員必須設定下列設定 (只在次要角色之下才有效)：  
  
    -   連接存取權必須設定為 [全部] 或 [唯讀]。  
  
    -   必須指定唯讀路由 URL。  
  
2.  對於每個這些複本，必須為主要角色指定唯讀路由清單。 指定一個或多個伺服器名稱做為路由目標。  
  
####  <a name="RelatedTasksROR"></a> 相關工作  
  
-   [設定可用性複本的唯讀存取 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [設定可用性群組的唯讀路由 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
###  <a name="ReadOnlyAppIntent"></a> 唯讀應用程式意圖和唯讀路由  
 應用程式意圖連接字串屬性表示用戶端應用程式要導向至讀寫或唯讀可用性群組資料庫版本的要求。 若要使用唯讀路由，在連接到可用性群組接聽程式時，用戶端必須使用連接字串中設為唯讀的應用程式意圖。 如果沒有唯讀的應用程式意圖，可用性群組接聽程式的連接會被導向至主要複本的資料庫。  
  
 應用程式意圖屬性在登入期間是儲存在用戶端的工作階段，然後 SQL Server 會處理此意圖，並依據可用性群組的設定和次要複本中目標資料庫的目前讀寫狀態，決定要執行的動作。  
  
 指定唯讀應用程式意圖之 ADO.NET 提供者 (System.Data.SqlClient) 的連接字串範例如下：  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly  
```  
  
 在這個連接字串範例中，用戶端嘗試連接到通訊埠 1433 (如果可用性群組接聽程式是在 1433 上接聽，也可以省略此通訊埠編號) 上名為 `AGListener` 的可用性群組接聽程式。  連接字串將`ApplicationIntent`屬性設定為`ReadOnly`，使其成為*讀取意圖的連接字串*。  如果沒有此設定，伺服器就不會嘗試唯讀路由連接。  
  
 可用性群組的主要資料庫會處理內送唯讀路由要求，並嘗試找出已聯結至主要複本並設定為唯讀路由的線上唯讀複本。  用戶端會從主要複本伺服器接收連接資訊，並連接到已識別的唯讀複本。  
  
 請注意，應用程式意圖可從用戶端驅動程式傳送至舊版 SQL Server 執行個體。  在此情況下，會忽略唯讀應用程式意圖，而且連接照常進行。  
  
 您可以透過下列方式略過唯讀路由：不將應用程式意圖連接屬性設為 `ReadOnly` (若未指定，登入期間預設值為 `ReadWrite`)，或者直接連接到主要複本的 SQL Server 執行個體，而不使用可用性群組接聽程式名稱。  如果您直接連接到唯讀複本，也不會發生唯讀路由。  
  
####  <a name="RelatedTasksApps"></a> 相關工作  
  
-   [高可用性/災害復原的 SQL Server Native Client 支援](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [搭配 SQL Server Native Client 使用連接字串關鍵字](../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> 略過可用性群組接聽程式  
 雖然可用性群組接聽程式支援容錯移轉重新導向和唯讀路由，但用戶端連接不一定要使用它們。 用戶端連接也可以直接參考 SQL Server 執行個體，而不連接到可用性群組接聽程式。  
  
 對 SQL Server 執行個體來說，登入連接是使用可用性群組接聽程式還是使用另一個執行個體端點，並沒有關係。  SQL Server 執行個體會確認目標資料庫的狀態，並依據可用性群組的組態和執行個體上資料庫的目前狀態，允許或不允許連接。  例如，如果用戶端應用程式直接連接到 SQL Server 執行個體的通訊埠，連接到裝載於可用性群組的目標資料庫，而且目標資料庫處於主要狀態並已上線，連接就會成功。  如果目標資料庫處於離線狀態或處於轉換狀態，資料庫連接就會失敗。  
  
 另外，從資料庫鏡像移轉至 [!INCLUDE[ssHADR](../includes/sshadr-md.md)]時，只要僅一個次要複本存在且不允許使用者連接，應用程式就可以指定資料庫鏡像連接字串。 如需詳細資訊，請參閱本節稍後的 [資料庫鏡像連接字串與可用性群組搭配使用](#DbmConnectionString)。  
  
###  <a name="DbmConnectionString"></a> 資料庫鏡像連接字串與可用性群組搭配使用  
 如果可用性群組只擁有一個次要複本，而且未設定為允許以唯讀方式存取次要複本，則用戶端可以透過使用資料庫鏡像連接字串連接到主要複本。 從資料庫鏡像將現有的應用程式移轉到可用性群組時，這種方法會很實用，前提是您要將可用性群組限制為只能有兩個可用性複本 (一個主要複本和一個次要複本)。 如果您加入其他次要複本，您需要為可用性群組建立可用性群組接聽程式，並更新您的應用程式使用可用性群組接聽程式 DNS 名稱。  
  
 當使用資料庫鏡像連接字串時，用戶端可以使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 或 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 用戶端提供的連接字串至少必須提供一個伺服器執行個體名稱，也就是 *「初始夥伴名稱」* ，以識別一開始裝載您打算連接之可用性複本的伺服器執行個體。 此連接字串也可以選擇性地提供另一個伺服器執行個體的名稱，也就是 *「容錯移轉夥伴名稱」* (Failover Partner Name)，以識別一開始將次要複本裝載為容錯移轉夥伴名稱的伺服器執行個體。  
  
 如需資料庫鏡像連接字串的詳細資訊，請參閱 [將用戶端連接至資料庫鏡像工作階段 &#40;SQL Server&#41;](database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)。  
  
##  <a name="CCBehaviorOnFailover"></a> 容錯移轉時用戶端連接的行為  
 當可用性群組發生容錯移轉時，對可用性群組的現有持續連線會終止，而且用戶端必須建立新連接，才能繼續使用相同的主要資料庫或唯讀次要資料庫。  在伺服器端發生容錯移轉時，對可用性群組的連接可能會失敗，而強制用戶端連接重試連接，直到主要資料庫恢復上線為止。  
  
 如果在用戶端應用程式嘗試連線期間，但在連線逾時之前，可用性群組恢復上線，用戶端驅動程式在其中一個內部重試期間可能會成功連線，而應用程式在此情況下不會發生錯誤。  
  
##  <a name="SupportAgMultiSubnetFailover"></a> 支援可用性群組多重子網路容錯移轉  
 若所用的用戶端程式庫可以在連接字串中使用 MultiSubnetFailover 連線選項，即可根據所使用之提供者的語法，將 MultiSubnetFailover 設定為 "True" 或 "Yes"，來最佳化可用性群組容錯移轉至不同的子網路。  
  
> [!NOTE]  
>  對於可用性群組接聽程式以及 SQL Server 容錯移轉叢集執行名稱的單一和多重子網路連接，建議使用此設定。  啟用此選項會增加額外的最佳化，甚至在單一子網路案例也一樣。  
  
 
  `MultiSubnetFailover` 連接選項只適用於 TCP 網路通訊協定，而且只在連接到可用性群組接聽程式時以及任何虛擬網路名稱連接到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 時才受支援。  
  
 可啟用多重子網路容錯移轉之 ADO.NET 提供者 (System.Data.SqlClient) 的連接字串範例如下：  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI; MultiSubnetFailover=True  
```  
  
 
  `MultiSubnetFailover` 連接選項應該設為 `True`，即使可用性群組只跨越單一子網路也一樣。  這可讓您將新用戶端預先設定為支援子網路的未來跨越，而不需要在未來變更用戶端連接字串，此外也會最佳化單一子網路容錯移轉的容錯移轉效能。  雖然 `MultiSubnetFailover` 連接選項不是必要，但是它提供更快子網路容錯移轉的好處。  這是因為用戶端驅動程式會嘗試對與可用性群組平行相關的每個 IP 位址開啟 TCP 通訊端。  用戶端驅動程式會等候第一個成功回應的 IP，一旦回應，就會將它用於連接。  
  
##  <a name="SSLcertificates"></a> 可用性群組接聽程式和 SSL 憑證  
 連接到可用性群組接聽程式時，如果參與的 SQL Server 執行個體同時使用 SSL 憑證和工作階段加密，連接的用戶端驅動程式需要支援 SSL 憑證中的主體替代名稱，才能強制加密。  我們已計劃針對 ADO.NET (SqlClient)、Microsoft JDBC 和 SQL Native Client (SNAC)，提供 SQL Server 驅動程式對憑證主體替代名稱的支援。  
  
 您必須針對容錯移轉叢集中的每個參與伺服器節點來設定 X.509 憑證，並在憑證的主體替代名稱中設定所有可用性群組接聽程式的清單。  
  
 例如，如果 WSFC 有三個可用性群組接聽程式，名為 `AG1_listener.Adventure-Works.com`、 `AG2_listener.Adventure-Works.com`和 `AG3_listener.Adventure-Works.com`，憑證的主體替代名稱設定應如下：  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> 可用性群組接聽程式和伺服器主體名稱 (SPN)  
 網域管理員必須在 Active Directory 中設定每個可用性群組接聽程式名稱的伺服器主體名稱 (SPN)，以便針對可用性群組接聽程式的用戶端連接啟用 Kerberos。 註冊 SPN 時，您必須使用裝載可用性複本之伺服器執行個體的服務帳戶。  若要讓 SPN 在所有複本上運作，相同服務帳戶必須用於裝載可用性群組之 WSFC 叢集的所有執行個體。  
  
 您可以使用 `setspn` Windows 命令列工具來設定 SPN。  例如，若要設定 SPN 用於 `AG1listener.Adventure-Works.com` 可用性群組，而此可用性群組裝載於一組都設為使用 `corp/svclogin2`網域帳戶的 SQL Server 執行個體：  
  
```cmd
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 如需有關為 SQL Server 手動註冊 SPN 的詳細資訊，請參閱＜ [註冊 Kerberos 連接的服務主體名稱](configure-windows/register-a-service-principal-name-for-kerberos-connections.md)＞。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [AlwaysOn 用戶端連線性 &#40;SQL Server&#41;](availability-groups/windows/always-on-client-connectivity-sql-server.md)
  
-   [建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [檢視可用性群組接聽程式屬性 &#40;SQL Server&#41;](availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [移除可用性群組接聽程式 &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [設定可用性複本的唯讀存取 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [設定可用性群組的唯讀路由 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相關內容  
  
-   [Microsoft SQL Server AlwaysOn 高可用性和災害復原方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [可用性群組](https://blogs.msdn.com/b/sqlalwayson/archive/2012/01/16/introduction-to-the-availability-group-listener.aspx)接聽程式簡介（SQL Server AlwaysOn 小組的 blog）  
  
-   [SQL Server AlwaysOn 小組 Blog：官方 SQL Server AlwaysOn 小組的 Blog](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 用戶端連線性 &#40;SQL Server&#41;](availability-groups/windows/always-on-client-connectivity-sql-server.md)  
 [關於可用性複本的用戶端連線存取 &#40;SQL Server&#41;](availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [使用中次要：可讀取的次要複本 &#40;AlwaysOn 可用性群組&#41;](availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [將用戶端連接至資料庫鏡像工作階段 &#40;SQL Server&#41;](database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)
