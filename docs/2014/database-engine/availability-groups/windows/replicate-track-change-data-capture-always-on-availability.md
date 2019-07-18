---
title: 複寫、 變更追蹤、 異動資料擷取和 AlwaysOn 可用性群組 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server], AlwaysOn Availability Groups
- change data capture [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: e17a9ca9-dd96-4f84-a85d-60f590da96ad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c52283ce9d512da6dc2e5ad05a4c8356524bef01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814054"
---
# <a name="replication-change-tracking-change-data-capture-and-alwayson-availability-groups-sql-server"></a>複寫、變更追蹤、變更資料擷取和 AlwaysOn 可用性群組 (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]支援複寫、異動資料擷取 (CDC) 和變更追蹤 (CT)。 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 有助於提供高可用性以及其他資料庫復原功能。  
  
 
  
##  <a name="Overview"></a> AlwaysOn 可用性群組的複寫概觀  
  
###  <a name="PublisherRedirect"></a> 發行者重新導向  
 當發行的資料庫能夠感知 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]時，提供發行資料庫之代理程式存取權的散發者就會使用 redirected_publishers 項目來設定。 這些項目會重新導向原本設定的發行者/資料庫配對，並利用可用性群組接聽程式名稱來連接到發行者和發行資料庫。 透過可用性群組接聽程式名稱所建立的連接將會在容錯移轉時失敗。 在容錯移轉之後，當複寫代理程式重新啟動時，連接將自動重新導向至新的主要複本。  
  
 在 AlwaysOn 可用性群組中，次要資料庫不能是發行者。 當複寫與 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]結合時，不支援重新發行。  
  
 如果發行的資料庫是可用性群組的成員，而且發行者已重新導向，它就必須重新導向至與可用性群組相關聯的可用性群組接聽程式名稱。 它可能不會重新導向至明確節點。  
  
> [!NOTE]  
>  在容錯移轉到次要複本之後，複寫監視器就無法調整 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行執行個體的名稱，而且會繼續在原始主要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體名稱之下顯示複寫資訊。 在容錯移轉之後，便無法使用複寫監視器輸入追蹤 Token，但是可以在複寫監視器中看到在新的發行者端使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]輸入的追蹤 Token。  
  
###  <a name="Changes"></a> 支援 AlwaysOn 可用性群組之複寫代理程式的一般變更  
 三個複寫代理程式已修改成支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 記錄讀取器、快照集和合併代理程式已修改成查詢重新導向發行者的散發資料庫，並且使用傳回的可用性群組接聽程式名稱來連接到資料庫發行者 (如果已宣告重新導向發行者的話)。  
  
 根據預設，當代理程式查詢散發者以判斷原始發行者是否已重新導向時，會驗證重新導向目前目標的適用性，然後才將重新導向的主機傳回至代理程式。 這是建議的行為。 不過，如果代理程式啟動太頻繁，與驗證預存程序相關的負擔成本可能太高。 新命令列參數 *BypassPublisherValidation*已加入至記錄讀取器、快照集和合併代理程式。 使用此參數時，重新導向的主機會立即傳回至代理程式，而略過驗證預存程序的執行。  
  
 從驗證預存程序傳回的失敗會記錄在代理程式記錄檔中。 嚴重性大於或等於 16 的這些錯誤會導致代理程式終止。 某些重試功能已內建到代理程式，以處理在容錯移轉至新主要複本時預期的已發行資料庫中斷連接。  
  
#### <a name="log-reader-agent-modifications"></a>記錄讀取器代理程式修改  
 記錄讀取器代理程式有下列變更。  
  
-   **複寫的資料庫一致性**  
  
     當發行的資料庫是 AlwaysOn 可用性群組的成員時，記錄讀取器預設不會處理所有可用性群組次要複本上尚未強行寫入的記錄檔記錄。 這樣可確保容錯移轉時，所有複寫至訂閱者的資料列也會存在新的主要複本上。  
  
     當發行者只有兩個 AlwaysOn 可用性複本 (一個主要和一個次要) 且發生容錯移轉時，原始的主要複本會保持離線，因為在所有次要資料庫恢復連線或發生錯誤的次要複本從可用性群組中移除之前，Logreader 不會向前移動。 現在針對次要資料庫執行的 Logreader 將不會繼續前進，因為 AlwaysOn 無法強行對任何次要資料庫進行任何變更。 若要讓 Logreader 繼續前進並且仍然擁有災害復原的能力，請使用 ALTER AVAILABITY GROUP <group_name> REMOVE REPLICA 從可用性群組中移除原始主要複本。 然後將新的次要複本加入至可用性群組。  
  
