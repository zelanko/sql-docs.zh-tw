---
title: 使用 Oracle CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04be5896-2301-45f5-a8ce-5f4ef2b69aa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2f8854dba3c1d998d572481c285ee75dc933e480
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771178"
---
# <a name="working-with-the-oracle-cdc-service"></a>使用 Oracle CDC 服務
  本章節描述 Oracle CDC 服務的一些重要概念。 本章節包含的概念如下：  
  
-   [MSXDBCDC 資料庫](#BKMK_MSXDBCDC)  
  
     本章節描述此資料庫中所包含的資料表以及這對於 CDC 的重要性。  
  
-   [CDC 資料庫](#BKMK_CDCdatabase)  
  
     本章節提供 CDC 資料庫的簡短描述。 這些資料庫是使用 Oracle CDC 設計工具主控台所建立。 如需有關 CDC 資料庫的詳細資訊，請參閱 CDC 設計工具主控台安裝所隨附的文件集。  
  
-   [使用命令列來設定 CDC 服務](#BKMK_CommandConfigCDC)  
  
     本章節描述可用於設定 Oracle CDC 服務的命令列命令。  
  
##  <a name="BKMK_MSXDBCDC"></a> MSXDBCDC 資料庫  
 MSXDBCDC (Microsoft 外部資料庫 CDC) 資料庫是一種特殊的資料庫，當搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體使用 Oracle CDC 服務時便需要它。  
  
 這個資料庫的名稱不得變更。 如果名為 MSXDBCDC 的資料庫存在於主機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上而且包含 Oracle CDC 服務所定義之資料表以外的資料表，則不得使用主機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 此資料庫的主要用途如下：  
  
-   當做與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體關聯之 Oracle CDC 服務的登錄。 此資訊會用於服務組態和設計元件，以及支援協調不同節點上相同名稱的多個 CDC 服務 (其中有一個節點為使用中節點)。  
  
-   當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內包含之 Oracle CDC 執行個體的登錄，處理每一個執行個體以及每一個執行個體使用之組態版本的 CDC 服務。 此資訊相當於 master 資料庫中 **sys.databases** 資料表內的 **is_cdc_enabled** 資料行。 CDC 服務會定期掃描 **dbo.xdbcdc_databases** 資料表，以識別對 CDC 組態或對擷取的執行個體清單所做的變更。  
  
-   持有 **sysadmin**擁有的預存程序，有助於建立及維護 CDC 執行個體。 這些類似於用於實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 功能的系統程序。  
  
### <a name="creating-the-msxdbcdc-database"></a>建立 MSXDBCDC 資料庫  
 在可以定義 Oracle CDC 服務之前，必須建立 MSXDBCDC 資料庫。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上只能建立一個 MSXDBCDC 資料庫。 當您為 Oracle CDC 準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫時，便會建立 MSXDBCDC 資料庫。 若要執行這項作業，請使用 Oracle CDC 服務組態主控台，或是執行 CDC 服務組態主控台所產生的建立指令碼。  
  
 此資料庫的擁有者為 Oracle CDC 服務管理員，他可以控制在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之下主控的所有 Oracle CDC 執行個體。  
  
 **另請參閱：**  
  
 [如何準備 SQL Server 以使用 CDC](prepare-sql-server-for-cdc.md)  
  
### <a name="the-msxdbcdc-database-tables"></a>MSXDBCDC 資料庫資料表  
 本節描述 MSXDBCDC 資料庫中的以下資料表。  
  
-   [dbo.xdbcdc_trace](#BKMK_dboxdbcdc_trace)  
  
-   [dbo.xdbcdc_databases](#BKMK_dboxdbcdc_databases)  
  
-   [dbo.xdbcdc_services](#BKMK_dboxdbcdc_services)  
  
###  <a name="BKMK_dboxdbcdc_trace"></a> dbo.xdbcdc_trace  
 此資料表會儲存 Oracle CDC 服務的追蹤資訊。 儲存在這個資料表中的資訊包括顯著的狀態變更及追蹤記錄。  
  
 Oracle CDC 服務會將錯誤記錄和某些資訊記錄寫入 Windows 事件記錄檔和追蹤資料表中。 在某些情況下可能無法存取追蹤資料表，此時可從事件記錄檔存取錯誤資訊。  
  
 以下描述 **dbo.xdbcdc_trace** 資料表中包含的項目。  
  
|Item|描述|  
|----------|-----------------|  
|timestamp|寫入追蹤記錄的精確 UTC 時間戳記。|  
|type|包含下列其中一個值。<br /><br /> ERROR<br /><br /> INFO<br /><br /> TRACE|  
|node|寫入記錄的節點名稱。|  
|status|狀態資料表使用的狀態碼。|  
|sub_status|狀態資料表使用的子狀態碼。|  
|status_message|狀態資料表使用的狀態訊息。|  
|source|產生追蹤記錄的 Oracle CDC 元件名稱。|  
|text_data|當錯誤或追蹤記錄包含文字裝載時的其他文字資料。|  
|binary_data|當錯誤或追蹤記錄包含二進位裝載時的其他二進位資料。|  
  
 Oracle CDC 執行個體將會根據變更資料表保留原則來刪除舊的追蹤資料表資料列。  
  
###  <a name="BKMK_dboxdbcdc_databases"></a> dbo.xdbcdc_databases  
 此資料表會包含目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 Oracle CDC 資料庫的 CDC 服務名稱。 每個資料庫都會對應到 Oracle CDC 執行個體。 Oracle CDC 服務會使用此資料表來判斷哪些執行個體要啟動或停止，以及哪些執行個體要重新設定。  
  
 下表描述 **dbo.xdbcdc_databases** 資料表中包含的項目。  
  
|Item|描述|  
|----------|-----------------|  
|NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 Oracle 資料庫的名稱。|  
|config_version|對應 CDC 資料庫 **xdbcdc_config** 資料表中上次變更的時間戳記 (UTC)，或是此資料表中目前資料列的時間戳記 (UTC)。<br /><br /> UPDATE 觸發程序會針對這個項目強制使用 GETUTCDATE() 的值。 **config_version** 可讓 CDC 服務識別需要檢查是否有組態變更或啟用/停用的 CDC 執行個體。|  
|cdc_service_name|這個項目會判斷哪一個 Oracle CDC 服務處理選取的 Oracle 資料庫。|  
|已啟用|指出 Oracle CDC 執行個體為使用中 (1) 還是停用 (0) 狀態。 當 Oracle CDC 服務啟動時，只會啟動標示為啟用 (1) 的執行個體。<br /><br /> **注意**：發生無法重試的錯誤時，Oracle CDC 執行個體可能會停用。 在此情況下，必須在解決錯誤之後手動重新啟動執行個體。|  
  
###  <a name="BKMK_dboxdbcdc_services"></a> dbo.xdbcdc_services  
 此資料表列出與主機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體相關聯的 CDC 服務。 CDC 設計工具主控台會使用此資料表來判斷針對本機 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體設定的 CDC 服務清單。 CDC 服務也會使用此資料表來確保只有一個執行中的 Windows 服務會處理給定的 Oracle CDC 服務名稱。  
  
 以下描述 **dbo.xdbcdc_databases** 資料表中包含的擷取狀態項目。  
  
|Item|描述|  
|----------|-----------------|  
|cdc_service_name|Oracle CDC 服務的名稱 (Windows 服務名稱)。|  
|cdc_service_sql_login|Oracle CDC 服務為了連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。 隨即建立名為 cdc_service 的新 SQL 使用者並與這個登入名稱產生關聯，然後針對此服務處理的每一個 CDC 資料庫，將此使用者當做 db_ddladmin、db_datareader 和 db_datawriter 固定資料庫角色的成員加入。|  
|ref_count|這個項目會計算安裝相同 Oracle CDC 服務的電腦數目。 每次加入相同名稱的 Oracle CDC 服務時，這個數目就會遞增，每當移除這類服務時，這個數目就會遞減。 當計數器到達零時，這個資料列會遭到刪除。|  
|active_service_node|目前處理 CDC 服務的 Windows 節點名稱。 當此服務正確停止時，這個資料行會設定為 null，表示不再有使用中的服務。|  
|active_service_heartbeat|這個項目會追蹤目前的 CDC 服務來判斷它是否依然使用中。<br /><br /> 對於固定間隔的使用中 CDC 服務而言，將會使用目前資料庫 UTC 時間戳記來更新這個項目。 預設間隔為 30 秒，但是可以設定間隔。<br /><br /> 當暫止的 CDC 服務偵測到經過設定的間隔時間後並未更新活動訊號時，暫止的服務會嘗試接管使用中的 CDC 服務角色。|  
|選項|這個項目會指定次要選項，例如追蹤或微調。 它會以 **name[=value][; ]** 格式寫入。 選項字串會使用與 ODBC 連接字串相同的語意。 如果選項為布林值 (值為是/否)，此值只能包含名稱。<br /><br /> 追蹤具有下列可能的值：<br /><br /> true<br /><br /> on<br /><br /> false<br /><br /> 關<br /><br /> \<類別名稱> [，類別名稱>]<br /><br /> 預設值為 **false**。<br /><br /> <br /><br /> **service_heartbeat_interval** 是此服務更新 active_service_heartbeat 資料行的時間間隔 (以秒數為單位)。 預設值是 **30**。 最大值為 **3600**。<br /><br /> **service_config_polling_interval** 是 CDC 服務檢查組態變更的輪詢間隔 (以秒數為單位)。 預設值是 **30**。 最大值為 **3600**。<br /><br /> **sql_command_timeout** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的命令逾時。 預設值是 **1**秒。 最大值為 **3600**。|  
||  
  
### <a name="the-msxdbcdc-database-stored-procedures"></a>MSXDBCDC 資料庫預存程序  
 本節描述 MSXDBCDC 資料庫中的以下預存程序。  
  
-   [dbo.xcbcdc_reset_db(資料庫名稱)](#BKMK_dboxcbcdc_reset_db)  
  
-   [dbo.xdbcdc_disable_db(dbname)](#BKMK_dboxdbcdc_disable_db)  
  
-   [dbo.xcbcdc_add_service(svcname,sqlusr)](#BKMK_dboxcbcdc_add_service)  
  
-   [dbo.xdbcdc_start(dbname)](#BKMK_dboxdbcdc_start)  
  
-   [dbo.xdbcdc_stop(dbname)](#BKMK_dboxdbcdc_stop)  
  
###  <a name="BKMK_dboxcbcdc_reset_db"></a> dbo.xcbcdc_reset_db(資料庫名稱)  
 此程序會清除 Oracle CDC 執行個體的資料。 其用途如下：  
  
-   為了重新開始資料擷取並忽略之前的資料，例如在來源資料庫復原之後，或是在某些 Oracle 交易記錄無法使用而停止活動之後。  
  
-   當 CDC 狀態中有損毀情況時 (特別是在任何 cdc.*tables 資料中)。  
  
 **dbo.xcbcdc_reset_db** 程序會執行以下工作：  
  
-   停止 CDC 執行個體 (若為使用中)。  
  
-   截斷變更資料表： **cdc_lsn_mapping** 資料表和 **cdc_ddl_history** 資料表。  
  
-   清除 **cdc_xdbcdc_state** 資料表。  
  
-   清除 **cdc_change_table**之每一個資料列的 start_lsn 資料行。  
  
 若要使用 **dbo.xcbcdc_reset_db** 程序，使用者必須是所指名之 CDC 執行個體資料庫的 **db_owner** 資料庫角色成員，或是 **sysadmin** 或 **serveradmin** 固定伺服器角色的成員。  
  
 如需 CDC 資料表的詳細資訊，請參閱 CDC 設計工具主控台中說明系統內的 *CDC 資料庫* 。  
  
###  <a name="BKMK_dboxdbcdc_disable_db"></a> dbo.xdbcdc_disable_db(dbname)  
 **dbo.xcbcdc_disable_db** 程序會執行以下工作：  
  
-   移除選定 CDC 資料庫中 MSXDBCDC.xdbcdc_databases 資料表的項目。  
  
 若要使用 **dbo.xcbcdc_disable_db** 程序，使用者必須是所指名之 CDC 執行個體的 **db_owner** 資料庫角色成員，或是 **sysadmin** 或 **serveradmin** 固定伺服器角色的成員。  
  
 如需有關 CDC 資料表的詳細資訊，請參閱 CDC 設計工具主控台中說明系統內的＜CDC 資料庫＞。  
  
###  <a name="BKMK_dboxcbcdc_add_service"></a> dbo.xcbcdc_add_service(svcname,sqlusr)  
 **dbo.xcbcdc_add_service** 程序會將項目加入至 **MSXDBCDC.xdbcdc_services** 資料表，並針對 **MSXDBCDC.xdbcdc_services** 資料表中的服務名稱將 1 的遞增值加入 ref_count 資料行。 當 **ref_count** 為 0 時，它會刪除資料列。  
  
 若要使用 **dbo.xcbcdc_add_service\<服務名稱, 使用者名稱>** 程序，使用者必須是所指名之 CDC 執行個體資料庫的 **db_owner** 資料庫角色成員，或是**系統管理員**或 **serveradmin** 固定伺服器角色的成員。  
  
###  <a name="BKMK_dboxdbcdc_start"></a> dbo.xdbcdc_start(dbname)  
 **dbo.xdbcdc_start** 程序會傳送啟動要求給 CDC 服務，此服務會處理選取的 CDC 執行個體來開始變更處理。  
  
 若要使用 **dbo.xcdcdc_start** 程序，使用者必須是 CDC 資料庫的 **db_owner** 資料庫角色成員，或是 **執行個體之** sysadmin **或** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色的成員。  
  
###  <a name="BKMK_dboxdbcdc_stop"></a> dbo.xdbcdc_stop(dbname)  
 **dbo.xdbcdc_stop** 程序會傳送停止要求給 CDC 服務，此服務會處理選取的 CDC 執行個體來停止變更處理。  
  
 若要使用 **dbo.xcdcdc_stop** 程序，使用者必須是 CDC 資料庫的 **db_owner** 資料庫角色成員，或是 **執行個體之** sysadmin **或** serveradmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色的成員。  
  
##  <a name="BKMK_CDCdatabase"></a> CDC 資料庫  
 CDC 服務中使用的每一個 Oracle CDC 執行個體都與稱為 CDC 資料庫的特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關聯。 這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫會在與 Oracle CDC 服務相關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中主控。  
  
 CDC 資料庫包含特殊的 cdc 結構描述。 Oracle CDC 服務會搭配前置詞為 **xdbcdc_** 的資料表名稱使用這個結構描述。 此結構描述的用途是為了安全性和一致性。  
  
 Oracle CDC 執行個體和 CDC 資料庫都是使用 Oracle CDC 設計工具主控台所建立。 如需有關 CDC 資料庫的詳細資訊，請參閱 Oracle CDC 設計工具主控台安裝所隨附的文件集。  
  
##  <a name="BKMK_CommandConfigCDC"></a> 使用命令列來設定 CDC 服務  
 您可以從命令列操作 Oracle CDC 服務程式 (xdbcdcsvc.exe)。 CDC 服務程式是原生 32 位元/64 位元的 Windows 可執行檔。  
  
 **另請參閱**  
  
 [如何使用 CDC 服務命令列介面](how-to-use-the-cdc-service-command-line-interface.md)  
  
### <a name="service-program-commands"></a>服務程式命令  
 本章節描述用來設定 CDC 服務的以下命令。  
  
-   [Config](#BKMK_config)  
  
-   [建立](#BKMK_create)  
  
-   [刪除](#BKMK_delete)  
  
###  <a name="BKMK_config"></a> Config  
 使用 `Config` 可從指令碼更新 Oracle CDC 服務組態。 此命令只能用於更新 CDC 服務組態的特定部分 (例如，只有連接字串，而不知道非對稱金鑰密碼)。 此命令必須由電腦管理員執行。 以下是 `Config` 命令的範例。  
  
```  
"<path>xdbcdcsvc.exe" config  
     <cdc-service-name>  
     [connect= <sql-server-connection-string>]  
     [key= <asym-key-password>]  
     [svcacct= <windows-account> <windows-password>]  
     [sqlacct= <sql-username> <sql-password>]  
  
```  
  
 其中：  
  
 **cdc-service-name** 是要更新的 CDC 服務名稱。 這是必要參數。  
  
 **sql-server-connection-string** 是要更新的連接字串。 如果連接字串包含空格或引號，則必須用雙引號 (") 括住。 放置兩個引號會讓內嵌引號逸出。  
  
 **asym-key-password** 是要更新的密碼。  
  
 **windows-account**和 **windows-password** 為正在更新之服務的 Windows 帳戶認證。  
  
 **sql-username**和 **sql-password** 為正在更新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證認證。 如果 sqlacct 同時有空的使用者名稱和空的密碼，Oracle CDC 服務會使用 Windows 驗證連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **注意**：必須用雙引號 (") 括住任何包含空格或雙引號的參數。 內嵌雙引號必須成對 (例如，若要使用 **"A#B" D** 當作密碼，請輸入 **""A#B"" D"** )。  
  
###  <a name="BKMK_create"></a> 建立  
 使用 `Create` 可從指令碼建立 Oracle CDC 服務。 此命令必須由電腦管理員執行。 以下是 `Create` 命令的範例：  
  
```  
"<path>xdbcdcsvc.exe" create  
     <cdc-service-name>  
     [connect= "<sql-server-connection-string>"]  
     [key= <asym-key-password>]  
     [svcacct <windows-account> <windows-password>]  
     [sqlacct <sql-username> <sql-password>]  
```  
  
 其中：  
  
 **cdc-service-name** 是新建立服務的名稱。 如果已經有這個名稱的服務，此程式會傳回錯誤。 您不應該使用完整名稱或是有空格的名稱。 "/" 和 "\\" 字元在服務名稱中是無效的字元。 這是必要參數。  
  
 **sql-server-connection-string** 是用來連接與新 Oracle CDC 服務相關聯之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接字串。  
  
 **asym-key-password** 是保護非對稱金鑰的密碼，該金鑰是用來儲存來源資料庫的記錄採礦認證。  
  
 **windows-account**和 **windows-password** 是與所建立之 Oracle CDC 服務相關聯的帳戶名稱和密碼。  
  
 **sql-username**和 **sql-password** 是用來連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶名稱和密碼。 如果這兩個參數都是空的，則 Oracle CDC 服務會使用 Windows 驗證連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **注意**：必須用雙引號 (") 括住任何包含空格或雙引號的參數。 內嵌雙引號必須成對 (例如，若要使用 **"A#B" D** 當作密碼，請輸入 **""A#B"" D"** )。  
  
###  <a name="BKMK_delete"></a> Delete  
 使用 `Delete` 可從指令碼完全刪除 Oracle CDC 服務。 此命令必須由電腦管理員執行。 以下是 `Delete` 命令的範例。  
  
```  
"<path>xdbcdcsvc.exe" delete  
    <cdc-service-name>  
  
```  
  
 其中：  
  
 **cdc-service-name** 是要刪除的 CDC 服務名稱。  
  
 **注意**：必須用雙引號 (") 括住任何包含空格或雙引號的參數。 內嵌雙引號必須成對 (例如，若要使用 **"A#B" D** 當作密碼，請輸入 **""A#B"" D"** )。  
  
## <a name="see-also"></a>另請參閱  
 [如何使用 CDC 服務命令列介面](how-to-use-the-cdc-service-command-line-interface.md)   
 [如何準備 SQL Server 以使用 CDC](prepare-sql-server-for-cdc.md)  
