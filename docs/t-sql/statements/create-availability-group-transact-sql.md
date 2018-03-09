---
title: "建立可用性群組 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e0a4792974ec9aa78678aec74dc390e992471e64
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟用了 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 功能，則會建立新的可用性群組。  
  
> [!IMPORTANT]  
>  在您預定要做為新可用性群組的初始主要複本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行 CREATE AVAILABILITY GROUP。 這個伺服器執行個體必須位於 Windows Server 容錯移轉叢集 (WSFC) 節點。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```SQL  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER ‘dns_name’ ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL | EXTERNAL }  
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE } ]  
     } )  
     | SESSION_TIMEOUT = integer  
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’    
  
  <ip_address_option> ::=  
     {   
        ‘four_part_ipv4_address’, ‘four_part_ipv4_mask’  
      | ‘ipv6_address’  
     }  
  
```  
  
## <a name="arguments"></a>引數  
 *group_name*  
 指定新的可用性群組名稱。 *group_name*必須是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][識別碼](../../relational-databases/databases/database-identifiers.md)，而且它必須是唯一的 WSFC 叢集中的所有可用性群組。 可用性群組名稱的最大長度為 128 個字元。  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {主要 |SECONDARY_ONLY |次要 |無}  
 指定在選擇要在何處執行備份時，有關備份作業應該如何評估主要複本的喜好設定。 您可以編寫給定備份作業，將自動備份喜好設定納入考量。 請務必了解，喜好設定並不是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 強制施行，所以它對於隨選備份沒有任何影響。  
  
 支援的值如下所示：  
  
 PRIMARY  
 指定備份一定要在主要複本上進行。 如果當您在次要複本上執行備份時，需要不支援的備份功能 (例如建立差異備份)，這個選項會很實用。  
  
> [!IMPORTANT]  
>  如果您計畫要使用記錄傳送來準備可用性群組的任何次要資料庫，請將自動備份喜好設定設為 [主要]，直到所有次要資料庫都已經準備完成並且聯結至可用性群組為止。  
  
 SECONDARY_ONLY  
 指定絕對不能在主要複本上執行備份。 如果主要複本是唯一的線上複本，不應該進行備份。  
  
 SECONDARY  
 指定應該在次要複本上進行備份，但是主要複本是唯一線上複本的情況例外。 在此情況下，應該在主要複本上進行備份。 這是預設行為。  
  
 無  
 指定當您選擇要執行備份的複本時，您希望備份作業忽略可用性複本的角色。 請注意，備份作業可能會評估其他因素，例如每個可用性複本的備份優先權，搭配其操作狀態和連接狀態。  
  
