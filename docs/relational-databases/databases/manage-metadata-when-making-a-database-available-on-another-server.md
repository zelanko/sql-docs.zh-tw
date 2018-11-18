---
title: 管理在另一部伺服器上提供資料庫時所需的中繼資料 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- cross-database queries [SQL Server]
- logins [SQL Server], recreating on another server instance
- triggers [SQL Server], DLL
- user-defined error messages [SQL Server]
- permissions [SQL Server], metadata access
- Full-Text Engine [SQL Server]
- metadata [SQL Server], databases available to other instances
- jobs [SQL Server Agent], recreating on another server instance
- failover [SQL Server], managing metadata
- event notifications [SQL Server], metadata
- database mirroring [SQL Server], metadata
- startup options [SQL Server]
- restoring [SQL Server], onto another server instance
- linked servers [SQL Server], metadata
- WMI Provider for Server Events, metadata
- attaching databases [SQL Server]
- log shipping [SQL Server], metadata
- encryption [SQL Server], metadata
- server configuration [SQL Server]
- distributed queries [SQL Server], metadata
- extended stored procedures [SQL Server], metadata
- credentials [SQL Server], metadata
- copying databases
ms.assetid: 5d98cf2a-9fc2-4610-be72-b422b8682681
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8480a8b8f3889a1686d29bcd3858ee3921383cd
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559467"
---
# <a name="manage-metadata-when-making-a-database-available-on-another-server"></a>管理在另一部伺服器上提供資料庫時所需的中繼資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本文與下列情況有關：  
  
-   設定 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 可用性群組的可用性複本。  
  
-   設定資料庫的資料庫鏡像。  
  
-   當您準備在記錄傳送組態中變更主要和次要伺服器的角色時。  
  
-   將資料庫還原至另一個伺服器執行個體。  
  
-   在另一個伺服器執行個體上附加資料庫的副本。  
  
 某些應用程式會相依於超出單一使用者資料庫範圍之外的資訊、實體和/或物件。 一般而言，應用程式相依於 **master** 和 **msdb** 資料庫以及使用者資料庫。 如果有資料庫正確運作所需的任何項目儲存在使用者資料庫外部，則必須設法讓目的地伺服器執行個體也能提供。 例如，應用程式的登入在 **master** 資料庫中儲存為中繼資料，就必須在目的地伺服器上加以重新建立。 如果應用程式或資料庫維護計畫相依於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，而其中繼資料儲存於 **msdb** 資料庫，則必須在目的地伺服器執行個體上重新建立那些作業。 同樣的，伺服器層級觸發程序的中繼資料會儲存在 **master**中。  
  
 當您將應用程式的資料庫移動到其他伺服器執行個體時，您必須在目的地伺服器執行個體上重新建立 **master** 和 **msdb** 中的相依實體及物件的所有中繼資料。 例如，如果資料庫應用程式使用伺服器層級觸發程序，僅在新系統上附加或還原資料庫是不夠的。 除非您以手動方式為 **master** 資料庫中的那些觸發程序重新建立中繼資料，否則資料庫無法如預期一般運作。  
  
##  <a name="information_entities_and_objects"></a> 儲存在使用者資料庫外部的資訊、實體和物件  
 本文其餘的篇幅將摘要說明在其他伺服器執行個體上提供資料庫時，可能對該資料庫造成影響的潛在問題。 您可能需要重新建立下列清單列出的其中一個或多個資訊、實體或物件類型。 若要查看摘要，請按一下各項目的連結。  
  