-   **追蹤旗標 1448**  
  
     追蹤旗標 1448 可讓複寫記錄讀取器向前移動，即使非同步次要複本尚未認可收到變更也一樣。 即使這個追蹤旗標已啟用，記錄讀取器一定會等候同步次要複本。 記錄讀取器不會超過同步次要複本的最小認可。 這個追蹤旗標會套用至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體，而不只套用至可用性群組、可用性資料庫或記錄讀取器執行個體。 這個追蹤旗標會立即生效，不必重新啟動。 您可以事先或在非同步次要複本失敗時啟動它。  
  
###  <a name="StoredProcs"></a> 支援 AlwaysOn 的預存程序  
  
-   **sp_redirect_publisher**  
  
     預存程序 **sp_redirect_publisher** 可用來指定現有發行者/資料庫配對的重新導向發行者。 如果發行者資料庫屬於可用性群組，重新導向發行者就是可用性群組接聽程式名稱。  
  
-   **sp_get_redirected_publisher**  
  
     預存程序 **sp_get_redirected_publisher** 可由複寫代理程式用來查詢散發者，以便判斷發行者/資料庫配對是否具有定義的重新導向發行者。 此預存程序有兩種目的。 首先，它可讓代理程式判斷原始發行者是否已經重新導向。 其次，它也可以在散發者端起始驗證預存程序 (**sp_validate_redirected_publisher**)，以便驗證重新導向的目標節點是否適合作為具名資料庫的發行者。  
  
     若要執行此預存程序，呼叫端必須是 **系統管理員** 伺服器角色的成員、散發資料庫的 **db_owner** 資料庫角色，或是與發行者資料庫相關聯之定義發行集的 **發行集存取清單** 的成員。  
  
-   **sp_validate_redirected_publisher**  
  
     此預存程序會嘗試驗證目前的發行者是否能夠裝載發行的資料庫。 您可以隨時呼叫此預存程序，以便確認發行之資料庫的目前主機是否能夠支援複寫。  
  
-   **sp_validate_replicate_hosts_as_publishers**  
  
     雖然讓代理程式確保目前主要複本能夠當做發行者資料庫的複寫發行者運作已經很有用，不過還是需要一項更全面的驗證功能，才能確立 AlwaysOn 可用性資料庫上整個複寫拓撲的有效性。 預存程序 **sp_validate_replica_hosts_as_publishers** 就是為了滿足這項需求所設計。  
  
     此預存程序一律以手動方式執行。 呼叫端必須是散發者端的系統管理員 ( **sysadmin** )、散發資料庫的 **dbowner** 或是發行者資料庫中發行集之 **發行集存取清單** 的成員。 此外，對於所有可用性複本主機而言，呼叫端的登入必須是有效的登入，而且擁有與發行者資料庫相關聯之可用性資料庫的選取權限。  
  
###  <a name="CDC"></a> 異動資料擷取  
 啟用異動資料擷取 (CDC) 的資料庫能夠運用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ，以便確保資料庫在發生失敗時維持可用狀態，而且資料庫資料表的變更會繼續受到監視並且儲放在 CDC 變更資料表中。 設定 CDC 和 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的順序並不重要。 啟用 CDC 的資料庫可以加入至 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，而且可以啟用本身為 AlwaysOn 可用性群組成員之資料庫的 CDC。 不過，在這兩種情況下，CDC 組態一律在目前或預期的主要複本上執行。 CDC 會使用記錄讀取器代理程式，而且其限制與本主題稍早的＜ **記錄讀取器代理程式修改** ＞一節中所述的限制相同。  
  