> [!IMPORTANT]  
>  不會強制執行 AUTOMATED_BACKUP_PREFERENCE 設定。 這個喜好設定的解譯取決於您在給定可用性群組之資料庫的備份作業中所編寫的邏輯 (如果有的話)。 自動備份喜好設定對於特定備份沒有任何影響。 如需詳細資訊，請參閱[設定可用性複本 &#40; 上的備份SQL Server &#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md).  
  
> [!NOTE]  
>  若要檢視現有的可用性群組的自動備份喜好設定，請選取**automated_backup_preference**或**automated_backup_preference_desc**資料行[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目錄檢視。 此外， [sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)可用來判斷慣用的備份複本。  此函數會傳回至少一個複本，1，即使`AUTOMATED_BACKUP_PREFERENCE = NONE`。  
  
 FAILURE_CONDITION_LEVEL **=** { 1 | 2 | **3** | 4 | 5 }  
 指定何種失敗條件觸發這個可用性群組自動容錯移轉。 FAILURE_CONDITION_LEVEL 群組層級設定，但卻設定成同步認可可用性模式的可用性複本上才相關 (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT)。 此外，失敗狀況可以觸發自動容錯移轉只有當主要和次要複本設定成自動容錯移轉模式 (FAILOVER_MODE  **=** 自動)，而且次要複本是目前與主要複本同步處理。  
  
 失敗狀況層級 (1–5) 的範圍從最低限制 (層級 1) 到最高限制 (層級 5)。 給定的狀況層級包含所有較少限制的層級。 因此，最嚴格的狀況層級 5 包含四個較少限制的狀況層級 (1-4)，層級 4 則包含層級 1-3，依此類推。 下表描述與每個層級對應的失敗狀況。  
  
|Level|失敗狀況|  
|-----------|-----------------------|  
|1|指定在發生以下任何情況時應該起始自動容錯移轉：<br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務已關閉。<br /><br /> -由於伺服器執行個體不收到任何通知用於連接到 WSFC 叢集的可用性群組租用已到期。 如需詳細資訊，請參閱 [How It Works: SQL Server Always On Lease Timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx)(運作方式：SQL Server AlwaysOn 租用逾時)。|  
|2|指定在發生以下任何情況時應該起始自動容錯移轉：<br /><br /> -執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會連線到叢集且超過可用性群組的使用者指定 HEALTH_CHECK_TIMEOUT 臨界值時。<br /><br /> -可用性複本處於失敗狀態。|  
|3|指定應該在嚴重 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部錯誤發生時起始自動容錯移轉，例如執行緒同步鎖定遭到遺棄、嚴重的寫入存取違規或是傾印過多。<br /><br /> 這是預設行為。|  
|4|指定應該在發生中度 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部錯誤時起始自動容錯移轉，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部資源集區中持續的記憶體不足狀況。|  
|5|指定應該在發生任何符合的失敗狀況時起始自動容錯移轉，這些狀況包括：<br /><br /> -SQL 引擎工作者執行緒已耗盡。<br /><br /> -無法解決的死結偵測。|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體對用戶端要求缺少回應與可用性群組無關。  
  
 FAILURE_CONDITION_LEVEL 和 HEALTH_CHECK_TIMEOUT 值會定義*彈性容錯移轉原則*特定群組。 這個具彈性的容錯移轉原則讓您能夠更精確控制哪些條件必須造成自動容錯移轉。 如需詳細資訊，請參閱[彈性的容錯移轉原則，自動容錯移轉的可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *（毫秒)*  
 指定等候時間 （以毫秒為單位） 的[sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系統預存程序在 WSFC 叢集假設伺服器執行個體很慢或無回應之前，傳回伺服器健全狀況資訊。 HEALTH_CHECK_TIMEOUT 群組層級設定，但卻設定為具有自動容錯移轉的同步認可可用性模式的可用性複本上才相關 (AVAILIBILITY_MODE  **=** 同步_COMMIT)。  此外，健全狀況檢查逾時可以觸發自動容錯移轉只有當主要和次要複本設定成自動容錯移轉模式 (FAILOVER_MODE  **=** 自動) 與次要資料庫複本目前與主要複本 synchronized。  
  
 預設 HEALTH_CHECK_TIMEOUT 值為 30000 毫秒 (30 秒)。 最小值為 15000 毫秒 (15 秒)，最大值為 4294967295 毫秒。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 不會在資料庫層級執行健全狀況檢查。  
  
 DB_FAILOVER  **=**  {ON |OFF}  
 指定要採取的主要複本上資料庫離線時的回應。 可用性群組中資料庫的任何狀態不是 ONLINE 設定為 ON 時，會觸發自動容錯移轉。 當這個選項設為 OFF 時的執行個體的健全狀況用來觸發自動容錯移轉。  
  
  如需有關這項設定的詳細資訊，請參閱[資料庫層級健全狀況偵測選項](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 
  
 DTC_SUPPORT  **=**  {PER_DB |無}  
 指定是否透過分散式的交易協調器 (DTC) 支援跨資料庫交易。 從開始才支援跨資料庫交易[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 PER_DB 建立可用性群組，可以支援這些交易。 如需詳細資訊，請參閱[資料庫鏡像或 AlwaysOn 可用性群組不支援跨資料庫交易 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)。  
  
 BASIC  
 用來建立基本可用性群組。 基本可用性群組僅限於一個資料庫和兩個複本： 一個主要複本和一個次要複本。 這個選項會取代已被取代的資料庫鏡像 SQL Server Standard Edition 上的功能。 如需詳細資訊，請參閱[基本可用性群組 &#40;Always On 可用性群組 &#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md). 基本可用性群組支援從[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。  

 DISTRIBUTED  
 用來建立分散式的可用性群組。 此選項搭配 AVAILABILITY GROUP ON 參數用於連接兩個不同的 Windows Server 容錯移轉叢集的可用性群組。  如需詳細資訊，請參閱[分散式可用性群組 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)。 分散式的可用性群組支援從[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 2017 中導入。 用來設定主要認可交易之前認可所需的同步次要複本的最小數目。 可保證 SQL Server 交易等候直到更新次要複本的最小數目上的交易記錄檔。 預設值為 0 可讓 SQL Server 2016 相同的行為。 最小值為 0。 最大值是減 1 的複本數目。 此選項與在同步認可模式下的複本。 當複本在同步認可模式，主要複本上的寫入等候同步次要複本上的寫入會認可到複本資料庫的交易記錄檔。 如果裝載次要複本的 SQL Server 停止回應，裝載主要複本的 SQL Server 會標示該次要複本未同步處理，並繼續進行。 沒有回應的資料庫回到線上時它處於 「 未同步處理 」 狀態，並將複本標示為狀況不良，直到主要可讓您同步一次。 此設定可確保主要複本會等候直到複本的最小數目已認可的每個交易。 如果無法使用之複本的最小數目主要的認可失敗。 叢集類型`EXTERNAL`可用性群組新增到叢集資源時，變更設定。 請參閱[的可用性群組組態的高可用性與資料保護](../../linux/sql-server-linux-availability-group-ha.md)。

 CLUSTER_TYPE  
 SQL Server 2017 中導入。 用來識別可用性群組是否在 Windows Server 容錯移轉叢集 (WSFC)。  設定至 WSFC 可用性群組容錯移轉叢集執行個體的 Windows Server 容錯移轉叢集時。 叢集由不像 Linux Pacemaker Windows Server 容錯移轉叢集的叢集管理員所管理時設為外部。 當可用性群組不使用 WSFC 叢集一起使用時，將會設定為 NONE。 例如，當可用性群組包含 Linux 伺服器與任何叢集管理員。 

 DATABASE *database_name*  
 指定本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (也就是建立可用性群組的伺服器執行個體) 上一個或多個使用者資料庫的清單。 您可以為可用性群組指定多個資料庫，但每個資料庫只能屬於一個可用性群組。 如需可用性群組可支援的資料庫類型資訊，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). 若要了解哪些本機資料庫已屬於可用性群組，請參閱**replica_id**中的資料行[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。  
  
 DATABASE 子句是選擇性的。 如果您省略它，新的可用性群組是空的。  
  
 建立可用性群組之後，連接到裝載次要複本的每個伺服器執行個體然後準備每一個次要資料庫並將它聯結至可用性群組。 如需詳細資訊，請參閱 [於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
> [!NOTE]  
>  之後，您可以在裝載目前主要複本的伺服器執行個體上，將適合的資料庫加入至可用性群組。 您也可以從可用性群組中移除資料庫。 如需詳細資訊，請參閱 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)中的 PowerShell，將次要複本加入現有的 AlwaysOn 可用性群組中。  
  
 REPLICA ON  
 指定要在新的可用性群組中裝載可用性複本的 SQL 伺服器執行個體 (一個到五個)。  每個複本是由後面接著 WITH (…) 子句的伺服器執行個體位址所指定。 您至少必須指定您的本機伺服器執行個體，而成為初始主要複本。 您最多也可以選擇指定四個次要複本。  
  
 您必須將每個次要複本聯結至可用性群組。 如需詳細資訊，請參閱 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)中的 PowerShell，將次要複本加入現有的 AlwaysOn 可用性群組中。  
  
> [!NOTE]  
>  如果您指定少於四個次要複本，當您建立可用性群組時，您可以新增額外的次要複本在任何時候使用[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。 您也可以使用這個陳述式，從現有的可用性群組移除任何次要複本。  
  
 \<臨界點 > 指定的執行個體的位址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也就是針對複本主機。 此位址格式取決於執行個體為預設執行個體還是具名執行個體，以及它是獨立的執行個體還是容錯移轉叢集執行個體 (FCI)，如下所示：  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 這個位址的元件如下所示：  
  
 *system_name*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目標執行個體所在之電腦系統的 NetBIOS 名稱。 這部電腦必須是 WSFC 節點。  
  
 *FCI_network_name*  
 這是用來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的網路名稱。 如果伺服器執行個體當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉夥伴來參與，則使用它。 執行 SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)在 FCI 上伺服器執行個體傳回它的完整 '*FCI_network_name*[\\*instance_name*]' 字串 (即完整複本名稱）。  
  
 *instance_name*  
 是的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所裝載*系統名稱*或*FCI_network_name*且具有 HADR 服務已啟用。 如果是預設伺服器執行個體，*instance_name* 為選擇性。 執行個體名稱不區分大小寫。 在獨立伺服器執行個體，這個值名稱等同於所執行 SELECT 傳回的值[@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)。  
  
 \  
 只有當指定時，才使用分隔符號*instance_name*，以便將它從*系統名稱*或*FCI_network_name*。  
  
 WSFC 節點和伺服器執行個體的必要條件的詳細資訊，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL **='**TCP**://***系統位址***:***連接埠***'**  
 指定的 URL 路徑[資料庫鏡像端點](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]裝載可用性複本目前的 REPLICA ON 子句中定義。  
  
 ENDPOINT_URL 子句是必要的。 如需詳細資訊，請參閱[在加入或修改可用性複本時指定端點 URL &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)。  
  
 **'**TCP**://***system-address***:***port***'**  
 指定 URL 以指定端點 URL 或唯讀的路由 URL。 URL 參數如下所示：  
  
 *system-address*  
 這是明確識別目的地電腦系統的字串，例如系統名稱、完整網域名稱或 IP 位址。  
  
 *port*  
 這是與夥伴伺服器執行個體之鏡像端點相關聯的通訊埠編號 (針對 ENDPOINT_URL 選項)，或伺服器執行個體之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的通訊埠編號 (針對 READ_ONLY_ROUTING_URL 選項)。  
  
 AVAILABILITY_MODE  **=**  {{SYNCHRONOUS_COMMIT |ASYNCHRONOUS_COMMIT |CONFIGURATION_ONLY}  
 SYNCHRONOUS_COMMIT 或 ASYNCHRONOUS_COMMIT 指定主要複本是否等待認可至磁碟之前的主要複本可以認可給定主要上的交易記錄檔記錄強化 （寫入） 的次要複本資料庫。 相同主要複本上不同資料庫的交易可以獨立認可。 SQL Server 2017 CU 1 導入了 CONFIGURATION_ONLY。 CONFIGURATION_ONLY 複本只適用於可用性群組與 CLUSTER_TYPE = 外部或 CLUSTER_TYPE = 無。 
  
 SYNCHRONOUS_COMMIT  
 指定的主要複本會等候認可的交易，直到已強化這個次要複本 （同步認可模式）。 您最多可以為三個複本指定 SYNCHRONOUS_COMMIT，包括主要複本在內。  
  
 ASYNCHRONOUS_COMMIT  
 指定主要複本會認可交易，而不等候這個次要複本強化記錄 (同步-認可可用性模式)。 您最多可以為五個可用性複本指定 ASYNCHRONOUS_COMMIT，包括主要複本在內。  

 CONFIGURATION_ONLY 指定主要複本，以同步方式認可至 master 資料庫，在這個複本上可用性群組組態中繼資料。 複本不會包含使用者資料。 此選項：

- 可裝載於任何版本的 SQL Server，包括 Express Edition。
- 需要資料庫鏡像端點的型別 CONFIGURATION_ONLY 複本`WITNESS`。
- 無法改變。
- 不正確時`CLUSTER_TYPE = WSFC`。 

   如需詳細資訊，請參閱[組態的唯一複本](../../linux/sql-server-linux-availability-group-ha.md)。
  
 AVAILABILITY_MODE 子句是必要的。 如需詳細資訊，請參閱 [可用性模式 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)或 PowerShell，針對 AlwaysOn 可用性群組執行規劃的手動容錯移轉或強制手動容錯移轉 (強制容錯移轉)。  
  
 FAILOVER_MODE  **=**  {自動 |手動}  
 指定您所定義之可用性複本的容錯移轉模式。  
  
 AUTOMATIC  
 啟用自動容錯移轉。 只有當您也指定 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 時，才會支援這個選項。 您可以為兩個可用性複本指定 AUTOMATIC，包括主要複本在內。  
  
> [!NOTE]  
>  SQL Server 容錯移轉叢集執行個體 (FCI) 不支援依照可用性群組進行自動容錯移轉，因此任何由 FCI 裝載的可用性複本只能設定為手動容錯移轉。  
  
 MANUAL  
 可讓已規劃手動容錯移轉或強制手動容錯移轉 (通常稱為*強制容錯移轉*) 的資料庫管理員。  
  
 FAILOVER_MODE 子句是必要的。 不遺失資料的手動容錯移轉以及強制容錯移轉 (可能遺失資料) 這兩種類型的手動容錯移轉會在不同情況下支援。 如需詳細資訊，請參閱本主題稍後的 [容錯移轉及容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。  
  
 SEEDING_MODE  **=**  {自動 |手動}  
 指定如何在次要複本一開始植入。  
  
 AUTOMATIC  
 可讓直接植入。 這個方法植入次要複本，在網路上。 這個方法不需要備份和還原的主要複本上資料庫複本。  
  
> [!NOTE]  
>  直接植入，您必須允許資料庫建立每個次要複本上藉由呼叫**ALTER AVAILABILITY GROUP**與**GRANT CREATE ANY DATABASE**選項。  
  
 MANUAL  
 指定手動植入 （預設值）。 此方法需要您在主要複本上建立資料庫的備份，並手動將次要複本上的該備份還原。  
  
 BACKUP_PRIORITY  **=** *n*  
 指定在這個複本上執行備份的優先權 (相對於相同可用性群組中的其他複本)。 這個值是 0 到 100 範圍之間的整數。 這些值具有以下意義：  
  
-   1..100 表示可以選擇可用性複本來執行備份。 1 表示最低優先權，100 表示最高優先權。 如果 BACKUP_PRIORITY = 1，則只有當目前沒有更高優先權的可用性複本可用時，才會選擇此可用性複本來執行備份。  
  
-   0 表示此可用性複本不是執行備份。 例如，這對於您永遠不希望將備份容錯移轉到其中的遠端可用性複本十分有用。  
  
 如需詳細資訊，請參閱 [使用中次要：在次要複本上備份 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。  
  
 SECONDARY_ROLE **(** ... **)**  
 指定此可用性複本目前擁有次要角色時生效的角色專屬設定 （亦即，每當它是次要複本）。 在括弧內指定任一個或兩個次要角色選項。 如果您同時指定兩個選項，則使用逗號分隔清單。  
  
 次要角色選項如下：  
  
 ALLOW_CONNECTIONS  **=**  {否 |READ_ONLY |所有}  
 指定執行次要角色之給定可用性複本 (也就是做為次要複本) 的資料庫是否可接受來自用戶端的連接，下列其中一個值：  
  
 否  
 不允許使用者連接至這個複本的次要資料庫。 無法讀取這些資料庫。 這是預設行為。  
  
 READ_ONLY  
 只允許連接至其中的應用程式意圖屬性設定為次要複本的資料庫**ReadOnly**。 如需有關這個屬性的詳細資訊，請參閱＜ [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)＞。  
  
 ALL  
 次要複本的資料庫允許所有連接進行唯讀存取。  
  
 如需詳細資訊，請參閱 [使用中次要：可讀取的次要複本 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)中心概念。  
  
 READ_ONLY_ROUTING_URL **='**TCP**://***系統位址***:***連接埠***'**  
 指定向此可用性複本路由傳送讀取意圖連接要求所使用的 URL。 這是 SQL Server Database Engine 接聽的 URL。 SQL Server Database Engine 的預設執行個體通常會接聽 TCP 通訊埠 1433。  
  
 具名的執行個體，您可以透過查詢取得的連接埠號碼**連接埠**和**type_desc**的資料行[sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md)動態管理檢視。 伺服器執行個體會使用 TRANSACT-SQL 接聽程式 (**type_desc = 'TSQL'**)。  
  
 如需計算複本之唯讀路由 URL 的詳細資訊，請參閱[計算 read_only_routing_url for Always On](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx)。  
  
> [!NOTE]  
>  若是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體，則應該將 Transact-SQL 接聽程式設定為使用特定通訊埠。 如需詳細資訊，請參閱[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
 PRIMARY_ROLE **(** ... **)**  
 指定此可用性複本目前擁有主要角色時生效的角色專屬設定 （亦即，每當它是主要複本）。 在括弧內指定任一個或兩個主要角色選項。 如果您同時指定兩個選項，則使用逗號分隔清單。  
  
 主要角色選項如下：  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE |所有}  
 指定執行主要角色之給定可用性複本 (也就是做為主要複本) 的資料庫可從用戶端接受的連接類型，下列其中一個值：  
  
 READ_WRITE  
 不允許 Application Intent 連接屬性設為 **ReadOnly** 的連接。  當 Application Intent 屬性設為 **ReadWrite** 或是未設定 Application Intent 連接屬性時，便會允許連接。 如需有關 Application Intent 連接屬性的詳細資訊，請參閱＜ [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)＞。  
  
 ALL  
 主要複本的資料庫允許所有連接。 這是預設行為。  
  
 READ_ONLY_ROUTING_LIST  **=**  { **('**\<臨界點 >**'** [ **，**...*n* ] **)** |無} 指定以逗號分隔清單的伺服器執行個體裝載此可用性群組的可用性複本在次要角色之下執行時，符合下列需求：  
  
-   設定為允許所有連接或唯讀連接 (請參閱 SECONDARY_ROLE 選項的 ALLOW_CONNECTIONS 引數，如上所示)。  
  
-   定義其唯讀的路由 URL (請參閱 SECONDARY_ROLE 選項的 READ_ONLY_ROUTING_URL 引數，如上所示)。  
  
 READ_ONLY_ROUTING_LIST 值如下：  
  
 \<臨界點 > 指定的執行個體的位址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也就是次要角色之下執行時，是可讀取次要複本的複本的主機。  
  
 使用逗號分隔清單指定可能裝載可讀取之次要複本的所有伺服器執行個體。 唯讀路由會依照的順序清單中指定的伺服器執行個體。 如果您將複本的主機伺服器執行個體包含在複本的唯讀路由清單中，將此伺服器執行個體放在清單結尾通常是很好的作法，讓讀取意圖的連接通往次要複本 (如果有一個可用的次要複本的話)。  
  
 開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，您可以在可讀取的次要複本之間的負載平衡讀取意圖要求。 您指定將複本放在一組巢狀的唯讀路由清單中的括號。 如需詳細資訊和範例，請參閱[設定唯讀複本之間的負載平衡](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)。  
  
 無  
 指定當此可用性複本的主要複本時，唯讀路由不支援的。 這是預設行為。  
  
 SESSION_TIMEOUT  **=**  *整數*  
 指定工作階段逾時期限 (以秒為單位)。 如果您沒有指定這個選項，依預設，這個期間是 10 秒。 最小值是 5 秒。  
  
> [!IMPORTANT]  
>  我們建議您讓逾時期限保持在 10 秒或更久。  
  
 如需工作階段逾時期限的詳細資訊，請參閱[的 Alwayson 可用性群組概觀 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 在可用性群組  
 指定兩個可用性群組構成*分散式的可用性群組*。 每個可用性群組屬於它自己 Windows Server 容錯移轉叢集 (WSFC)。 當您建立分散式的可用性群組時，目前的 SQL Server 執行個體上之可用性群組會成為主要可用性群組。 第二個可用性群組會變成次要可用性群組。  
  
 您要加入分散式的可用性群組的次要可用性群組。 如需詳細資訊，請參閱 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)中的 PowerShell，將次要複本加入現有的 AlwaysOn 可用性群組中。  
  
 \<ag_name > 指定名稱的可用性群組會組成一個分散式的可用性群組的一半。  
  
 LISTENER **='**TCP**://***system-address***:***port***'**  
 指定可用性群組相關聯的接聽程式的 URL 路徑。  
  
 接聽程式子句是必要的。  
  
 **'**TCP**://***system-address***:***port***'**  
 指定的 URL 相關聯的可用性群組接聽程式。 URL 參數如下所示：  
  
 *system-address*  
 這是字串，例如系統名稱、 完整的網域名稱或 IP 位址，可明確識別接聽程式。  
  
 *port*  
 為可用性群組的鏡像端點相關聯的通訊埠編號。 請注意，這不是接聽程式的連接埠。  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT |ASYNCHRONOUS_COMMIT |CONFIGURATION_ONLY}  
 指定的主要複本是否等待認可至磁碟之前的主要複本可以認可給定主要資料庫上的交易的記錄檔記錄強化 （寫入） 的次要可用性群組。  
  
 SYNCHRONOUS_COMMIT  
 指定的主要複本會等候認可的交易，直到已強化次要可用性群組上。 您可以指定 synchronous_commit 時，最多兩個可用性群組，包括主要可用性群組。  
  
 ASYNCHRONOUS_COMMIT  
 指定的主要複本會認可交易而不等候這個次要可用性群組，強行寫入記錄。 您可以指定 ASYNCHRONOUS_COMMIT，最多兩個可用性群組，包括主要可用性群組。  
  
 AVAILABILITY_MODE 子句是必要的。  
  
 FAILOVER_MODE  **=**  {手動}  
 指定分散式的可用性群組的容錯移轉模式。  
  
 MANUAL  
 可讓已規劃手動容錯移轉或強制手動容錯移轉 (通常稱為*強制容錯移轉*) 的資料庫管理員。  
  
 FAILOVER_MODE 子句是必要項目，並為 [手動] 的唯一選項。 不支援自動容錯移轉至次要可用性群組。  
  
 SEEDING_MODE  **=**  {自動 |手動}  
 指定如何次要可用性群組一開始植入。  
  
 AUTOMATIC  
 可讓直接植入。 這個方法植入次要可用性群組，在網路上。 這個方法不需要備份和還原的次要可用性群組之複本的主要資料庫複本。  
  
 MANUAL  
 指定手動植入 （預設值）。 此方法需要您在主要複本上建立資料庫的備份，並手動還原的次要可用性群組複本上備份。  
  
 接聽程式**'***dns_name***' (** \<listener_option > **)**定義新的可用性群組接聽程式，這個可用性群組。 LISTENER 是選擇性引數。  
  
> [!IMPORTANT]  
>  建立第一個接聽程式之前，我們強烈建議您先閱讀[建立或設定可用性群組接聽程式 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  針對給定的可用性群組建立接聽程式之後，我們強烈建議您執行以下操作：  
>   
>  -   要求網路管理員將接聽程式的 IP 位址保留為專用。  
> -   將接聽程式的 DNS 主機名稱提供給應用程式開發人員，以便在要求與這個可用性群組進行用戶端連接時，用於連接字串中。  
  
 *dns_name*  
 指定可用性群組接聽程式的 DNS 主機名稱。 接聽程式的 DNS 名稱在網域和 NetBIOS 中都必須是唯一的。  
  
 *dns_name*是字串值。 此名稱只能包含英數字元、虛線 (-) 和連字號 (_) (順序不拘)。 DNS 主機名稱不區分大小寫。 長度上限是 63 個字元。  
  
 我們建議您指定一個有意義的字串。 例如，如果是名為 `AG1`的可用性群組，有意義的 DNS 主機名稱會是 `ag1-listener`。  
  
> [!IMPORTANT]  
>  NetBIOS 只會辨識 DNS 名稱中的前 15 個字元。 如果您有兩個由相同 Active Directory 所控制的 WSFC 叢集，而且您嘗試建立可用性群組接聽程式中使用名稱超過 15 個字元以及完全相同的 15 個字元前置詞這兩個叢集，錯誤會報告 虛擬網路名稱資源無法上線。 如需有關 DNS 名稱之前置詞命名規則的詳細資訊，請參閱＜ [指派網域名稱](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx)＞。  
  
 \<listener_option > LISTENER 採用下列其中一種\<listener_option > 選項： 
  
 WITH DHCP [ ON { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** } ]  
 指定可用性群組接聽程式使用動態主機設定通訊協定 (DHCP)。  （選擇性） 使用 ON 子句來識別此接聽程式建立所在的網路。 DHCP 僅限於單一子網路用於每個伺服器執行個體裝載可用性群組中的複本。  
  
> [!IMPORTANT]  
>  不建議在實際執行環境中使用 DHCP。 如果有停機時間且 DHCP IP 租用到期，則需要額外的時間來註冊與接聽程式 DNS 名稱相關聯的新 DHCP 網路 IP 位址，而影響用戶端連接。 但是，DHCP 適合用於設定開發和測試環境，以驗證可用性群組的基本功能，也適合與應用程式整合。  
  
 例如：  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **(‘***four_part_ipv4_address***’,‘***four_part_ipv4_mask***’)** | **(‘***ipv6_address***’)** } [ **,** ...*n* ] **)** [ **,** PORT **=***listener_port* ]  
 指定，而不是使用 DHCP，可用性群組接聽程式使用一或多個靜態 IP 位址。 若要建立跨多個子網路的可用性群組，接聽程式組態中每個子網路都需要一個靜態 IP 位址。 對於給定的子網路，靜態 IP 位址可以是 IPv4 位址或 IPv6 位址。 請連絡網路系統管理員以取得裝載新可用性群組之複本的每個子網路的靜態 IP 位址。  
  
 例如：  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 指定可用性群組接聽程式的 IPv4 四部分位址。 例如， `10.120.19.155`。  
  
 *four_part_ipv4_mask*  
 指定可用性群組接聽程式的 IPv4 四部分遮罩。 例如， `255.255.254.0`。  
  
 *ipv6_address*  
 指定可用性群組接聽程式的 IPv6 位址。 例如， `2001::4898:23:1002:20f:1fff:feff:b3a3`。  
  
 PORT **=** *listener_port*  
 指定的連接埠號碼 —*listener_port*，WITH IP 子句所指定的可用性群組接聽程式所使用。 PORT 為選擇性。  
  
 支援預設通訊埠編號 1433。 但是，如果您有安全考量，我們建議您使用不同的通訊埠編號。  
  
 例如： `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>必要條件和限制  
 如需建立可用性群組之必要條件的資訊，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 如需可用性群組 TRANSACT-SQL 陳述式有關限制的詳細資訊，請參閱[概觀的 TRANSACT-SQL 陳述式的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色的成員資格，以及 CREATE AVAILABILITY GROUP 伺服器權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>A. 設定次要複本上的備份、具彈性的容錯移轉原則和連接存取  
 下列範例會針對兩個使用者資料庫 `MyAg` 和 `ThisDatabase` 建立名為 `ThatDatabase` 的可用性群組。 下表摘要說明針對選項指定的值，這些選項是針對整個可用性群組所設定。  
  
|群組選項|設定|Description|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|這個自動備份喜好設定會指示應該在次要複本上進行備份，但是主要複本是唯一線上複本 (這是預設行為) 的情況例外。 若要讓 AUTOMATED_BACKUP_PREFERENCE 設定有任何效果，您必須在可用性資料庫上撰寫備份工作的指令碼，以便將自動備份喜好設定納入考量。|  
|FAILURE_CONDITION_LEVEL|3|這個失敗狀況層級會指定應該在嚴重 SQL Server 內部錯誤發生時起始自動容錯移轉，例如執行緒同步鎖定遭到遺棄、嚴重的寫入存取違規或是傾印過多。|  
|HEALTH_CHECK_TIMEOUT|600000|此健全狀況檢查逾時值 60 秒，指定在 WSFC 叢集會等待 60000 毫秒[sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系統預存程序傳回伺服器健全狀況資訊的伺服器執行個體叢集假設主機伺服器執行個體很慢或無回應之前，請使用 自動裝載的同步認可複本。 (預設值為 30000 毫秒)。|  
  
 三個可用性複本會由 `COMPUTER01`、`COMPUTER02` 和 `COMPUTER03` 電腦上的預設伺服器執行個體所主控。 下表摘要說明針對每個複本之複本選項所指定的值。  
  
|複本選項|`COMPUTER01` 的設定|`COMPUTER02` 的設定|`COMPUTER03` 的設定|Description|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP://*COMPUTER01:5022*|TCP://*COMPUTER02:5022*|TCP://*COMPUTER03:5022*|在此範例中，這些系統是相同的網域，因此端點 URL 可以使用電腦系統的名稱做為系統位址。|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|其中兩個複本會使用同步認可模式。 同步時，它們支援容錯移轉，但不會失去資料。 使用非同步認可可用性模式的第三個複本。|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|同步認可複本支援自動容錯移轉和計畫的手動容錯移轉。 同步認可的可用性模式複本僅支援強制手動容錯移轉。|  
|BACKUP_PRIORITY|30|30|90|更高的優先順序 90 會被指派給非同步認可的複本，而非同步認可的副本。 備份通常會發生在主控非同步認可複本的伺服器執行個體。|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|只有非同步認可的複本會當做可讀取的次要複本。<br /><br /> 指定電腦名稱和預設的 Database Engine 通訊埠編號 (1433)。<br /><br /> 此引數是選擇性的。|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|在主要角色中，所有複本都拒絕讀取意圖的連接嘗試。<br /><br /> 如果本機複本次要角色之下執行，讀取意圖連接要求會路由傳送至 COMPUTER03。 當該複本以主要角色執行時，就會停用唯讀路由。<br /><br /> 此引數是選擇性的。|  
|SESSION_TIMEOUT|10|10|10|此範例會指定預設的工作階段逾時值 (10)。 此引數是選擇性的。|  
  
 最後，此範例會指定選用的 LISTENER 子句，以建立新可用性群組的可用性群組接聽程式。 系統會針對此接聽程式指定唯一的 DNS 名稱 `MyAgListenerIvP6`。 兩個複本位於不同的子網路上，因此接聽程式必須使用靜態 IP 位址。 針對這兩個可用性複本，WITH IP 子句都會指定使用 IPv6 格式的靜態 IP 位址 `2001:4898:f0:f00f::cf3c` 及 `2001:4898:e0:f213::4ce2`。 此範例也會指定使用選用的 PORT 引數指定通訊埠 `60173` 做為接聽程式通訊埠。  
  
```SQL
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABIIITY GROUP [MyAg]
  ADD LISTENER ‘MyAgListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立可用性群組 &#40;TRANSACT-SQL &#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [使用可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [卸除可用性群組 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [疑難排解 Always On 可用性群組組態 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性群組接聽程式、用戶端連接及應用程式容錯移轉 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

