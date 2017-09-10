---
title: "ALTER 可用性群組 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_AVAILABILITY_GROUP_TSQL
- ALTER_AVAILABILITY_TSQL
- ALTER AVAILABILITY GROUP
- ALTER AVAILABILITY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- ALTER AVAILABILITY GROUP statement
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: f039d0de-ade7-4aaf-8b7b-d207deb3371a
caps.latest.revision: 152
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef1d68317c2e288a13d7b07d559b5de45e29cd28
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-availability-group-transact-sql"></a>ALTER AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  改變現有 Alwayson 可用性群組中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 大部分 ALTER AVAILABILITY GROUP 引數僅在目前的主要複本上支援。 不過，JOIN、FAILOVER 和 FORCE_FAILOVER_ALLOW_DATA_LOSS 引數只在次要複本上支援。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER AVAILABILITY GROUP group_name   
  {  
     SET ( <set_option_spec> )   
   | ADD DATABASE database_name   
   | REMOVE DATABASE database_name  
   | ADD REPLICA ON <add_replica_spec>   
   | MODIFY REPLICA ON <modify_replica_spec>  
   | REMOVE REPLICA ON <server_instance>  
   | JOIN  
   | JOIN AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   | MODIFY AVAILABILITY GROUP ON <modify_availability_group_spec> [ ,...2 ]  
   | GRANT CREATE ANY DATABASE  
   | DENY CREATE ANY DATABASE  
   | FAILOVER  
   | FORCE_FAILOVER_ALLOW_DATA_LOSS   | ADD LISTENER ‘dns_name’ ( <add_listener_option> )  
   | MODIFY LISTENER ‘dns_name’ ( <modify_listener_option> )  
   | RESTART LISTENER ‘dns_name’  
   | REMOVE LISTENER ‘dns_name’  
   | OFFLINE  
  }  
[ ; ]  
  
<set_option_spec> ::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  
<server_instance> ::=   
 { 'system_name[\instance_name]' | 'FCI_network_name[\instance_name]' }  
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }   
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
  