-   [伺服器組態設定](#server_configuration_settings)  
  
-   [認證](#credentials)  
  
-   [跨資料庫查詢](#cross_database_queries)  
  
-   [資料庫擁有權](#database_ownership)  
  
-   [分散式查詢/連結的伺服器](#distributed_queries_and_linked_servers)  
  
-   [加密的資料](#encrypted_data)  
  
-   [使用者自訂錯誤訊息](#user_defined_error_messages)  
  
-   [事件通知和 Windows Management Instrumentation (WMI) 事件 (伺服器層級)](#event_notif_and_wmi_events)  
  
-   [擴充預存程序](#extended_stored_procedures)  
  
-   [Full-Text Engine for SQL Server 屬性](#ifts_service_properties)  
  
-   [作業](#jobs)  
  
-   [登入](#logins)  
  
-   [Permissions](#permissions)  
  
-   [複寫設定](#replication_settings)  
  
-   [Service Broker 應用程式](#sb_applications)  
  
-   [啟動程序](#startup_procedures)  
  
-   [觸發程序 (伺服器層級)](#triggers)  
  
##  <a name="server_configuration_settings"></a> Server Configuration Settings  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本會選擇性地安裝並啟動主要服務與功能。 這可有助於減少系統易受攻擊的介面區。 在新安裝的預設組態中，許多功能都不會啟用。 如果資料庫仰賴預設關閉的任何服務或功能，您就必須在目的地伺服器執行個體上啟用這項服務或功能。  
  
 如需設定和啟用或停用服務或功能的詳細資訊，請參閱[伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
  
##  <a name="credentials"></a> 認證  
 認證是包含驗證資訊的記錄，該項資訊是連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]外部資源時所需的資訊。 大部分認證由 Windows 登入和密碼組成。  
  
 如需此功能的詳細資訊，請參閱[認證 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
> **注意︰**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶使用認證。 若要了解 Proxy 帳戶的認證識別碼，請使用 [sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md) 系統資料表。  
  
  
##  <a name="cross_database_queries"></a> Cross-Database Queries  
 DB_CHAINING 和 TRUSTWORTHY 資料庫選項預設是 OFF。 如果原始資料庫的其中一個選項設定為 ON，您就必須在目的地伺服器執行個體的資料庫上啟用該選項。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
 附加與卸離作業會停用資料庫的跨資料庫擁有權鏈結。 如需如何啟用鏈結的相關資訊，請參閱[跨資料庫擁有權鏈結伺服器組態選項](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)。  
  
 如需詳細資訊，另請參閱[設定鏡像資料庫可使用 Trustworthy 屬性 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)。  
  
  
##  <a name="database_ownership"></a> Database Ownership  
 當資料庫在另一部電腦上還原時，起始還原作業的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 Windows 使用者會自動變成新資料庫的擁有者。 還原資料庫時，系統管理員或新的資料庫擁有者可以變更資料庫擁有權。  
  
##  <a name="distributed_queries_and_linked_servers"></a> 分散式查詢和連結的伺服器  
 OLE DB 應用程式支援分散式查詢和連結的伺服器。 分散式查詢會從相同或不同電腦上的多重異質資料來源存取資料。 連結伺服器的組態可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對遠端伺服器上的 OLE DB 資料來源執行命令。 如需這些功能的詳細資訊，請參閱[連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)。  
  
  
##  <a name="encrypted_data"></a> Encrypted Data  
 如果您在另一個伺服器執行個體上提供的可用資料庫包含加密的資料，而且資料庫主要金鑰受到原始伺服器的服務主要金鑰保護時，可能就必須重新建立服務主要金鑰加密。 *「資料庫主要金鑰」* 是一個用來保護加密資料庫中憑證私密金鑰和非對稱金鑰的對稱金鑰。 建立資料庫主要金鑰時，會利用三重 DES 演算法和使用者提供的密碼來加密資料主要金鑰。  
  
 若要在伺服器執行個體上啟用資料庫主要金鑰的自動解密，就要使用服務主要金鑰來加密此金鑰的副本。 這個加密的副本會同時存放在資料庫和 **master**中。 通常，每當主要金鑰變更時，儲存在 **master** 中的副本便會以無訊息模式更新。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會先嘗試使用執行個體的服務主要金鑰來解密資料庫主要金鑰。 如果該解密失敗， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會從認證存放區中搜尋主要金鑰認證，這些主要金鑰認證具有與它需要其主要金鑰之資料庫相同的家族 GUID。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試利用每個相符的認證來將資料庫主要金鑰解密，直到解密成功或沒有其他認證為止。 未以服務主要金鑰加密的主要金鑰必須使用 OPEN MASTER KEY 陳述式和密碼來開啟。  
  
 當加密的資料庫複製、還原或附加至新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時，以服務主要金鑰加密的資料庫主要金鑰副本並不會存放在目的地伺服器執行個體的 **master** 中。 您必須在目的地伺服器執行個體上，開啟資料庫的主要金鑰。 若要開啟主要金鑰，請執行下列陳述式：OPEN MASTER KEY DECRYPTION BY PASSWORD **='**_密碼_**'**。 建議您接著執行下列陳述式來啟用資料庫主要金鑰的自動解密：ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY。 這個 ALTER MASTER KEY 陳述式會將以服務主要金鑰加密的資料庫主要金鑰副本提供給伺服器執行個體。 如需詳細資訊，請參閱 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md) 和 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。  
  
 如需如何啟用鏡像資料庫之資料庫主要金鑰的自動解密相關資訊，請參閱[設定加密鏡像資料庫](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)。  
  
 如需詳細資訊，請參閱：  
  
-   [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [設定加密鏡像資料庫](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [在兩部伺服器上建立相同的對稱金鑰](../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
##  <a name="user_defined_error_messages"></a> User-defined Error Messages  
 使用者定義錯誤訊息位於 [sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 目錄檢視中。 此目錄檢視會存放在 **master**內。 如果資料庫應用程式仰賴使用者定義錯誤訊息，而且此資料庫可在另一個伺服器執行個體上使用時，請使用 [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md) ，在目的地伺服器執行個體上加入這些使用者定義訊息。  

  
##  <a name="event_notif_and_wmi_events"></a> Event Notifications and Windows Management Instrumentation (WMI) Events (at Server Level)  
  
### <a name="server-level-event-notifications"></a>伺服器層級事件通知  
 伺服器層級事件通知會存放在 **msdb**中。 因此，如果資料庫應用程式依賴伺服器層級事件通知，就必須在目的地伺服器執行個體上重新建立該事件通知。 若要檢視伺服器執行個體上的事件通知，請使用 [sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) 目錄檢視。 如需詳細資訊，請參閱 [Event Notifications](../../relational-databases/service-broker/event-notifications.md)。  
  
 此外，事件通知是使用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]進行傳送。 包含服務的資料庫中不包括內送訊息路由。 但是，外顯路由會儲存在 **msdb**中。 如果服務使用 **msdb** 資料庫中的外顯路由將內送訊息傳送至服務，當您在不同執行個體中附加資料庫時，就必須重新建立此路由。  
  
### <a name="windows-management-instrumentation-wmi-events"></a>Windows Management Instrumentation (WMI) 事件  
 WMI Provider for Server Events 可讓您使用 Windows Management Instrumentation (WMI) 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中監視事件。 如果伺服器層級事件要透過資料庫所依賴的 WMI 提供者來公開，則任何依賴此事件的應用程式必須定義有目的地伺服器執行個體的電腦。 WMI 事件提供者會以 **msdb**中定義的目標服務來建立事件通知。  
  
> **注意：** 如需詳細資訊，請參閱 [伺服器事件的 WMI 提供者概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)。  
  
 **若要使用 SQL Server Management Studio 建立 WMI 警示**  
  
-   [建立 WMI 事件警示](../../ssms/agent/create-a-wmi-event-alert.md)  
  
### <a name="how-event-notifications-work-for-a-mirrored-database"></a>鏡像資料庫如何使用事件通知  
 根據定義，若涉及鏡像資料庫時，跨資料庫傳送事件通知為遠端作業，因為鏡像資料庫可以容錯移轉。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會以 *「鏡像路由」*(Mirrored Route) 的形式，為鏡像資料庫提供特殊支援。 鏡像路由有兩個位址：一個是主體伺服器執行個體的位址，另一個是鏡像伺服器執行個體的位址。  
  
 透過設定鏡像路由，可以讓 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由知道資料庫鏡像的存在。 鏡像路由可讓 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 將交談明確地重新導向至目前的主體伺服器執行個體。 例如，假設有一個服務 Service_A 是由鏡像資料庫 Database_A 所裝載。 假設您需要另一個服務 Service_B (由 Database_B 所裝載) 與 Service_A 對話。 為了要讓這個對話可行，Database_B 必須包含 Service_A 的鏡像路由。 此外，Database_A 也必須包含與 Service_B 之間的非鏡像 TCP 傳輸路由，此路由在容錯移轉之後會維持有效狀態，與本機路由不同。 這些路由可讓 ACK 在容錯移轉之後傳送回來。 因為傳送者的服務永遠是以相同方式來命名，所以路由必須指定 Broker 執行個體。  
  
 不論鏡像資料庫中的服務是起始端服務，或是目標服務，鏡像路由的需求都適用：  
  
-   如果目標服務在鏡像資料庫中，則起始端服務必須有回到目標的鏡像路由。 不過，目標可以有回到起始端的一般路由。  
  
-   如果起始端服務在鏡像資料庫中，則目標服務必須有回到起始端的鏡像路由，才能傳送收條與回應。 不過，起始端可以有指向目標的一般路由。  
  
  
##  <a name="extended_stored_procedures"></a> Extended Stored Procedures  
  
> **重要！** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CLR 整合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 。  
  
 擴充預存程序是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擴充預存程序 API 進行程式設計的。 **sysadmin** 固定伺服器角色的成員可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來註冊擴充預存程序並授與使用者執行該程序的權限。 擴充預存程序只能加入 **master** 資料庫。  
  
 擴充預存程序會直接在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的位址空間中執行，而且它們可能會產生降低伺服器效能和可靠性的記憶體遺漏或其他問題。 您應考慮將擴充預存程序與參考資料儲存在不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中。 同時應考慮使用分散式查詢來存取資料庫。  
  
  > [!IMPORTANT]
  > 將擴充預存程序加入伺服器並將 EXECUTE 權限授與其他使用者之前，系統管理員應徹底檢閱每個擴充預存程序，確定其中不含任何有害或惡意的程式碼。  
  
 如需詳細資訊，請參閱 [GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)、[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md) 和 [REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)。  
  
  
##  <a name="ifts_service_properties"></a> Full-Text Engine for SQL Server Properties  
 全文檢索引擎的屬性是由 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)所設定。 請確定目的地伺服器執行個體具有這些屬性的必要設定。 如需這些屬性的詳細資訊，請參閱 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)。  
  
 此外，如果[斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)元件或[全文檢索搜尋篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)元件在原始和目的地伺服器執行個體上具有不同的版本，全文檢索索引和查詢就可能會有不同的行為方式。 而且， [同義字](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md) 會存放在執行個體專用的檔案中。 您必須將這些檔案的副本傳送至目的地伺服器執行個體上的對等位置，或在新執行個體上重新建立這些檔案。  
  
> **注意：** 當您將包含全文檢索目錄檔案的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體時，系統就會從先前的位置附加這些目錄檔案以及其他資料庫檔案，此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同。 如需詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
 如需詳細資訊，請參閱：  
  
-   [備份並還原全文檢索目錄與索引。](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   [資料庫鏡像和全文檢索目錄 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  

  
##  <a name="jobs"></a> 作業  
 如果資料庫仰賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，您就必須在目的地伺服器執行個體上重新建立這些作業。 作業會仰賴所屬的環境。 如果您打算在目的地伺服器執行個體上重新建立現有的作業，可能必須修改目的地伺服器執行個體，以便符合該作業在原始伺服器執行個體上的環境。 下列環境因素相當重要：  
  
-   作業使用的登入  
  
     若要建立或執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，您必須先將作業所需的任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入加入至目的地伺服器執行個體。 如需詳細資訊，請參閱 [設定使用者可建立及管理 SQL Server Agent 作業](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動帳戶  
  
     服務啟動帳戶會定義 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Agent 用來執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 帳戶及其網路權限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會以指定的使用者帳戶執行。 Agent 服務的內容會影響作業及其執行環境的設定。 此帳戶必須具有作業所需之資源 (例如，網路共用) 的存取權。 如需如何選取和修改服務啟動帳戶的相關資訊，請參閱 [選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)。  
  
     為了正確運作，服務啟動帳戶必須設定成具有正確的網域、檔案系統和登錄權限。 此外，作業可能會需要使用必須針對服務帳戶設定的共用網路資源。 如需相關資訊，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務 (與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的特定執行個體相關聯) 具有自己的登錄區，而且它的作業通常會相依於此登錄區中的一或多項設定。 為了如預期方式運作，作業會需要使用這些登錄設定。 如果您使用指令碼在另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務中重新建立作業，其登錄可能不會有該作業的正確設定。 為了讓重新建立的作業在目的地伺服器執行個體上正確運作，原始和目的地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務都應該具有相同的登錄設定。  
  
    > [!CAUTION]  
    >  如果目前的設定是其他作業所需，在目的地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務上變更登錄設定以便處理重新建立的作業可能會產生問題。 此外，不當編輯登錄可能會造成系統嚴重受損。 在變更登錄之前，我們建議您先備份電腦上所有重要的資料。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 可定義指定之作業步驟的安全性內容。 為了讓作業在目的地伺服器執行個體上執行，您必須在該執行個體上手動重新建立此作業所需的所有 Proxy。 如需詳細資訊，請參閱 [建立 SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md) 和 [疑難排解使用 Proxy 的多伺服器作業](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)。  
  
 如需詳細資訊，請參閱：  
  
-   [實作作業](../../ssms/agent/implement-jobs.md)  
  
-   [角色切換後針對登入和作業進行管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md) (適用於資料庫鏡像)  
  
-   [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) (當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時)  
  
-   [設定 SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md) (當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體時)  
  
-   [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)  
  
 **若要檢視現有的作業及其屬性**  
  
-   [監視作業活動](../../ssms/agent/monitor-job-activity.md)  
  
-   [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)  
  
-   [檢視作業步驟資訊](../../ssms/agent/view-job-step-information.md)  
  
-   [dbo.sysjobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
  
 **若要建立作業**  
  
-   [建立作業](../../ssms/agent/create-a-job.md)  
  
-   [建立作業](../../ssms/agent/create-a-job.md)  
  
#### <a name="best-practices-for-using-a-script-to-re-create-a-job"></a>使用指令碼來重新建立作業的最佳作法  
 我們建議您先編寫簡單作業的指令碼、在其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務上重新建立作業，然後執行該作業，看看是否如預期方式運作。 這項做法可讓您識別不相容性並嘗試加以解決。 如果以指令碼編寫的作業無法如預期方式在新環境中運作，建議您建立可在該環境下正確運作的對等作業。  
  

##  <a name="logins"></a> 登入  
 登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體需要有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 此登入是用於驗證處理序，可確認主體是否能連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 在伺服器執行個體上未定義或定義不正確之對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的資料庫使用者無法登入此執行個體。 這類使用者就是伺服器執行個體上的資料庫 *「被遺棄使用者」* (Orphaned User)。 當資料庫還原、附加或複製到不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體後，資料庫使用者就可能會成為被遺棄使用者。  
  
 若要在原始資料庫副本中產生部分或所有物件的指令碼，您可以使用「產生指令碼精靈」，然後在 **[選擇指令碼選項]** 對話方塊中，將 **[編寫登入的指令碼]** 選項設定為 **[True]**。  
  
> **注意：** 如需如何設定鏡像資料庫登入的資訊，請參閱[設定資料庫鏡像或 AlwaysOn 可用性群組的登入帳戶 (SQL Server)](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md) 和[角色切換後針對登入和作業進行管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)。  
  
  
##  <a name="permissions"></a> Permissions  
 當您在其他伺服器執行個體上提供資料庫時，可能會影響下列類型的權限。  
  
-   系統物件的 GRANT、REVOKE 或 DENY 權限  
  
-   伺服器執行個體的 GRANT、REVOKE 或 DENY 權限 (*「伺服器層級權限」*)  
  
### <a name="grant-revoke-and-deny-permissions-on-system-objects"></a>系統物件的 GRANT、REVOKE 及 DENY 權限  
 系統物件 (例如，預存程序、擴充預存程序、函數和檢視) 的權限會存放在 **master** 資料庫中，而且您必須在目的地伺服器執行個體上設定這些權限。  
  
 若要在原始資料庫副本中產生部分或所有物件的指令碼，您可以使用「產生指令碼精靈」，然後在 **[選擇指令碼選項]** 對話方塊中，將 **[編寫物件層級權限的指令碼]** 選項設定為 **[True]**。  
  
   > [!IMPORTANT]
   > 當您在編寫登入的指令碼時，密碼並不會編寫在指令碼中。 如果您具有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入，就必須修改目的地上的指令碼。  
  
 您可以在 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 目錄檢視中看到系統物件。 您可以在 **master** 資料庫的 [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 目錄檢視中，看到系統物件的權限。 如需查詢這些目錄檢視和授與系統物件權限的詳細資訊，請參閱 [GRANT 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)。 如需詳細資訊，請參閱 [REVOKE 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md) 和 [DENY 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)。  
  
### <a name="grant-revoke-and-deny-permissions-on-a-server-instance"></a>伺服器執行個體的 GRANT、REVOKE 及 DENY 權限  
 伺服器範圍的權限會存放在 **master** 資料庫中，而且您必須在目的地伺服器執行個體上設定這些權限。 如需伺服器執行個體之伺服器權限的詳細資訊，請查詢 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 目錄檢視。如需伺服器主體的詳細資訊，請查詢 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 目錄檢視。如需伺服器角色之成員資格的詳細資訊，請查詢 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 目錄檢視。  
  
 如需詳細資訊，請參閱 [GRANT 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)、[REVOKE 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md) 和 [DENY 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)。  
  
#### <a name="server-level-permissions-for-a-certificate-or-asymmetric-key"></a>憑證或非對稱金鑰的伺服器層級權限  
 您無法直接將伺服器層級權限授與憑證或非對稱金鑰。 不過，伺服器層級權限會授與專為特定憑證或非對稱金鑰建立的對應登入。 因此，需要伺服器層級權限的每個憑證或非對稱金鑰都會需要自己的 *「憑證對應登入」* 或 *「非對稱金鑰對應登入」*。 若要授與憑證或非對稱金鑰的伺服器層級權限，請將這些權限授與對應的登入。  
  
> **注意：** 對應的登入只會用於授權以對應憑證或非對稱金鑰簽署的程式碼。 對應的登入無法用於驗證。  
  
 對應的登入及其權限都位於 **master**中。 如果憑證或非對稱金鑰位於 **master**以外的資料庫中，您就必須在 **master** 中重新建立此項目並將它對應至登入。 如果您將資料庫移動、複製或還原至另一個伺服器執行個體，就必須在目的地伺服器執行個體的 **master** 資料庫中重新建立其憑證或非對稱金鑰、將它對應至登入，然後將所需的伺服器層級權限授與此登入。  
  
 **若要建立憑證或非對稱金鑰**  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
 **若要將憑證或非對稱金鑰對應至登入**  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 **若要將權限指派給對應的登入**  
  
-   [GRANT 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)  
  
 如需憑證和非對稱金鑰的詳細資訊，請參閱＜ [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)＞。  
  
## <a name="trustworthy-property"></a>TRUSTWORHTY 屬性
TRUSTWORHTY 資料庫屬性是用來指定 SQL Server 執行個體是否信任資料庫及其中的內容。 附加資料庫時，根據預設且為了安全起見，此選項會設定為 OFF，即使此選項在原始伺服器上設定為 ON 也一樣。 如需這個屬性的詳細資訊，請參閱 [TRUSTWORTHY 資料庫屬性](../security/trustworthy-database-property.md)；如需開啟這個選項的資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  


##  <a name="replication_settings"></a> Replication Settings  
 如果您將複寫資料庫的備份還原到另一個伺服器或資料庫，將無法保留複寫設定。 在此情況下，您必須在還原備份之後，重新建立所有發行集和訂閱。 若要讓此程序更簡單，請針對目前的複寫設定和啟用及停用複寫，建立指令碼。 若要協助重新建立複寫設定，請複製這些指令碼並變更伺服器名稱參考，以便針對目的地伺服器執行個體運作。  
  
 如需詳細資訊，請參閱[備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)、[資料庫鏡像和複寫 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md) 和[記錄傳送和複寫 &#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)。  
  
  
##  <a name="sb_applications"></a> Service Broker Applications  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 應用程式的許多部分都會隨資料庫移動。 不過，此應用程式的某些部分則必須在新位置中重新建立或重新設定。  根據預設且為了安全起見，從其他伺服器附加資料庫時，*is_broker_enabled* 和 *is_honoor_broker_priority_on* 的選項都會設定為 OFF。 如需如何將這些選項設定為 ON 的資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
  
##  <a name="startup_procedures"></a> Startup Procedures  
 啟動程序是指標示為自動執行而且每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時都會執行的預存程序。 如果資料庫仰賴任何啟動程序，您就必須在目的地伺服器執行個體上定義這些程序，並將它們設定為啟動時自動執行。  

  
##  <a name="triggers"></a> Triggers (at Server Level)  
 DDL 觸發程序會引發預存程序，以便回應各種資料定義語言 (DDL) 事件。 這些事件主要對應至以 CREATE、ALTER 和 DROP 關鍵字開頭的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 執行類似 DDL 作業的某些系統預存程序也可能引發 DDL 觸發程序。  
  
 如需有關這項功能的詳細資訊，請參閱＜ [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md)＞。  
  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫](../../relational-databases/databases/contained-databases.md)   
 [複製資料庫至其他伺服器](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [容錯移轉至記錄傳送次要 &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)   
 [資料庫鏡像工作階段期間的角色切換 &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [設定加密鏡像資料庫](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)   
 [孤立的使用者疑難排解 &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
