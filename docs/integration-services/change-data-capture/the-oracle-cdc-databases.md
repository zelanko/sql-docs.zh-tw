---
title: "Oracle CDC 資料庫 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a96486e9-f79b-4b24-bfaf-56203dd0e435
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54eb41670979c83b200060128da8564b765bcd5d
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="the-oracle-cdc-databases"></a>Oracle CDC 資料庫
  Oracle CDC 執行個體與目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上同名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫有關聯。 此資料庫稱為 Oracle CDC 資料庫 (或 CDC 資料庫)。  
  
 CDC 資料庫是使用 Oracle CDC 設計工具主控台所建立及設定，而且其中包含以下元素：  
  
-   藉由啟用 SQL Server CDC 的資料庫所建立的 `cdc` 結構描述。  
  
-   Oracle CDC 執行個體使用的一組 **cdc.xdbcdc_xxxx** 資料表。  
  
-   一組空的鏡像資料表，其中包含來源 Oracle 資料庫中擷取的資料表定義。  
  
-   SQL Server CDC 機制產生的一組變更資料表和變更存取函數，與一般非 Oracle 的 SQL Server CDC 中使用的項目相同。  
  
 `cdc` 結構描述一開始僅供 **dbowner** 固定資料庫角色的成員存取。 對變更資料表和變更函數的存取是由與 SQL Server CDC 相同的安全性模型所決定。 如需安全性模型的詳細資訊，請參閱 [安全性模型](http://go.microsoft.com/fwlink/?LinkId=231151)。  
  
## <a name="creating-the-cdc-database"></a>建立 CDC 資料庫  
 在大多數情況下，CDC 資料庫是使用 CDC 設計工具主控台所建立，但是也可以使用透過 CDC 設計工具主控台產生的 CDC 部署指令碼來建立。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員可以視需要變更資料庫設定 (例如儲存體、安全性或可用性等項目)。  
  
 如需使用 CDC 設計工具主控台建立資料庫資料表和必要指令碼的詳細資訊，請參閱 [使用新增執行個體精靈](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)。  
  
## <a name="cdc-database-user-roles"></a>CDC 資料庫使用者角色  
 當建立 CDC 資料庫並啟用 CDC 時，便會在 CDC 資料庫中建立稱為 **cdc_service** 的資料庫使用者，而且該使用者會與 Oracle CDC 服務所設定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入相關聯。 這個使用者會成為 **db_datareader**、 **db_datawriter**和 **db_ddladmin** 資料庫角色的成員。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入也與 `dbo` 使用者相關聯，則不會建立 **cdc_service** 。  
  
 這個角色指派可讓 Oracle CDC 服務在包含擷取之資料和控制資訊的 `cdc` 結構描述之下更新資料表。  
  
 當建立 CDC 資料庫及設定 CDC 來源 Oracle 資料表時，CDC 資料庫擁有者可以授與鏡像資料表的 SELECT 權限，並定義 SQL Server CDC 控制角色來控制存取變更資料的人。  
  
## <a name="mirror-tables"></a>鏡像資料表  
 對於每一個擷取的資料表 \<結構描述名稱>.\<資料表名稱> 而言 (在 Oracle 來源資料庫中)，都會在 CDC 資料庫中建立類似的空白資料表，而且具有相同的結構描述與資料表名稱。 無法擷取結構描述名稱為 `cdc` (不區分大小寫) 的 Oracle 來源資料表，因為會保留 `cdc` 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結構描述給 SQL Server CDC。  
  
 鏡像資料表是空的，其中不會儲存任何資料。 鏡像資料表是用來啟用 Oracle CDC 執行個體所使用的標準 SQL Server CDC 基礎結構。 為了避免將資料插入或更新到鏡像資料表中，PUBLIC 拒絕所有的 UPDATE、DELETE 和 INSERT 作業。 這可確保無法修改這些資料表。  
  
## <a name="access-to-change-data"></a>存取變更資料  
 由於用來存取與擷取執行個體相關聯之變更資料的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性模型的緣故，必須將相關鏡像資料表之所有擷取資料行的 `select` 存取權限授與使用者 (對原始 Oracle 資料表的存取權限不會提供對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中之變更資料表的存取權)。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性模型的資訊，請參閱 [安全性模型](http://go.microsoft.com/fwlink/?LinkId=231151)。  
  
 此外，如果建立擷取執行個體時指定了控制角色，呼叫端也必須是指定之控制角色的成員。 雖然傳回之中繼資料的存取權通常也會使用基礎來源資料表的選取存取權以及任何已定義之控制角色的成員資格來控制，但是所有資料庫使用者都可以透過 PUBLIC 角色存取用以存取中繼資料的其他一般異動資料擷取函數。  
  
 當建立擷取執行個體時，可能會藉由呼叫特殊資料表函數 (由 SQL Server CDC 元件產生) 來讀取變更資料。 如需此函數的詳細資訊，請參閱 [異動資料擷取函數 (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=231152)。  
  
 透過 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CDC 來源元件存取 CDC 資料受限於相同的規則。  
  
## <a name="the-cdc-database-tables"></a>CDC 資料庫資料表  
 本節描述 CDC 資料庫中的以下資料表。  
  
-   [變更資料表 (_CT)](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_Change_Tables_CT)  
  
-   [cdc.lsn_time_mapping](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdclsn_time_mapping)  
  
-   [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config)  
  
-   [cdc.xdbcdc_state](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state)  
  
-   [cdc.xdbcdc_trace](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_trace)  
  
-   [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions)  
  
###  <a name="BKMK_Change_Tables_CT"></a> 變更資料表 (_CT)  
 變更資料表是從鏡像資料表建立而來。 其中包含擷取自 Oracle 資料庫的變更資料。 這些資料表是根據以下慣例所命名：  
  
 **[cdc].[\<capture-instance>_CT]**  
  
 一開始為資料表 `<schema-name>.<table-name>`啟用擷取時，預設擷取執行個體名稱為 `<schema-name>_<table-name>`。 例如，Oracle HR.EMPLOYEES 資料表的預設擷取執行個體名稱為 HR_EMPLOYEES 而且關聯的變更資料表為 [cdc]。 [HR_EMPLOYEES_CT]。  
  
 擷取資料表是由 Oracle CDC 執行個體寫入。 當建立擷取執行個體時，便會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的特殊資料表值函式讀取這些資料表。 例如， `fn_cdc_get_all_changes_HR_EMPLOYEES`。 如需這些 CDC 函數的詳細資訊，請參閱 [異動資料擷取函數 (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=231152)。  
  
###  <a name="BKMK_cdclsn_time_mapping"></a> cdc.lsn_time_mapping  
 **[cdc].[lsn_time_mapping]** 資料表是由 SQL Server CDC 元件所產生。 它在 Oracle CDC 中的使用情況與一般使用情況不同。  
  
 如果是 Oracle CDC，這個資料表中儲存的 LSN 值是根據與變更相關聯的 Oracle 系統變更編號 (SCN) 值。 LSN 值的前 6 個位元組是原始 Oracle SCN 編號。  
  
 此外在使用 Oracle CDC 時，時間資料行 (`tran_begin_time` 和 `tran_end_time`) 會儲存變更的 UTC 時間，而不是當地時間，就像在一般 SQL Server CDC 中一樣。 如此可確保日光節約時間變更不會影響 lsn_time_mapping 中所儲存的資料。  
  
###  <a name="BKMK_cdcxdbcdc_config"></a> cdc.xdbcdc_config  
 此資料表包含 Oracle CDC 執行個體的組態資料。 它是使用 CDC 設計工具主控台來更新。 此資料表只有一個資料列。  
  
 下表描述 **cdc.xdbcdc_config** 資料表資料行。  
  
|項目|描述|  
|----------|-----------------|  
|version|這會追蹤 CDC 執行個體組態的版本。 每當更新資料表以及加入新的擷取執行個體或是移除現有的擷取執行個體時，都會更新此項目。|  
|connect_string|Oracle 連接字串。 基本範例如下：<br /><br /> `<server>:<port>/<instance>` (例如 `erp.contoso.com:1521/orcl`)。<br /><br /> 連接字串還可以指定 Oracle Net 連接描述項，例如， `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`。<br /><br /> 如果使用目錄伺服器或 tnsnames，則連接字串可以是連接的名稱。<br /><br /> 如需 Oracle 連接字串的詳細資訊，請參閱 [http://go.microsoft.com/fwlink/?LinkId=231153](http://go.microsoft.com/fwlink/?LinkId=231153) ，以取得 Oracle CDC 服務所使用之 Oracle Instant Client 的 Oracle 資料庫連接字串詳細資訊。|  
|use_windows_authentication|下列其中一個值的布林值：<br /><br /> **0**：提供 Oracle 使用者名稱和密碼進行驗證 (預設)<br /><br /> **1**：使用 Windows 驗證連接到 Oracle 資料庫。 只有當設定 Oracle 資料庫使用 Windows 驗證時，才可使用這個選項。|  
|username|記錄採礦之 Oracle 資料庫使用者的名稱。 只有當 **use_windows_authentication = 0**時，才會強制這項設定。|  
|密碼|記錄採礦之 Oracle 資料庫使用者的密碼。 只有當 **use_windows_authentication = 0**時，才會強制這項設定。|  
|transaction_staging_timeout|未認可的 Oracle 交易在寫入 **cdc.xdbcdc_staged_transactions** 資料表之前保留在記憶體中的時間 (以秒數為單位)。 預設值是 120 秒。|  
|memory_limit|可用於快取記憶體中之資料的記憶體數量限制 (以 MB 為單位)。 較低的設定會導致更多的交易寫入 **cdc.xdbcdc_staged_transactions** 資料表中。 預設值為 50 MB。|  
|選項|name[=value][; ] 格式的選項清單 - 這是用於指定次要選項 (例如追蹤、微調)。 請參閱下表，取得可用選項的描述。|  
  
 下表描述可用的選項。  
  
|[屬性]|預設|Min|Max|靜態|描述|  
|----------|-------------|---------|---------|------------|-----------------|  
|追蹤|False|-|-|False|可用的值為：<br /><br /> True<br /><br /> False<br /><br /> on<br /><br /> 關閉|  
|cdc_update_state_interval|10|@shouldalert|120|False|配置給交易的記憶體區塊大小，以 KB 為單位 (一筆交易可以配置一個以上的區塊)。 請參閱 [cdc.xdbcdc_config](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_config) 資料表中的 memory_limit 資料行。|  
|target_max_batched_transactions|100|@shouldalert|1000|True|可以在 SQL Server CT 資料表更新中當做一筆交易來處理的最大 Oracle 交易數目。|  
|target_idle_lsn_update_interval|10|0|@shouldalert|False|當擷取的資料表沒有活動時，用來更新 **lsn_time_mapping** 資料表的間隔 (以秒數為單位)。|  
|trace_retention_period|24|@shouldalert|24*31|False|時間數量 (將訊息保留在追蹤資料表中的時數)。|  
|sql_reconnect_interval|2|2|3600|False|重新連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前所等候的時間數量 (以秒數為單位)。 除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端的連接逾時之外，也會使用這個間隔。|  
|sql_reconnect_limit|-1|-1|-1|False|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新連接的最大數目。 預設值 -1 表示此程序會嘗試重新連接，直到停止。|  
|cdc_restart_limit|6|-1|3600|False|在大多數情況下，CDC 服務會重新啟動異常情況下自動結束的 CDC 執行個體。 此屬性會定義每個小時有多少失敗次數，此服務才會停止並重新啟動執行個體。 -1 的值表示執行個體永遠都應該重新啟動。<br /><br /> 在組態資料表的任何更新之後，此服務會返回來重新啟動執行個體。|  
|cdc_memory_report|0|0|1000|False|如果參數的值已變更，CDC 執行個體會將它的記憶體報表列印在追蹤資料表上。|  
|target_command_timeout|600|@shouldalert|3600|False|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時發生命令逾時。|  
|source_character_set|-|-|-|True|可以設定為要使用的特定 Oracle 編碼方式，而不是 Oracle 資料庫字碼頁。 當字元資料使用的實際編碼方式與 Oracle 資料庫字碼頁所表示的編碼方式不同時，這樣的處理方式可能會很實用。|  
|source_error_retry_interval|30|@shouldalert|3600|False|在發生數個錯誤而重試之前使用，例如連接錯誤，或是系統資料表之間暫時缺少同步處理。|  
|source_prefetch_size|100|@shouldalert|10000|True|預先提取批次的大小。|  
|source_max_tables_in_query|100|@shouldalert|10000|True|在切換模式來讀取 Oracle 記錄而不篩選資料表之前，WHERE 子句中的最大資料表數目。|  
|source_read_retry_interval|2|@shouldalert|3600|False|嘗試再次於 EOF 上讀取 Oracle 交易記錄之前，來源等候的時間數量。|  
|source_reconnect_interval|30|@shouldalert|3600|False|嘗試重新連接到來源資料庫之前等候的時間 (以秒數為單位)。|  
|source_reconnect_limit|-1|-1||False|來源資料庫重新連接的最大數目。 預設值 -1 表示此程序會嘗試重新連接，直到停止。|  
|source_command_timeout|30|@shouldalert|3600|False|使用 Oracle 時發生連接逾時。|  
|source_connection_timeout|30|@shouldalert|3600|False|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時發生連接逾時。|  
|trace_data_errors|True|-|-|False|布林值。 **True** 表示記錄資料轉換和截斷錯誤。|  
|CDC_stop_on_breaking_schema_changes|False|-|-|False|布林值。 **True** 表示在偵測到重大結構描述變更時停止。<br /><br /> **False** 表示卸除鏡像資料表和擷取執行個體。|  
|source_oracle_home||-|-|False|可設定為特定的 Oracle Home 路徑，或是 CDC 執行個體將用來連接到 Oracle 的 Oracle Home 名稱。|  
  
###  <a name="BKMK_cdcxdbcdc_state"></a> cdc.xdbcdc_state  
 此資料表包含有關 Oracle CDC 執行個體之已保存狀態的資訊。 擷取狀態會用於復原和容錯移轉情況，也可用於監控健全狀態。  
  
 下表描述 **cdc.xdbcdc_state** 資料表資料行。  
  
|項目|描述|  
|----------|-----------------|  
|status|目前 Oracle CDC 執行個體的目前狀態碼。 此狀態會描述 CDC 的目前狀態。|  
|sub_status|提供有關目前狀態之其他資訊的第二層狀態。|  
|active|下列其中一個值的布林值：<br /><br /> **0**：Oracle CDC 執行個體處理序不在使用中。<br /><br /> **1**：Oracle CDC 執行個體處理序為使用中。|  
|error|下列其中一個值的布林值：<br /><br /> **0**：Oracle CDC 執行個體處理序不在錯誤狀態中。<br /><br /> **1**：Oracle CDC 執行個體在錯誤狀態中。|  
|status_message|提供錯誤或狀態描述的字串。|  
|TIMESTAMP|包含上次更新擷取狀態之時間 (UTC) 的時間戳記。|  
|active_capture_node|目前正在執行 Oracle CDC 服務和 Oracle CDC 執行個體 (它正在處理 Oracle 交易記錄) 的主機名稱 (此主機可以是叢集上的節點)。|  
|last_transaction_timestamp|包含上次交易寫入變更資料表之時間 (UTC) 的時間戳記。|  
|last_change_timestamp|包含從來源 Oracle 交易記錄讀取最近變更記錄之時間 (UTC) 的時間戳記。 此時間戳記有助於識別 CDC 程序的目前延遲。|  
|transaction_log_head_cn|從 Oracle 交易記錄讀取的最近變更編號 (CN)。|  
|transaction_log_tail_cn|Oracle 交易記錄上的變更編號 (CN)，其上的 Oracle CDC 執行個體會在重新啟動或復原時重新調整位置。|  
|current_cn|已知在來源資料庫中的最近變更編號 (CN)。|  
|software_version|Oracle CDC 服務的內部版本。|  
|completed_transactions|上次重設 CDC 之後處理過的交易數目。|  
|written_changes|寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更資料表的變更記錄數目。|  
|read_changes|從來源 Oracle 交易記錄讀取的變更記錄數目。|  
|staged_transactions|目前暫存於 **cdc.xdbcdc_staged_transactions** 資料表中的使用中交易數目。|  
  
###  <a name="BKMK_cdcxdbcdc_trace"></a> cdc.xdbcdc_trace  
 此資料表包含有關 CDC 執行個體操作的資訊。 儲存在此資料表中的資訊包括錯誤記錄、顯著的狀態變更及追蹤記錄。 錯誤資訊也會寫入 Windows 事件記錄檔，以確保當 **cdc.xcbcdc_trace** 資料表無法使用時可以使用該資訊。  
  
 下表描述 cdc.xdbcdc_trace 資料表資料行。  
  
|項目|描述|  
|----------|-----------------|  
|TIMESTAMP|寫入追蹤記錄的精確 UTC 時間戳記。|  
|型別|包含下列其中一個值。<br /><br /> error<br /><br /> INFO<br /><br /> 追蹤|  
|node|寫入記錄的節點名稱。|  
|status|狀態資料表使用的狀態碼。|  
|sub_status|狀態資料表使用的子狀態碼。|  
|status_message|狀態資料表使用的狀態訊息。|  
|data|當錯誤或追蹤記錄包含裝載時的其他資料 (例如，損毀的記錄檔記錄)。|  
  
###  <a name="BKMK_cdcxdbcdc_staged_transactions"></a> cdc.xdbcdc_staged_transactions  
 此資料表會儲存大型交易或長時間執行之交易的變更記錄，直到擷取交易認可或回復事件為止。 Oracle CDC 服務會依據交易認可時間，然後依據每一筆交易的時間順序來排序擷取的記錄檔記錄。 相同交易的記錄檔記錄會儲存在記憶體中，直到交易結束然後寫入目標變更資料表或遭到捨棄為止 (如果進行回復作業的話)。 因為可用記憶體數量有限，所以大型交易會寫入 **cdc.xdbcdc_staged_transactions** 資料表中，直到交易完成為止。 當交易長時間執行時，也會寫入暫存資料表。 因此在重新啟動 Oracle CDC 執行個體時，不需要從 Oracle 交易記錄重新讀取舊的變更。  
  
 下表描述 **cdc.xdbcdc_staged_transactions** 資料表資料行。  
  
|項目|描述|  
|----------|-----------------|  
|transaction_id|正在暫存之交易的唯一交易識別碼。|  
|seq_num|目前交易的 **xcbcdc_staged_transactions** 資料列數目 (從 0 開始)。|  
|data_start_cn|此資料列中資料之第一項變更的變更編號 (CN)。|  
|data_end_cn|此資料列中資料之最後一項變更的變更編號 (CN)。|  
|data|BLOB 形式之交易的暫存變更。|  
  
## <a name="see-also"></a>另請參閱  
 [Attunity Oracle 異動資料擷取設計工具](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)  
  
  