-   **在有異動資料擷取但沒有複寫的情況下，收集變更**  
  
     如果資料庫啟用了 CDC，但是沒有啟用複寫，用來從記錄中收集變更並將變更儲放在 CDC 變更資料表中的擷取處理序就會在 CDC 主機上當做它自己的 SQL 代理程式作業執行。  
  
     若要在容錯移轉之後繼續收集變更，您必須在新的主要複本上執行預存程序 **sp_cdc_add_job** ，以便建立本機擷取作業。  
  
     下列範例會建立擷取作業。  
  
    ```  
    EXEC sys.sp_cdc_add_job @job_type = 'capture';  
    ```  
  
-   **在有異動資料擷取且有複寫的情況下，收集變更**  
  
     如果同時啟用了資料庫的 CDC 和複寫，記錄讀取器就會處理 CDC 變更資料表的母體擴展。 在此情況中，複寫用來運用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的技術將可確保系統在容錯移轉之後繼續從記錄中收集變更並儲放在 CDC 變更資料表中。 在此組態中，不需要為 CDC 執行其他動作，以確保變更資料表會擴展。  
  
-   **異動資料擷取清除**  
  
     為了確保新的主要資料庫會進行適當的清除，一定要建立本機清除作業。 下列範例會建立清除作業。  
  
    ```  
    EXEC sys.sp_cdc_add_job @job_type = 'cleanup';  
    ```  
  
    > [!NOTE]  
    >  您應該在容錯移轉前於所有可能的容錯移轉目標上建立這些作業，並且將它們標示為停用，直到主機上的可用性複本變成新的主要複本為止。 當本機資料庫變成次要資料庫時，在舊主要資料庫上執行的 CDC 作業也應該停用。 若要停用和啟用作業，請使用 [sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) 的 *@enabled* 選項。 如需有關建立 CDC 作業的詳細資訊，請參閱 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql)支援複寫、異動資料擷取 (CDC) 和變更追蹤 (CT)。  
  
-   **將 CDC 角色加入 AlwaysOn 主要資料庫複本**  
  
     當資料表啟用 CDC 時，有可能將資料庫角色與擷取執行個體建立關聯。 如果指定了角色，希望使用 CDC 資料表值函式來存取資料表變更的使用者必須不只有追蹤資料表資料行的選取存取權，也必須是具名角色的成員。 如果指定的角色尚未存在，則會建立角色。 當資料庫角色自動加入至 AlwaysOn 主要資料庫時，這些角色也會傳播至可用性群組的次要資料庫。  
  