<modify_replica_spec>::=  
  <server_instance> WITH  
    (    
       ENDPOINT_URL = 'TCP://system-address:port'   
     | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }   
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }   
     | SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( ‘<server_instance>’ [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
    )   
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<modify_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER = 'TCP://system-address:port'  
       | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
       | SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<add_listener_option> ::=  
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
  
<modify_listener_option>::=  
    {  
       ADD IP ( <ip_address_option> )   
     | PORT = listener_port  
    }  
  
```  
  
## <a name="arguments"></a>引數  
 *群組名稱*  
 指定新的可用性群組名稱。 *group_name*必須是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別碼，而且必須是唯一的 WSFC 叢集中的所有可用性群組。  
  
 AUTOMATED_BACKUP_PREFERENCE  **=**  {主要 |SECONDARY_ONLY |次要 |無}  
 指定在選擇要在何處執行備份時，有關備份作業應該如何評估主要複本的喜好設定。 您可以編寫給定備份作業，將自動備份喜好設定納入考量。 請務必了解，喜好設定並不是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 強制施行，所以它對於隨選備份沒有任何影響。  
  
 只有主要複本上才支援。  
  
 其值如下：  
  
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
>  若要檢視現有的可用性群組的自動備份喜好設定，請選取**automated_backup_preference**或**automated_backup_preference_desc**資料行[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目錄檢視。 此外， [sys.fn_hadr_backup_is_preferred_replica &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)可用來判斷慣用的備份複本。  此函數永遠都會針對至少其中一個複本傳回 1，即使當 `AUTOMATED_BACKUP_PREFERENCE = NONE` 時亦然。  
  
 FAILURE_CONDITION_LEVEL  **=**  {1 | 2 |**3** | 4 | 5}  
 指定哪一個失敗狀況將會觸發這個可用性群組的自動容錯移轉。 FAILURE_CONDITION_LEVEL 群組層級設定，但卻設定成同步認可可用性模式的可用性複本上才相關 (AVAILIBILITY_MODE  **=**  SYNCHRONOUS_COMMIT)。 此外，失敗狀況可以觸發自動容錯移轉只有當主要和次要複本設定成自動容錯移轉模式 (FAILOVER_MODE  **=** 自動)，而且次要複本是目前與主要複本同步處理。  
  
 只有主要複本上才支援。  
  
 失敗狀況層級 (1–5) 的範圍從最低限制 (層級 1) 到最高限制 (層級 5)。 給定的狀況層級包含所有較少限制的層級。 因此，最嚴格的狀況層級 5 包含四個較少限制的狀況層級 (1-4)，層級 4 則包含層級 1-3，依此類推。 下表描述與每個層級對應的失敗狀況。  
  
|Level|失敗狀況|  
|-----------|-----------------------|  
|1|指定在發生以下任何情況時應該起始自動容錯移轉：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務關閉。<br /><br /> 由於未從伺服器執行個體收到 ACK，所以用於連接到 WSFC 叢集的可用性群組租用已到期。 如需詳細資訊，請參閱 [How It Works: SQL Server Always On Lease Timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)(運作方式：SQL Server AlwaysOn 租用逾時)。|  
|2|指定在發生以下任何情況時應該起始自動容錯移轉：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體未連接到叢集，而且已超出使用者指定之可用性群組的 HEALTH_CHECK_TIMEOUT 臨界值。<br /><br /> 可用性複本處於失敗狀態。|  
|3|指定應該在嚴重 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部錯誤發生時起始自動容錯移轉，例如執行緒同步鎖定遭到遺棄、嚴重的寫入存取違規或是傾印過多。<br /><br /> 這是預設行為。|  
|4|指定應該在發生中度 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部錯誤時起始自動容錯移轉，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部資源集區中持續的記憶體不足狀況。|  
|5|指定應該在發生任何符合的失敗狀況時起始自動容錯移轉，這些狀況包括：<br /><br /> SQL 引擎工作者執行緒已耗盡。<br /><br /> 偵測到無法解決的死結。|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體對用戶端要求缺少回應與可用性群組無關。  
  
 FAILURE_CONDITION_LEVEL 和 HEALTH_CHECK_TIMEOUT 值會定義*彈性容錯移轉原則*特定群組。 這個具彈性的容錯移轉原則讓您能夠更精確控制哪些條件必須造成自動容錯移轉。 如需詳細資訊，請參閱[彈性的容錯移轉原則，自動容錯移轉的可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
 HEALTH_CHECK_TIMEOUT  **=**  *（毫秒)*  
 指定等候時間 （以毫秒為單位） 的[sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)系統預存程序傳回伺服器健全狀況資訊，WSFC 叢集假設伺服器執行個體很慢或無回應之前。 HEALTH_CHECK_TIMEOUT 群組層級設定，但卻設定為具有自動容錯移轉的同步認可可用性模式的可用性複本上才相關 (AVAILIBILITY_MODE  **=** 同步_COMMIT)。  此外，健全狀況檢查逾時可以觸發自動容錯移轉只有當主要和次要複本設定成自動容錯移轉模式 (FAILOVER_MODE  **=** 自動) 與次要資料庫複本目前與主要複本 synchronized。  
  
 預設 HEALTH_CHECK_TIMEOUT 值為 30000 毫秒 (30 秒)。 最小值為 15000 毫秒 (15 秒)，最大值為 4294967295 毫秒。  
  
 只有主要複本上才支援。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** 不會在資料庫層級執行健全狀況檢查。  
  
 DB_FAILOVER  **=**  {ON |OFF}  
 指定要採取的主要複本上資料庫離線時的回應。 可用性群組中資料庫的任何狀態不是 ONLINE 設定為 ON 時，會觸發自動容錯移轉。 當這個選項設為 OFF 時的執行個體的健全狀況用來觸發自動容錯移轉。  
 
 如需有關這項設定的詳細資訊，請參閱[資料庫層級健全狀況偵測選項](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md) 

 
 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 2017 CTP 2.2 中導入。 用來設定主要認可交易之前認可所需的同步次要複本的最小數目。 可保證 SQL Server 交易將會等待直到更新次要複本的最小數目上的交易記錄檔。 預設值為 0 可讓 SQL Server 2016 相同的行為。 最小值為 0。 最大值是減 1 的複本數目。 此選項與在同步認可模式下的複本。 當複本在同步認可模式，主要複本上的寫入等候同步次要複本上的寫入會認可到複本資料庫的交易記錄檔。 如果裝載次要複本的 SQL Server 停止回應，SQL Server 裝載主要複本會標記該次要複本未同步處理，並繼續。 沒有回應的資料庫回到線上時它會處於 「 未同步處理 」 狀態，複本會標示為狀況不良，直到主要可讓您同步一次。 此設定可確保主要複本將不會繼續直到複本的最小數目已認可的每個交易。 如果無法使用之複本的最小數目認可在主要伺服器上的將會失敗。 此設定適用於可用性群組的叢集類型`WSFC`和`EXTERNAL`。 叢集類型`EXTERNAL`可用性群組新增到叢集資源時，變更設定。 請參閱[的可用性群組組態的高可用性與資料保護](../../linux/sql-server-linux-availability-group-ha.md)。
  
 將資料庫加入*database_name*  
 指定您想要加入至可用性群組之一個或多個使用者資料庫的清單。 這些資料庫必須位於裝載目前主要複本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。 您可以為可用性群組指定多個資料庫，但每個資料庫只能屬於一個可用性群組。 如需可用性群組可支援的資料庫類型資訊，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md). 若要了解哪些本機資料庫已屬於可用性群組，請參閱**replica_id**中的資料行[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。  
  
 只有主要複本上才支援。  
  
> [!NOTE]  
>  建立可用性群組之後，您將需要連接至裝載次要複本的每個伺服器執行個體，然後準備每個次要資料庫，並將其聯結至該可用性群組。 如需詳細資訊，請參閱 [於 AlwaysOn 次要資料庫啟動資料移動 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)。  
  
 移除資料庫*database_name*  
 從可用性群組中移除指定的主要資料庫和對應的次要資料庫。 只有主要複本上才支援。  
  
 從可用性群組中移除可用性資料庫之後建議後續操作的相關資訊，請參閱[移除主要資料庫從可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
 ADD REPLICA ON  
 指定要在可用性群組中裝載次要複本的 SQL 伺服器執行個體 (一個到八個)。  每個複本是由後面接著 WITH (…) 子句的伺服器執行個體位址所指定。  
  
 只有主要複本上才支援。  
  
 您必須將每個新的次要複本聯結至可用性群組。 如需詳細資訊，請參閱本節稍後的 JOIN 選項描述。  
  
 \<臨界點 >  
 指定的執行個體的位址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]也就是針對複本主機。 此位址格式取決於執行個體為預設執行個體還是具名執行個體，以及它是獨立的執行個體還是容錯移轉叢集執行個體 (FCI)。 其語法如下：  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 這個位址的元件如下所示：  
  
 *system_name*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目標執行個體所在之電腦系統的 NetBIOS 名稱。 這部電腦必須是 WSFC 節點。  
  
 *FCI_network_name*  
 這是用來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集的網路名稱。 如果伺服器執行個體當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉夥伴來參與，則使用它。 執行 SELECT [@@SERVERNAME ](../../t-sql/functions/servername-transact-sql.md)在 FCI 上伺服器執行個體傳回它的完整 '*FCI_network_name*[\\*instance_name*]' 字串 (即完整複本名稱）。  
  
 *instance_name*  
 是的執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所裝載*系統名稱*或*FCI_network_name*且具有啟用 Always On。 如果是預設伺服器執行個體， *instance_name* 為選擇性。 執行個體名稱不區分大小寫。 在獨立伺服器執行個體，這個值名稱等同於所執行 SELECT 傳回的值[@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md)。  
  
 \  
 只有當指定時，才使用分隔符號*instance_name*，以便將它從*系統名稱*或*FCI_network_name*。  
  
 WSFC 節點和伺服器執行個體的必要條件的詳細資訊，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 ENDPOINT_URL ='TCP: / /*系統位址*:*連接埠*'  
 指定的 URL 路徑[資料庫鏡像端點](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將要裝載您要加入或修改之可用性複本。  
  
 ENDPOINT_URL 在 ADD REPLICA ON 子句中是必要的，而在 MODIFY REPLICA ON 子句中則是選擇性。  如需詳細資訊，請參閱 [在加入或修改可用性複本時指定端點 URL &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)設定伺服器執行個體時常見的問題。  
  
 **'**TCP**://***系統位址***:***連接埠***'**  
 指定 URL 以指定端點 URL 或唯讀的路由 URL。 URL 參數如下所示：  
  
 *system-address*  
 這是明確識別目的地電腦系統的字串，例如系統名稱、完整網域名稱或 IP 位址。  
  
 *port*  
 這是與伺服器執行個體之鏡像端點相關聯的通訊埠編號 (針對 ENDPOINT_URL 選項)，或伺服器執行個體之 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 所使用的通訊埠編號 (針對 READ_ONLY_ROUTING_URL 選項)。  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT |ASYNCHRONOUS_COMMIT}  
 指定在主要複本可以認可給定主要資料庫上的交易之前，主要複本是否必須等候次要複本認可將記錄檔記錄強化 (寫入) 至磁碟。 相同主要複本上不同資料庫的交易可以獨立認可。  
  
 SYNCHRONOUS_COMMIT  
 指定在這個次要複本上強化交易之前，主要複本將會等候認可交易 (同步-認可模式)。 您最多可以為三個複本指定 SYNCHRONOUS_COMMIT，包括主要複本在內。  
  
 ASYNCHRONOUS_COMMIT  
 指定主要複本會認可交易，而不等候這個次要複本強化記錄 (同步-認可可用性模式)。 您最多可以為五個可用性複本指定 ASYNCHRONOUS_COMMIT，包括主要複本在內。  
  
 AVAILABILITY_MODE 在 ADD REPLICA ON 子句中是必要的，而在 MODIFY REPLICA ON 子句中則是選擇性。 如需詳細資訊，請參閱 [可用性模式 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)或 PowerShell，針對 AlwaysOn 可用性群組執行規劃的手動容錯移轉或強制手動容錯移轉 (強制容錯移轉)。  
  
 FAILOVER_MODE  **=**  {自動 |手動}  
 指定您所定義之可用性複本的容錯移轉模式。  
  
 AUTOMATIC  
 啟用自動容錯移轉。 只有當您同時指定 AVAILABILITY_MODE = SYNCHRONOUS_COMMIT 時，才支援 AUTOMATIC。 您可以為兩個可用性複本指定 AUTOMATIC，包括主要複本在內。  
  
> [!NOTE]  
>  SQL Server 容錯移轉叢集執行個體 (FCI) 不支援依照可用性群組進行自動容錯移轉，因此任何由 FCI 裝載的可用性複本只能設定為手動容錯移轉。  
  
 MANUAL  
 可讓手動容錯移轉或強制手動容錯移轉 (*強制容錯移轉*) 的資料庫管理員。  
  
 FAILOVER_MODE 在 ADD REPLICA ON 子句中是必要的，而在 MODIFY REPLICA ON 子句中則是選擇性。 有兩種手動容錯移轉類型存在，也就是不遺失資料的手動容錯移轉以及強制容錯移轉 (可能遺失資料)，不同情況下會支援不同類型。  如需詳細資訊，請參閱[容錯移轉及容錯移轉模式 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)。  
  
 SEEDING_MODE  **=**  {自動 |手動}  
 指定如何在次要複本會一開始植入。  
  
 AUTOMATIC  
 可讓直接植入。 這個方法會在網路上，植入次要複本。 這個方法不需要備份和還原的主要複本上資料庫複本。  
  
> [!NOTE]  
>  直接植入，您必須允許資料庫建立每個次要複本上藉由呼叫**ALTER AVAILABILITY GROUP**與**GRANT CREATE ANY DATABASE**選項。  
  
 MANUAL  
 指定手動植入 （預設值）。 此方法需要您在主要複本上建立資料庫的備份，並手動將次要複本上的該備份還原。  
  
 BACKUP_PRIORITY**=***n*  
 指定在這個複本上執行備份的優先權 (相對於相同可用性群組中的其他複本)。 這個值是 0 到 100 範圍之間的整數。 這些值具有以下意義：  
  
-   1..100 表示可以選擇可用性複本來執行備份。 1 表示最低優先權，100 表示最高優先權。 如果 BACKUP_PRIORITY = 1，則只有當目前沒有更高優先權的可用性複本可用時，才會選擇此可用性複本來執行備份。  
  
-   0 表示絕對不會選擇這個可用性複本來執行備份。 例如，這對於您永遠不希望將備份容錯移轉到其中的遠端可用性複本十分有用。  
  
 如需詳細資訊，請參閱 [使用中次要：在次要複本上備份 &#40;AlwaysOn 可用性群組&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)中心概念。  
  
 SECONDARY_ROLE **(** ... **)**  
 指定將會在此可用性複本目前擁有次要角色 (亦即，每當它是次要複本時) 時生效的角色專屬設定。 在括弧內指定任一個或兩個次要角色選項。 如果您同時指定兩個選項，則使用逗號分隔清單。  
  
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
  
 如需有關計算可用性複本之唯讀路由 URL 的詳細資訊，請參閱[計算 read_only_routing_url for Always On](http://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx)。  
  
> [!NOTE]  
>  若是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體，則應該將 Transact-SQL 接聽程式設定為使用特定通訊埠。 如需詳細資訊，請參閱[設定伺服器接聽特定 TCP 通訊埠 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
 PRIMARY_ROLE **(** ... **)**  
 指定將會在此可用性複本目前擁有主要角色 (亦即，每當它是主要複本時) 時生效的角色專屬設定。 在括弧內指定任一個或兩個主要角色選項。 如果您同時指定兩個選項，則使用逗號分隔清單。  
  
 主要角色選項如下：  
  
 ALLOW_CONNECTIONS  **=**  {READ_WRITE |所有}  
 指定執行主要角色之給定可用性複本 (也就是做為主要複本) 的資料庫可從用戶端接受的連接類型，下列其中一個值：  
  
 READ_WRITE  
 不允許 Application Intent 連接屬性設為 **ReadOnly** 的連接。  當 Application Intent 屬性設為 **ReadWrite** 或是未設定 Application Intent 連接屬性時，便會允許連接。 如需有關 Application Intent 連接屬性的詳細資訊，請參閱＜ [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)＞。  
  
 ALL  
 主要複本的資料庫允許所有連接。 這是預設行為。  
  
 READ_ONLY_ROUTING_LIST  **=**  { **('**\<臨界點 >**'** [ **，**...*n* ] **)** |無}  
 針對這個可用性群組，指定裝載可用性複本之伺服器執行個體的逗號分隔清單，以次要角色執行時，這些可用性複本會符合下列需求：  
  
-   設定為允許所有連接或唯讀連接 (請參閱 SECONDARY_ROLE 選項的 ALLOW_CONNECTIONS 引數，如上所示)。  
  
-   定義其唯讀的路由 URL (請參閱 SECONDARY_ROLE 選項的 READ_ONLY_ROUTING_URL 引數，如上所示)。  
  
 READ_ONLY_ROUTING_LIST 值如下：  
  
 \<臨界點 >  
 針對以次要角色執行時，可讀取之次要複本的可用性複本，指定其主機之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的位址。  
  
 使用逗號分隔清單指定可能裝載可讀取之次要複本的所有伺服器執行個體。 唯讀的路由將遵循清單中指定伺服器執行個體的順序。 如果您將複本的主機伺服器執行個體包含在複本的唯讀路由清單中，將此伺服器執行個體放在清單結尾通常是很好的作法，讓讀取意圖的連接通往次要複本 (如果有一個可用的次要複本的話)。  
  
 開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，您可以在可讀取的次要複本之間的負載平衡讀取意圖要求。 您指定將複本放在一組巢狀的唯讀路由清單中的括號。 如需詳細資訊和範例，請參閱[設定唯讀複本之間的負載平衡](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)。  
  
 無  
 指定當此可用性複本是主要複本時，將不支援唯讀路由。 這是預設行為。 搭配 MODIFY REPLICA ON 使用時，此值會停用現有的清單 (如果有的話)。  
  
 SESSION_TIMEOUT  **=** *秒*  
 指定工作階段逾時期限 (以秒為單位)。 如果您沒有指定這個選項，依預設，這個期間是 10 秒。 最小值是 5 秒。  
  
> [!IMPORTANT]  
>  我們建議您讓逾時期限保持在 10 秒或更久。  
  
 如需工作階段逾時期限的詳細資訊，請參閱[的 Alwayson 可用性群組概觀 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
 MODIFY REPLICA ON  
 修改可用性群組的任何複本。 要修改的複本清單針對每一個複本包含伺服器執行個體位址和 WITH (…) 子句。  
  
 只有主要複本上才支援。  
  
 REMOVE REPLICA ON  
 從可用性群組中移除指定的次要複本。 您不能從可用性群組中移除目前的主要複本。 當移除該複本時，它會停止接收資料。 其次要資料庫會從可用性群組中移除，並且進入 RESTORING 狀態。  
  
 只有主要複本上才支援。  
  
> [!NOTE]  
>  如果您在某個複本處於無法使用或失敗狀態時刪除該複本，則當它恢復連線狀態時，將會發現它不再屬於原來的可用性群組。  
  
 JOIN  
 使得本機伺服器執行個體裝載指定之可用性群組內的次要複本。  
  
 只有在尚未聯結至可用性群組的次要複本上支援。  
  
 如需詳細資訊，請參閱 [將次要複本聯結至可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)。  
  
 FAILOVER  
 起始可用性群組的手動容錯移轉，而不會讓連接的次要複本遺失資料。 您輸入容錯移轉目標容錯移轉命令所在的複本稱為。  容錯移轉目標將會接管主要角色，並復原每個資料庫的副本，然後讓這兩個資料庫連線，做為新的主要資料庫。 之前的主要複本會同時轉換到次要角色，且其資料庫會變成次要資料庫，並立即遭到暫停。 您可能可以透過一連串的失敗，來回切換這些角色。  
  
 只有在目前與主要複本同步處理的同步認可次要複本上支援。 請注意，次要複本也必須與主要複本同步處理，才能在同步認可模式下執行。  
  
> [!NOTE]  
>  只要容錯移轉目標接受了命令，就會傳回容錯移轉命令。 不過，在可用性群組完成容錯移轉之後，會以非同步方式復原資料庫。  
  
 如需限制的資訊，必要條件和建議執行規劃的手動容錯移轉，請參閱[執行已規劃的手動容錯移轉可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 > [!CAUTION]  
>  強制容錯移轉 (可能包含某些資料遺失) 嚴格來說是一種災害復原方法。 因此，我們強烈建議您只有在主要複本不再執行、您願意承擔遺失資料的風險，而且您必須立即將服務還原到可用性群組時，才進行強制容錯移轉。  
  
 僅在角色處於 SECONDARY 或 RESOLVING 狀態的複本上支援。 --您輸入容錯移轉命令所在的複本稱為*容錯移轉目標*。  
  
 強制可用性群組容錯移轉至容錯移轉目標 (可能會遺失資料)。 容錯移轉目標將會接管主要角色，並復原每個資料庫的副本，然後讓這兩個資料庫連線，做為新的主要資料庫。 在任一個剩餘的次要複本上，會暫停每個次要資料庫，到手動繼續為止。 當之前的主要複本變成可用複本時，會切換到次要角色，且其資料庫會變成暫停的次要資料庫。  
  
> [!NOTE]  
>  只要容錯移轉目標接受了命令，就會傳回容錯移轉命令。 不過，在可用性群組完成容錯移轉之後，會以非同步方式復原資料庫。  
  
 如需限制的資訊，必要條件和建議的強制容錯移轉以及強制容錯移轉的影響，對先前主要資料庫在可用性群組中，請參閱[執行強制手動容錯移轉的可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).  
  
 ADD LISTENER **'***dns_name***' (** \<add_listener_option > **)**  
 為這個可用性群組定義新的可用性群組接聽程式。 只有主要複本上才支援。  
  
> [!IMPORTANT]  
>  建立第一個接聽程式之前，我們強烈建議您先閱讀[建立或設定可用性群組接聽程式 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
>   
>  針對給定的可用性群組建立接聽程式之後，我們強烈建議您執行以下操作：  
>   
>  -   要求網路管理員將接聽程式的 IP 位址保留為專用。  
> -   將接聽程式的 DNS 主機名稱提供給應用程式開發人員，以便在要求與這個可用性群組進行用戶端連接時，用於連接字串中。  
  
 *dns 名稱*  
 指定可用性群組接聽程式的 DNS 主機名稱。 接聽程式的 DNS 名稱在網域和 NetBIOS 中都必須是唯一的。  
  
 *dns_name*是字串值。 此名稱只能包含英數字元、虛線 (-) 和連字號 (_) (順序不拘)。 DNS 主機名稱不區分大小寫。 長度上限是 63 個字元。  
  
 我們建議您指定一個有意義的字串。 例如，如果是名為 `AG1`的可用性群組，有意義的 DNS 主機名稱會是 `ag1-listener`。  
  
> [!IMPORTANT]  
>  NetBIOS 只會辨識 DNS 名稱中的前 15 個字元。 如果您有兩個由相同 Active Directory 所控制的 WSFC 叢集，而且嘗試使用超過 15 個字元的名稱以及完全相同的 15 個字元前置詞，在這兩個叢集中建立可用性群組接聽程式，就會收到一則錯誤，指出系統無法讓虛擬網路名稱資源上線。 如需有關 DNS 名稱之前置詞命名規則的詳細資訊，請參閱＜ [指派網域名稱](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx)＞。  
  
 在加入可用性群組  
 加入*分散式的可用性群組*。 當您建立分散式的可用性群組時，可用性群組建立所在的叢集上為主要可用性群組。 聯結分散式的可用性群組之可用性群組是次要可用性群組。  
  
 \<ag_name >  
 指定名稱的可用性群組會組成一個分散式的可用性群組的一半。  
  
 接聽程式**='**TCP**://***系統位址***:***連接埠***'**  
 指定可用性群組相關聯的接聽程式的 URL 路徑。  
  
 接聽程式子句是必要的。  
  
 **'**TCP**://***系統位址***:***連接埠***'**  
 指定的 URL 相關聯的可用性群組接聽程式。 URL 參數如下所示：  
  
 *system-address*  
 這是字串，例如系統名稱、 完整的網域名稱或 IP 位址，可明確識別接聽程式。  
  
 *port*  
 為可用性群組的鏡像端點相關聯的通訊埠編號。 請注意，這不是接聽程式的連接埠。  
  
 AVAILABILITY_MODE  **=**  {SYNCHRONOUS_COMMIT |ASYNCHRONOUS_COMMIT}  
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
  
 不支援自動容錯移轉至次要可用性群組。  
  
 SEEDING_MODE **=**  {自動 |手動}  
 指定如何次要可用性群組會一開始植入。  
  
 AUTOMATIC  
 啟用自動植入。 這個方法會在網路上，植入次要可用性群組。 這個方法不需要備份和還原的次要可用性群組之複本的主要資料庫複本。  
  
 MANUAL  
 指定手動植入。 此方法需要您在主要複本上建立資料庫的備份，並手動還原的次要可用性群組複本上備份。  
  
 可用性群組上，修改  
 修改任何分散式的可用性群組的可用性群組設定。 若要修改可用性群組的清單包含可用性群組名稱和 WITH （…） 子句，每個可用性群組。  
  
> [!IMPORTANT]  
>  此命令必須在主要可用性群組和次要可用性群組執行個體上重複。  
  
 授與建立任何資料庫  
 允許可用性群組建立資料庫的主要複本，支援直接植入代表 (SEEDING_MODE = AUTOMATIC)。 此參數應支援直接植入該次要資料庫加入可用性群組之後每個次要複本上執行。  需要 CREATE ANY DATABASE 權限。  
  
 拒絕建立任何資料庫  
 移除可用性群組能夠建立代表主要複本的資料庫。  
  
 \<add_listener_option >  
 ADD LISTENER 可接受下列其中一個選項：  
  
 使用 DHCP [ON { **('***four_part_ipv4_address***'、'***four_part_ipv4_mask***')** }]  
 指定可用性群組接聽程式將會使用動態主機設定通訊協定 (DHCP)。  或者，使用 ON 子句以識別將建立此接聽程式的網路。 DHCP 受限於單一子網路，這個子網路用於可用性群組中主控可用性複本的每個伺服器執行個體。  
  
> [!IMPORTANT]  
>  不建議在實際執行環境中使用 DHCP。 如果有停機時間且 DHCP IP 租用到期，則需要額外的時間來註冊與接聽程式 DNS 名稱相關聯的新 DHCP 網路 IP 位址，而影響用戶端連接。 但是，DHCP 適合用於設定開發和測試環境，以驗證可用性群組的基本功能，也適合與應用程式整合。  
  
 例如：  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 IP **(** { **('***four_part_ipv4_address***'、'***four_part_ipv4_mask* **')** | **('***ipv6_address***')** } [ **，** ... *n*  ] **)** [ **，**連接埠 **=**  *listener_port*]  
 指定可用性群組接聽程式將使用一個或多個靜態 IP 位址，而不使用 DHCP。 若要建立跨多個子網路的可用性群組，接聽程式組態中每個子網路都需要一個靜態 IP 位址。 對於給定的子網路，靜態 IP 位址可以是 IPv4 位址或 IPv6 位址。 請與網路系統管理員連絡以取得將主控新可用性群組的可用性複本之每個子網路的靜態 IP 位址。  
  
 例如：  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *four_part_ipv4_address*  
 指定可用性群組接聽程式的 IPv4 四部分位址。 例如， `10.120.19.155`。  
  
 *four_part_ipv4_mask*  
 指定可用性群組接聽程式的 IPv4 四部分遮罩。 例如， `255.255.254.0`。  
  
 *ipv6_address*  
 指定可用性群組接聽程式的 IPv6 位址。 例如， `2001::4898:23:1002:20f:1fff:feff:b3a3`。  
  
 連接埠 **=**  *listener_port*  
 指定的連接埠號碼 —*listener_port*，WITH IP 子句所指定的可用性群組接聽程式所使用。 PORT 為選擇性。  
  
 支援預設通訊埠編號 1433。 但是，如果您有安全考量，我們建議您使用不同的通訊埠編號。  
  
 例如： `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
 MODIFY LISTENER **'***dns_name***' (** \<modify_listener_option > **)**  
 修改這個可用性群組的現有可用性群組接聽程式。 只有主要複本上才支援。  
  
 \<modify_listener_option >  
 MODIFY LISTENER 可接受下列其中一個選項：  
  
 新增 IP { **('***four_part_ipv4_address***'、'***four_part_ipv4_mask***')**  |  **('**dns_name*ipv6_address***')** }  
 將指定的 IP 位址加入至可用性群組接聽程式所指定*dns_name*。  
  
 連接埠 **=**  *listener_port*  
 請參閱本節稍早有關這個引數的描述。  
  
 重新啟動接聽程式**'***dns_name***'**  
 重新啟動與指定的 DNS 名稱關聯的接聽程式。 只有主要複本上才支援。  
  
 移除接聽程式**'***dns_name***'**  
 移除與指定的 DNS 名稱關聯的接聽程式。 只有主要複本上才支援。  
  
 OFFLINE  
 讓線上的可用性群組離線。 同步認可資料庫不會有資料遺失。  
  
 在可用性群組離線之後，其資料庫就無法供用戶端使用，而且您無法讓可用性群組恢復上線。 因此，將可用性群組資源移轉至新的 WSFC 叢集時，僅在跨叢集移轉 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 期間使用 OFFLINE 選項。  
  
 如需詳細資訊，請參閱[需要可用性群組離線 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md).  
  
## <a name="prerequisites-and-restrictions"></a>必要條件和限制  
 如需資訊的必要條件和限制可用性複本以及其主機伺服器執行個體和電腦上，請參閱[必要條件、 限制和建議的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).  
  
 如需可用性群組 TRANSACT-SQL 陳述式有關限制的詳細資訊，請參閱[概觀的 TRANSACT-SQL 陳述式的 Alwayson 可用性群組 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md).  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
  
###  <a name="Join_Secondary_Replica"></a> A. 將次要複本加入至可用性群組  
 下列範例會將您所連接的次要複本加入至 `AccountsAG` 可用性群組。  
  
```  
ALTER AVAILABILITY GROUP AccountsAG JOIN;  
GO  
```  
  
###  <a name="Force_Failover"></a> B. 強制容錯移轉可用性群組  
 下列範例會將 `AccountsAG` 可用性群組強制容錯移轉至您所連接的次要複本。  
  
```  
ALTER AVAILABILITY GROUP AccountsAG FORCE_FAILOVER_ALLOW_DATA_LOSS;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [卸除可用性群組 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [sys.availability_replicas &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.availability_groups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [疑難排解 Always On 可用性群組組態 &#40;SQL Server &#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性群組接聽程式、用戶端連接及應用程式容錯移轉 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