-   **存取 CDC 變更資料的用戶端應用程式和 AlwaysOn**  
  
     使用資料表值函式 (TVF) 或連結的伺服器存取變更資料表資料的用戶端應用程式，也需要在容錯移轉後找出適當 CDC 主機的功能。 可用性群組接聽程式名稱是 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 所提供的機制，這項機制會以透明的方式允許連接以不同主機為新目標。 一旦可用性群組接聽程式名稱與可用性群組產生關聯之後，它就可用於 TCP 連接字串中。 透過可用性群組接聽程式名稱支援兩個不同的連接案例。  
  
    -   一個確保連接要求一律導向至目前的主要複本。  
  
    -   一個確保連接要求會導向至唯讀的次要複本。  
  
     如果用來找出唯讀的次要複本，還必須為可用性群組定義唯讀的路由清單。 如需可讀取次要複本之路由存取的詳細資訊，請參閱本節稍後的 [若要將可用性複本設定為唯讀路由](../../listeners-client-connectivity-application-failover.md#ConfigureARsForROR)。  
  
    > [!NOTE]  
    >  建立可用性群組接聽程式名稱以及用戶端應用程式用它來存取可用性群組資料庫複本時，都會發生一些相關聯的傳播延遲。  
  
     請使用下列查詢來判斷是否已針對裝載 CDC 資料庫的可用性群組定義了可用性群組接聽程式名稱。 如果已建立可用性群組接聽程式名稱，查詢會傳回它。  
  
    ```  
    SELECT dns_name   
    FROM sys.availability_group_listeners AS l  
    INNER JOIN sys.availability_databases_cluster AS d  
        ON l.group_id = d.group_id  
    WHERE d.database_name = N'MyCDCDB';  
    ```  
  
-   **將查詢負載重新導向至可讀取次要複本**  
  
     雖然在許多情況下用戶端應用程式一定會要連接到目前的主要複本，但這不是利用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的唯一方法。 如果可用性群組設定為支援可讀取的次要複本，則也可以從次要節點收集變更資料。  
  
     已設定可用性群組時，與 SECONDARY_ROLE 關聯的 ALLOW_CONNECTIONS 屬性會用來指定支援的次要存取類型。 如果設定為 ALL，則會允許次要的所有連接，但只有需要唯讀存取的連接會成功。 如果設定為 READ_ONLY，則需要在建立次要資料庫的連接時指定唯讀意圖，連接才會成功。 如需詳細資訊，請參閱[設定可用性複本上的唯讀存取 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
     您可以使用下列查詢，以判斷是否需要唯讀意圖以連接到可讀取次要複本。  
  
    ```  
    SELECT g.name AS AG, replica_server_name, secondary_role_allow_connections_desc  
    FROM sys.availability_replicas AS r  
    JOIN sys.availability_groups AS g  
        ON r.group_id = g.group_id  
    WHERE g.name = N'MY_AG_NAME;  
    ```  
  
     可用性群組接聽程式名稱或明確節點名稱都可用於找出次要複本。 如果使用可用性群組接聽程式名稱，則存取會導向至任何合適的次要複本。  
  
     當`sp_addlinkedserver`用來建立連結的伺服器，以存取次要複本時， *@datasrc* 參數會用於可用性群組接聽程式名稱或明確伺服器名稱，而 *@provstr* 參數用來指定唯讀意圖。  
  
    ```  
    EXEC sp_addlinkedserver   
    @server = N'linked_svr',   
    @srvproduct=N'SqlServer',  
    @provider=N'SQLNCLI11',   
    @datasrc=N'AG_Listener_Name',   
    @provstr=N'ApplicationIntent=ReadOnly',   
    @catalog=N'MY_DB_NAME';  
    ```  
  
-   **CDC 變更資料的用戶端存取和網域登入**  
  
     一般而言，若要讓用戶端存取位於 AlwaysOn 可用性群組之成員資料庫的變更資料，您應該使用網域登入。 為確保在容錯移轉後持續存取變更資料，網域使用者需要所有支援可用性群組複本之主機的存取權限。 如果將資料庫使用者加入至主要複本的資料庫，而此使用者已與網域登入相關聯，則此資料庫使用者會傳播至次要資料庫並繼續與指定的網域登入相關聯。 如果新資料庫使用者與 SQL Server 驗證登入相關聯，則次要資料庫的使用者會傳播但沒有登入。 雖然相關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證登入可用來存取原本定義資料庫使用者所在之主要資料庫的變更資料，但該節點是唯一可存取的節點。 此 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證登入無法存取任何次要資料庫的資料，也無法存取資料庫使用者定義所在之原始資料庫以外的任何新主要資料庫的資料。  
  
###  <a name="CT"></a> 變更追蹤  
 啟用變更追蹤 (CT) 的資料庫可以屬於 AlwaysOn 可用性群組的一部分。 不需要進行其他組態設定。 使用 CDC 資料表值函式 (TVF) 存取變更資料表資料的變更追蹤用戶端應用程式，需要在容錯移轉後找出主要複本的功能。 如果用戶端應用程式透過可用性群組接聽程式名稱進行連接，連接要求一律會適當導向至目前的主要複本。  
  
> [!NOTE]  
>  變更追蹤資料必須一律從主要複本取得。 嘗試存取次要複本的變更資料會導致下列錯誤：  
>   
>  訊息 22117，層級 16，狀態 1，行 1  
>   
>  次要複本的成員資料庫 (即次要資料庫) 不支援變更追蹤。 請在主要複本的資料庫上執行變更追蹤查詢。  
  
##  <a name="Prereqs"></a> 使用複寫的必要條件、限制和考量  
 本節描述使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]來部署複寫的考量，包括必要條件、限制和建議。  
  
### <a name="prerequisites"></a>先決條件  
  
-   當使用異動複寫，而且發行集資料庫是在可用性群組時，發行者和散發者都必須至少執行 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。 訂閱者可以使用較低層級的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
-   當使用合併式複寫，而且發行集資料庫是在可用性群組時：  
  
    -   推入的訂用帳戶：「 發行者 」 和 「 散發者 」 必須至少執行[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。  
  
    -   提取訂閱：發行者、 散發者 」 和 「 訂閱者 」 資料庫必須至少在[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]。 這是因為訂閱者的合併代理程式必須知道可用性群組如何容錯移轉到次要複本。  
  
-   不支援將散發資料庫放置到可用性群組上。  
  
-   發行者執行個體必須滿足參與 AlwaysOn 可用性群組所需的所有必要條件。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組的必要條件、限制和建議 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。  
  
### <a name="restrictions"></a>限制  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]所支援的複寫組合：  
  
|||||  
|-|-|-|-|  
||**發行者**|**散發者** <sup>3</sup>|**訂閱者**|  
|**異動**|是<sup>1</sup>|否|是<sup>2</sup>|  
|**P2P**|否|否|否|  
|**合併式**|是|否|是<sup>2</sup>|  
|**快照式**|是|否|是<sup>2</sup>|  
  
 <sup>1</sup>不包含雙向和相互異動複寫的支援。  
  
 <sup>2</sup>容錯移轉至複本資料庫是手動程序。 沒有提供自動容錯移轉。  
  
 <sup>3</sup>散發者資料庫不支援搭配[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]或資料庫鏡像。  
  
### <a name="considerations"></a>考量  
  
-   散發資料庫不支援搭配 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 或資料庫鏡像使用。 複寫組態會結合至設定散發者所在的 SQL Server 執行個體。因此，無法鏡像或複寫散發資料庫。 若要針對散發者提供高可用性，請使用 SQL Server 容錯移轉叢集。 如需詳細資訊，請參閱 [AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)。  
  
-   雖然支援訂閱者容錯移轉至次要資料庫，不過這是相當複雜的手動程序。 此程序基本上與用來容錯移轉鏡像訂閱者資料庫的方法完全相同。 訂閱者必須執行 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 或更新版本，才能參與可用性群組。  
  
-   存在於資料庫之外的中繼資料和物件不會傳播到次要複本，包括登入、作業、連結的伺服器。 如果您需要在容錯移轉後使用新主要資料庫上的中繼資料和物件，則必須手動加以複製。 如需詳細資訊，請參閱 [管理可用性群組之資料庫的登入及工作 &#40;SQL Server&#41;](../../logins-and-jobs-for-availability-group-databases.md)(Failover) 的程序中通常可以互換。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **複寫**  
  
-   [設定 AlwaysOn 可用性群組 (SQL Server) 的複寫](always-on-availability-groups-sql-server.md)  
  
-   [維護 AlwaysOn 發行集資料庫&#40;SQL Server&#41;](maintaining-an-always-on-publication-database-sql-server.md)  
  
-   [複寫管理常見問題集](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
 **Change data capture**  
  
-   [啟用和停用異動資料擷取 &#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)  
  
-   [管理和監視異動資料擷取 &#40;SQL Server&#41;](../../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
-   [使用異動資料 &#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
 **Change tracking**  
  
-   [啟用和停用變更追蹤 &#40;SQL Server&#41;](../../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)  
  
-   [管理變更追蹤 &#40;SQL Server&#41;](../../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
-   [使用變更追蹤 &#40;SQL Server&#41;](../../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [複寫訂閱者及 AlwaysOn 可用性群組&#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)   
 [必要條件、 限制和建議，AlwaysOn 可用性群組的&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性群組：互通性 (SQL Server)](always-on-availability-groups-interoperability-sql-server.md) [AlwaysOn 容錯移轉叢集執行個體 (SQL Server)](../../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)   
 [關於異動資料擷取 &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [關於變更追蹤 &#40;SQL Server&#41;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [SQL Server 複寫](../../../relational-databases/replication/sql-server-replication.md)   
 [追蹤資料變更 &#40;SQL Server&#41;](../../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql)  
  
  
