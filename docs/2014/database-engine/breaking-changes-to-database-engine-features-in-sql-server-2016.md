---
title: 重大變更到資料庫引擎功能的 SQL Server 2014 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
caps.latest.revision: 143
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: db9392c92568442a17c4683b2c8a25a5487f59d4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394219"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2014"></a>SQL Server 2014 中對於 Database Engine 的重大變更
  本主題描述 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] 以及舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的重大變更。 這些變更可能會中斷以舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]為根據的應用程式、指令碼或功能。 當您升級時可能會遇到這些問題。 如需詳細資訊，請參閱＜ [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)＞。  
  
##  <a name="SQL14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 的重大變更  
 沒有任何新的問題。  
  
##  <a name="Denali"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 的重大變更  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|功能|描述|  
|-------------|-----------------|  
|從名為 NEXT 的資料行或資料表選取|序列會使用 ANSI 標準 NEXT VALUE FOR 函數。 如果資料表或資料行名為 NEXT，以及資料表或資料行的別名為 VALUE，且您省略 ANSI 標準 AS 時，產生的陳述式可能會導致錯誤。 若要解決這個問題，請加入 ANSI 標準 AS 關鍵字。 例如，`SELECT NEXT VALUE FROM Table` 應該改寫成 `SELECT NEXT AS VALUE FROM Table`，而 `SELECT Col1 FROM NEXT VALUE` 應該改寫成 `SELECT Col1 FROM NEXT AS VALUE`。|  
|PIVOT 運算子|當資料庫相容性層級設定為 110 時，不允許在遞迴通用資料表運算式 (CTE) 查詢中使用 PIVOT 運算子。 請重寫查詢，或將相容性層級變更為 100 或更低。 當每個群組具有多個資料列時，在遞迴 CTE 查詢中使用 PIVOT 會產生錯誤的結果。|  
|sp_setapprole 和 sp_unsetapprole|`OUTPUT` 的 Cookie `sp_setapprole` 參數目前記載成 `varbinary(8000)`，是正確的長度上限。 但目前的實作會傳回`varbinary(50)`。 應用程式應繼續保留 `varbinary(8000)`，如此後續版本的 Cookie 傳回大小如有增加，應用程式才可繼續正常地運作。 如需詳細資訊，請參閱 [sp_setapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)。|  
|EXECUTE AS|EXECUTE AS 的 Cookie OUTPUT 參數目前記載成 `varbinary(8000)`，這是正確的長度上限。 但目前的實作會傳回`varbinary(100)`。 應用程式應繼續保留 `varbinary(8000)`，如此後續版本的 Cookie 傳回大小如有增加，應用程式才可繼續正常地運作。 如需詳細資訊，請參閱 [EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql)。|  
|sys.fn_get_audit_file 函數|兩個額外的資料行 (**user_defined_event_id**並**user_defined_information**) 已新增以支援使用者定義稽核事件。 沒有依照名稱選取資料行的應用程式可能會傳回超過預期數目的資料行。 請依照名稱選取資料行，或調整應用程式以接受這些額外的資料行。|  
|WITHIN 保留關鍵字|WITHIN 現在是保留關鍵字。 名為 'within' 之物件或資料行的參考將會失敗。 請重新命名物件或資料行名稱，或者使用括號或引號來分隔名稱。  例如， `SELECT * FROM [within]` 。|  
|`time` 或 `datetime2` 類型之計算資料行的 CAST 和 CONVERT 作業|在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，除非用於計算資料行運算式，否則 `time` 和 `datetime2` 資料類型之 CAST 和 CONVERT 作業的預設樣式為 121。 若為計算資料行，預設樣式為 0。 當您建立計算資料行、將它們用於包含自動參數化的查詢或用於條件約束定義時，這種行為就會影響計算資料行。<br /><br /> 在相容性層級 110 底下，`time` 和 `datetime2` 資料類型之 CAST 和 CONVERT 作業的預設樣式一律為 121。 如果您的查詢仰賴舊的行為，請使用低於 110 的相容性層級，或在受影響的查詢中明確指定 0 樣式。<br /><br /> 將資料庫升級為相容性層級 110 不會變更已經儲存至磁碟的使用者資料。 您必須依適當情況手動更正這項資料。 例如，如果您使用了 SELECT INTO，根據包含上述計算資料行運算式的來源建立資料表，系統就會儲存資料 (使用樣式 0) 而非計算資料行定義本身。 您必須手動將這項資料更新為符合樣式 121。|  
|ALTER TABLE|ALTER TABLE 陳述式只允許兩部分 (schema.object) 資料表名稱。 現在使用下列格式的資料表名稱來指定會在編譯時期顯示錯誤 117 失敗：<br /><br /> server.database.schema.table<br /><br /> .database.schema.table<br /><br /> ..schema.table<br /><br /> 在舊版中，指定 server.database.schema.table 格式會傳回錯誤 4902。 不過，指定 .database.schema.table 格式或 ..schema.table 格式會成功。 若要解決此問題，請移除 4 部分前置詞的用法。|  
|瀏覽中繼資料|使用 FOR BROWSE 或 SET NO_BROWSETABLE ON 來查詢檢視現在會傳回檢視的中繼資料，而非基礎物件的中繼資料。 這種行為現在與其他瀏覽中繼資料的方法相符。|  
|SOUNDEX|在資料庫相容性層級 110 下，SOUNDEX 函式會實作新的規則，這些規則可能會使此函式將值計算成不同於在舊版相容性層級下計算的值。 升級到相容性層級 110 之後，您可能需要重建使用 SOUNDEX 函數的索引、堆積或 CHECK 條件約束。 如需詳細資訊，請參閱 [SOUNDEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/soundex-transact-sql)
 執行個體時提供 SQL Server 登入。|  
|失敗之 DML 陳述式的資料列計數訊息|在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中，當 DML 陳述式失敗時，[!INCLUDE[ssDE](../includes/ssde-md.md)] 會以一致的方式將含有 RowCount: 0 的 TDS DONE Token 傳送至用戶端。 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，當失敗的 DML 陳述式包含在 TRY-CATCH 區塊中，而且由 [!INCLUDE[ssDE](../includes/ssde-md.md)] 自動參數化，或者 TRY-CATCH 區塊與失敗的陳述式不在相同的層級上時，系統會將錯誤的值 -1 傳送至用戶端。 例如，如果 TRY-CATCH 區塊呼叫了預存程序，而且此程序中的 DML 陳述式失敗，則用戶端將收到錯誤的 -1 值。<br /><br /> 仰賴此錯誤行為的應用程式將會失敗。|  
|SERVERPROPERTY (‘Edition’)|已安裝的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 執行個體產品版本。 請利用這個屬性值來判斷已安裝的產品所支援的功能和限制 (如最大 CPU 數目)。<br /><br /> 根據已安裝的 Enterprise 版，這會傳回 ‘Enterprise Edition’ 或「Enterprise 版: 核心授權」。 Enterprise 版本會根據單一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的計算容量上限而區分。 如需有關中的計算容量限制[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]，請參閱 < [SQL server 版本計算容量限制](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。|  
|CREATE LOGIN|`CREATE LOGIN WITH PASSWORD = '`*密碼*`' HASHED`選項不能藉由建立雜湊[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]7 或更早版本。|  
|`datetimeoffset` 的 CAST 和 CONVERT 作業|從日期和時間類型轉換成 `datetimeoffset` 時，唯一支援的樣式是 0 或 1。 所有其他轉換樣式都會傳回錯誤 9809。 例如，下列程式碼會傳回錯誤 9809。<br /><br /> `SELECT CONVERT(date, CAST('7070-11-25 16:25:01.00986 -02:07' as datetimeoffset(5)), 107);`|  
  
### <a name="dynamic-management-views"></a>動態管理檢視  
  
|檢視|描述|  
|----------|-----------------|  
|sys.dm_exec_requests|命令資料行從 `nvarchar(16)` 變更為 `nvarchar(32)`。|  
|sys.dm_os_memory_cache_counters|下列資料行已重新命名：<br /><br /> single_pages_kb 現在是： <br />                          pages_kb<br /><br /> multi_pages_kb<br />                           現在是： pages_in_use_kb&lt|  
|sys.dm_os_memory_cache_entries|資料行 pages_allocated_count&lt 資料行已重新命名的 pages_kb。|  
|sys.dm_os_memory_clerks|已移除資料行 multi_pages_kb&lt。<br /><br /> 資料行 single_pages_kb 資料行已重新命名的 pages_kb。|  
|sys.dm_os_memory_nodes|下列資料行已重新命名：<br /><br /> single_pages_kb 現在是： <br />                            pages_kb<br /><br /> multi_pages_kb&lt 現在是： <br />                            foreign_committed_kb|  
|sys.dm_os_memory_objects|下列資料行已經重新命名。<br /><br /> pages_allocated_count&lt 現在是：<br />                            pages_in_bytes<br /><br /> 現已 max_pages_allocated_count: max_pages_in_bytes|  
|sys.dm_os_sys_info|下列資料行已重新命名：<br /><br /> physical_memory_in_bytes 現在是： <br />                            physical_memory_kb<br /><br /> bpool_commit_target 現在是： <br />                            committed_target_kb&lt<br /><br /> bpool_visible 現在是： <br />                            visible_target_kb&lt<br /><br /> virtual_memory_in_bytes 現在是： <br />                            virtual_memory_kb<br /><br /> bpool_commited 現在是：<br />                            committed_kb&lt|  
|sys.dm_os_workers|地區設定資料行已經被移除。|  
  
### <a name="catalog-views"></a>目錄檢視  
  
|檢視|描述|  
|----------|-----------------|  
|sys.data_spaces<br /><br /> sys.partition_schemes<br /><br /> sys.filegroups<br /><br /> sys.partition_functions|新的資料行 is_system 已經加入至 sys.data_spaces 和 sys.partition_functions  (sys.partition_schemes 和 sys.filegroups 會繼承 sys.data_spaces 的資料行)。<br /><br /> 這個資料行中的值 1 表示此物件用於全文檢索索引片段。<br /><br /> 在 sys.partition_functions、sys.partition_schemes 和 sys.filegroups 中，新的資料行不是最後一個資料行。 請修訂仰賴這些目錄檢視所傳回之資料行順序的現有查詢。|  
  
### <a name="sql-clr-data-types-geometry-geography-and-hierarchyid"></a>SQL CLR 資料類型 (geometry、geography 和 hierarchyid)  
 組件**Microsoft.SqlServer.Types.dll**，其中包含空間資料類型和 hierarchyid 類型，具有已從 10.0 版升級為 11.0 版。 當下列條件成立時，參考這個組件的自訂應用程式可能會失敗。  
  
-   當您移動自訂的應用程式從電腦所在[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]所在的電腦只安裝[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]是安裝，應用程式會失敗，因為參考的 10.0 版**SqlTypes**組件不存在。 您可能會看見這則錯誤訊息：`“Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified.”`  
  
-   當您參考**SqlTypes**組件 11.0 版，也安裝了 10.0 版，您可能會看到此錯誤訊息： `“System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'.”`  
  
-   當您參考**SqlTypes**組件 11.0 版從以.NET 3.5、 4 或 4.5 為目標的自訂應用程式，應用程式會失敗，因為 SqlClient 依照設計載入的組件 10.0 版。 當應用程式呼叫下列其中一個方法時，就會發生這項失敗：  
  
    -   `GetValue` 類別的 `SqlDataReader` 方法  
  
    -   `GetValues` 類別的 `SqlDataReader` 方法  
  
    -   `SqlDataReader` 類別的括號索引運算子 []  
  
    -   `ExecuteScalar` 類別的 `SqlCommand` 方法  
  
 您可以使用下列其中一個方法來解決這個問題：  
  
-   您可以在程式碼中呼叫 `GetSqlBytes` 方法 (而非上列 Get 方法) 來擷取 CLR [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 系統類型，藉以解決此問題，如下列範例所示：  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   您可以在應用程式組態檔中使用組件重新導向，藉以解決此問題，如下列範例所示：  
  
    ```xml  
    <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    <runtime>  
    ```  
  
-   您可以在連接字串中針對 "Type System Version" 屬性指定 "SQL Server 2012" 值，強制 SqlClient 載入組件 11.0 版，藉以解決此問題。 此連接字串屬性僅適用於 .NET 4.5 和更新版本。  
  
-   `assemblyBinding` 標記應該包裝在 `runtime` 標記下。  
  
### <a name="support-for-awe"></a>支援 AWE  
 32 位元 Address Windowing Extensions (AWE) 支援已停用。 這可能會導致 32 位元作業系統的效能降低。 若為使用大量記憶體的安裝，請移轉至 64 位元作業系統。  
  
### <a name="xquery-functions-are-surrogate-aware"></a>XQuery 函數能夠感知 Surrogate  
 XQuery 函數和運算子的 W3C 建議要求它們將代表高範圍 Unicode 字元的 Surrogate 字組視為 UTF-16 編碼中的單一影像。 不過，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 版本中，字串函數無法將 Surrogate 字組辨識成單一字元。 某些字串作業 (例如字串長度計算與子字串擷取) 會傳回錯誤的結果。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 現在完全支援 UTF-16，而且能夠正確處理 Surrogate 字組。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XML 資料類型僅允許格式正確的 Surrogate 字組。 不過，在某些情況下，部分函數仍然可能傳回未定義或非預期的結果，因為您可以將無效或部分 Surrogate 字組當做字串值傳遞給 XQuery 函數。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中使用 XQuery 時，請考慮採用下列方法來產生字串值：  
  
-   以二進位值的形式提供常數字串值。 使用此方法時，您仍然可以傳遞無效或部分 Surrogate 字組。  
  
-   透過提供字元實體，提供常數字串值。 使用此方法時，您無法傳遞無效的 Surrogate 字組。 XQuery 函數需要高層級字元的單一字元實體。 如果您提供了 Surrogate 字組字元的字元實體，這些函數會引發錯誤。  
  
-   使用匯入外部值**sql: column**或是**sql: variable**。 使用這些方法時，您仍然可以導入無效或部分 Surrogate 字組。  
  
#### <a name="affected-xquery-functions-and-operators"></a>受影響的 XQuery 函數和運算子  
 下列 XQuery 函數和運算子現在能夠正確地在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中處理 UTF-16 Surrogate 字組：  
  
-   **fn: string 的長度**。 不過，如果無效或部分 surrogate 字組傳遞做為引數的行為**字串長度**是未定義。  
  
-   **fn: substring**。  
  
-   **fn： 包含**。 不過，如果您將部分 surrogate 字組為值時，傳遞**包含**可能傳回未預期的結果，因為它可能會發現部分 surrogate 字組包含格式正確的 surrogate 字組中。  
  
-   **fn: concat**。 不過，如果您將部分 surrogate 字組為值時，傳遞**concat**可能會產生不正確的 surrogate 字組或部分 surrogate 字組。  
  
-   比較運算子和**依**子句。 比較運算子包括 +、 \<，>， \<=、 > =、 `eq`， `lt`， `gt`， `le`，和`ge`。  
  
#### <a name="distributed-query-calls-to-a-system-procedure"></a>對系統程序的分散式查詢呼叫  
 透過 `OPENQUERY` 對某些系統程序的分散式查詢呼叫，在從某個 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 伺服器呼叫到另一個伺服器時會失敗。 在 [!INCLUDE[ssDE](../includes/ssde-md.md)] 找不到程序的中繼資料時會出現此情況。 例如， `SELECT * FROM OPENQUERY(..., 'EXEC xp_loginfo')` 。  
  
#### <a name="isolation-level-and-spresetconnection"></a>隔離等級與 sp_reset_connection  
 用戶端驅動程式會以下列方式處理連接的隔離等級：  
  
-   所有原生的驅動程式 (SNAC、MDAC、ODBC) 都會在 sp_reset_connection 時設定隔離等級 (根據應用程式設定)。  
  
-   對於 ADO.NET，原則上您會依據您從集區中取得的連線，而隨機獲取一個隔離等級 (但前提是應用程式使用了不同的隔離等級)。 因為 ADO.NET 集區可以不著痕跡地從內部回收連線，所以您無法預測集區所提供的連接。  
  
-   JDBC 驅動程式的行為與 ADO.NET 相同。  
  
     應用程式必須在開啟連接之後，明確地設定隔離等級，如此才能取得所需要的連接。  
  
     JDBC 連接可能會存放在集區中，所以應用程式可能會得到隨機的隔離等級並無從得知。  
  
 若要保留這項新行為的回溯相容性，請只對 TDS 7.4 之後的新版用戶端套用此行為。  
  
#### <a name="backward-compatibility"></a>Backward Compatibility  
 **新的行為取決於相容性層級**  
  
 只有當相容性層級為 110 或更高時，下列函數和運算子才會呈現上述新行為：  
  
-   **fn： 包含**。  
  
-   **fn: concat**。  
  
-   比較運算子並**依**子句  
  
 **新的行為取決於函式的預設命名空間 URI**  
  
 下列函式示範新的行為描述上方時，才預設命名空間 URI 對應至命名空間在最終建議中，亦即[ http://www.w3.org/2005/xpath-functions ](http://www.w3.org/2005/xpath-functions)。 當相容性層級為 110 或更高時，則 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 預設會將預設函數命名空間繫結至這個命名空間。 不過，不論相容性層級為何，只要使用這個命名空間，這些函數就會呈現新行為。  
  
-   **fn: string 的長度**  
  
-   **fn: substring**  
  
##  <a name="KJKatmai"></a> 重大變更，在 SQL Server 2008/SQL Server 2008 r2  
 本節包含 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中導入的重大變更。 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 並未導入任何變更。  
  
### <a name="collations"></a>定序  
  
|功能|描述|  
|-------------|-----------------|  
|新的定序|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 導入了與 Windows Server 2008 所提供之定序完全一致的新定序。 這 80 個新定序具有改進的語言精確度，而且是由 *_100 版本參考所表示。 如果您針對伺服器或資料庫選擇新的定序，請注意，具有舊版用戶端驅動程式的用戶端可能無法辨識此定序。 無法辨識的定序可能會導致應用程式傳回錯誤並失敗。 請考慮下列解決方案：<br /><br /> 升級用戶端作業系統，以便更新基礎系統定序。<br /><br /> 如果您的用戶端已經安裝了資料庫用戶端軟體，請考慮將服務更新套用至資料庫用戶端軟體。<br /><br /> 選擇會對應至用戶端字碼頁的現有定序。|  
  
### <a name="common-language-runtime-clr"></a>Common Language Runtime (CLR)  
  
|功能|描述|  
|-------------|-----------------|  
|CLR 組件|當資料庫升級為 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 時，就會自動安裝支援新資料類型的 `Microsoft.SqlServer.Types` 組件。 Upgrade Advisor 規則會偵測任何具有衝突名稱的使用者類型或組件。 Upgrade Advisor 將建議您重新命名任何衝突的組件，以及重新命名任何衝突的類型，或在程式碼中使用兩部分名稱來參考預先存在的使用者類型。<br /><br /> 如果資料庫升級偵測到具有衝突名稱的使用者組件，它將自動重新命名該組件並讓資料庫進入質疑模式。<br /><br /> 如果具有衝突名稱的使用者類型在升級期間存在，將不會採取任何特殊步驟。 在升級之後，舊的使用者類型和新的系統類型都會一起存在。 但是，該使用者類型只能透過兩部分名稱使用。|  
|CLR 組件|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 會安裝 .NET Framework 3.5 SP1，以便更新全域組件快取 (GAC) 中的程式庫。 如果您在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫中註冊了不支援的程式庫，則升級至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之後，[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 應用程式可能會停止運作。 這是因為服務或升級 GAC 中的程式庫並不會更新 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 內部的組件。 如果某個組件同時存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫和 GAC 中，這個組件的兩個副本就必須完全相符。 如果它們不相符，當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] CLR 整合使用該組件時，將會發生錯誤。 如需詳細資訊，請參閱 <<c0> [ 支援的.NET Framework 程式庫](../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。<br /><br /> 升級您的資料庫之後，請使用 ALTER ASSEMBLY 陳述式來服務或升級 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫內部的組件副本。 如需詳細資訊，請參閱 <<c0> [ 知識庫文件 949080](http://go.microsoft.com/fwlink/?LinkId=154563)。<br /><br /> 若要偵測您是否正在應用程式中使用任何不支援的 .NET Framework 程式庫，請在資料庫中執行下列查詢。<br /><br /> `SELECT name FROM sys.assemblies WHERE clr_name LIKE '%publickeytoken=b03f5f7f11d50a3a,%';`|  
|CLR 常式|在 CLR 使用者定義函數、使用者定義彙總或使用者定義型別 (UDT) 內部使用模擬可能會導致您的應用程式在升級至 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 之後失敗並顯示錯誤 6522。 下列狀況在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中會成功，但在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中則會失敗。 我們已針對每個狀況提供解決方案。<br /><br /> CLR 使用者定義函數、 使用者定義彙總或使用模擬的 UDT 方法具有參數的型別`nvarchar(max)`， `varchar(max)`， `varbinary(max)`， `ntext`， `text`， `image`，或大型 UDT，而且沒有**DataAccessKind.Read**方法上的屬性。 若要解決此問題，請新增**DataAccessKind.Read**屬性的方法、 重新編譯組件，然後重新部署常式和組件。<br /><br /> CLR 資料表值函數具有**Init**執行模擬的方法。 若要解決此問題，請加入**DataAccessKind.Read**屬性的方法、 重新編譯組件，然後重新部署常式和組件。<br /><br /> CLR 資料表值函數具有**FillRow**執行模擬的方法。 若要解決此問題，移除模擬**FillRow**方法。 不使用會存取外部資源**FillRow**方法。 相反地，存取外部資源**Init**方法。|  
  
### <a name="dynamic-management-views"></a>動態管理檢視  
  
|檢視|描述|  
|----------|-----------------|  
|sys.dm_os_sys_info|已移除 cpu_ticks_in_ms 和 sqlserver_start_time_cpu_ticks 資料行。|  
|sys.dm_exec_query_resource_semaphoressys.dm_exec_query_memory_grants|resource_semaphore_id 資料行不是 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中的唯一識別碼。 這項變更可以影響疑難排解的查詢執行。 如需詳細資訊，請參閱 < [sys.dm_exec_query_resource_semaphores &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql)。|  
  
### <a name="errors-and-events"></a>錯誤和事件  
  
|功能|描述|  
|-------------|-----------------|  
|登入錯誤|在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 中，當 SQL 登入用來連接至設定成只使用 Windows 驗證的伺服器時，就會傳回錯誤 18452。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，系統會改為傳回錯誤 18456。|  
  
### <a name="showplan"></a>執行程序表  
  
|功能|描述|  
|-------------|-----------------|  
|執行程序表 XML 結構描述|新**SeekPredicateNew**項目加入至執行程序表 XML 結構描述和封閉式 xsd 順序 (**SqlPredicatesType**) 會轉換成 **\<xsd: choice> >** 項目。 而不是一或多個**SeekPredicate**項目，一或多個**SeekPredicateNew**項目現在可能會出現在執行程序表 XML 中。 這兩個元素互斥。 **SeekPredicate**保留的執行程序表 XML 結構描述回溯相容性; 不過，查詢中建立的計劃[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]可能會包含**SeekPredicateNew**項目。 只擷取預期的應用程式**SeekPredicate**從節點 ShowPlanXML/BatchSequence/Batch/陳述式/StmtSimple/QueryPlan/RelOp/IndexScan/seekpredicates 中單獨擷取的子系可能會失敗，如果**SeekPredicate**元素不存在。 請重寫應用程式，以便預期**SeekPredicate**或是**SeekPredicateNew**此節點中的項目。 若需相關資訊，請參閱 。|  
|執行程序表 XML 結構描述|新**IndexKind**屬性新增至**ObjectType**執行程序表 XML 結構描述中的複雜型別。 針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 結構描述嚴格驗證 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 計畫的應用程式將會失敗。|  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|功能|描述|  
|-------------|-----------------|  
|ALTER_AUTHORIZATION_DATABASE DDL 事件|在  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，當 DDL 事件 ALTER_AUTHORIZATION_DATABASE 引發時，會傳回 'object' 的值**ObjectType**的實體類型之安全性實體的資料定義中這個事件之 EVENTDATA xml 項目語言 (DDL) 作業是一個物件。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，則會傳回實際類型 (例如 'table' 或 'function')。|  
|CONVERT|如果您將無效的樣式傳遞給 CONVERT 函數，當轉換類型為二進位對字元或字元對二進位時，系統就會傳回錯誤。 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，無效的樣式會設定為二進位對字元或字元對二進位轉換的預設樣式。|  
|GRANT/DENY/REVOKE 組件的 EXECUTE|您無法針對組件授與、拒絕或撤銷 EXECUTE 權限。 這個權限沒有任何作用，而且現在會導致錯誤。 請改為針對參考此組件方法的預存程序或函數授與、拒絕或撤銷 EXECUTE 權限。|  
|GRANT/DENY/REVOKE 系統類型的權限|您無法針對系統類型授與、拒絕或撤銷權限。 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，雖然這些陳述式會成功，但是沒有任何作用。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，則會傳回錯誤。|  
|GROUP BY|在 GROUP BY 子句在用於依清單分組的運算式中，不得包含子查詢。 在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，允許這個動作。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中，則會傳回錯誤 144。<br /><br /> 例如，下列程式碼在 SQL Server 2005 中將會成功，而在 SQL Server 2008 中則會失敗。<br /><br /> `DECLARE @Test TABLE(a int NOT NULL);` <br /> `INSERT INTO @Test SELECT 1 union ALL SELECT 2;` <br /> `SELECT COUNT(*)` <br /> `FROM @Test` <br /> `GROUP BY CASE WHEN a IN (SELECT t.a FROM @Test AS t)` <br /> `THEN 1 ELSE 0` <br /> `END;`|  
|OUTPUT 子句|若要避免不具決定性的行為，當檢視表或嵌入資料表值函式中的資料行是由下列其中一種方法所定義時，OUTPUT 子句便不得參考該資料行：<br /><br /> 子查詢。<br /><br /> 執行使用者或系統資料存取的使用者定義函數，或假設會執行這類存取的使用者定義函數。<br /><br /> 在其定義中包含使用者定義函數的計算資料行，而該函數會執行使用者或系統資料存取。<br /><br /> <br /><br /> 當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 OUTPUT 子句中偵測到這類資料行時，就會引發錯誤 4186。 如需詳細資訊，請參閱 < [MSSQLSERVER_4186](../relational-databases/errors-events/mssqlserver-4186-database-engine-error.md)。|  
|OUTPUT INTO 子句|OUTPUT INTO 子句的目標資料表不可以有任何啟用的觸發程序。|  
|precompute rank 伺服器層級選項|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 不支援這個選項。 請盡快修改目前仍使用這項功能的應用程式。|  
|READPAST 資料表提示|您在快照集隔離的情況下指定 READPAST 提示。<br /><br /> 當 READ_COMMITED_SNAPSHOT 或 ALLOW_SNAPSHOT_ISOLATION 資料庫選項設為 ON 時，將會忽略 READPAST 提示。 但您若是合併了 READPAST 提示及 READCOMMITTEDLOCK，READPAST 的行為將與封鎖 READCOMMITTED 提示相同。|  
|sp_helpuser|下列在 sp_helpuser 預存程序的結果集傳回的資料行名稱已變更：<br /><br /> 群組名稱現在是：<br />                            RoleName<br /><br /> 群組名稱現在是：<br />                            Role_name<br /><br /> Group_id 現在是：<br />                            Role_id<br /><br /> Users_in_group 現在是：<br />                            Users_in_role|  
|透明資料加密|透明資料加密 (TDE) 是在 I/O 層級執行：頁面結構在記憶體中處於未加密狀態，而且只有當頁面寫入磁碟時，才會進行加密。 資料庫檔案和記錄檔都會進行加密。 當資料庫使用 TDE 時，略過存取頁面之一般 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 機制 (例如，直接掃描資料或記錄檔) 的協力廠商應用程式將會失敗，因為資料已在檔案中加密。 這類應用程式可以運用 Window Cryptographic API 來開發在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 外部解密資料的解決方案。|  
  
### <a name="xquery"></a>XQuery  
  
|功能|描述|  
|-------------|-----------------|  
|日期時間支援|在  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，資料類型`xs:time`， `xs:date`，和`xs:dateTime`沒有時區支援。 時區資料會對應至 UTC 時區。 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 提供了符合標準的行為，因而產生下列變更：<br /><br /> 驗證不含時區的值。<br /><br /> 保留提供的時區或缺少的時區。<br /><br /> 修改內部儲存體表示法。<br /><br /> 增加預存值的解析。<br /><br /> 不允許使用負值年份。<br /><br /> <br /><br /> 注意： 修改應用程式和 XQuery 運算式，以說明新的型別值。|  
|XQuery 和 Xpath 運算式|在  [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，開頭為冒號 XQuery 或 XPath 運算式中的步驟 (': ') 允許。 例如，下列陳述式在冒號開頭的路徑運算式中，包含一個名稱測試 (`CTR02)`)。<br /><br /> `SELECT FileContext.query('for n$ in //CTR return <C>{data )(n$/:CTR02)} </C>) AS Files FROM dbo.MyTable;`<br /><br /> 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 中不允許此種用法，因為它不符合 XML 標準。 傳回錯誤 9341。 移除開頭的冒號，或為名稱測試指定一個前置詞，例如，(n$/CTR02) 或 (n$/p1:CTR02)。|  
  
### <a name="connecting"></a>Connecting  
  
|功能|描述|  
|-------------|-----------------|  
|使用 SSL 從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 連接|當使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 連接時，使用 "SERVER=shortname; FORCE ENCRYPTION=true" 而且憑證的主旨可指定完整網域名稱 (FQDN) 的應用程式在過去因為寬鬆的驗證所以已經連接。 SQL Server 2008 R2 藉由強制施行憑證的 FQDN 主旨來增強安全性。 依賴寬鬆驗證的應用程式必須採取下列其中一項動作：<br /><br /> 使用連接字串中的 FQDN。<br /><br /> -這個選項不需要重新編譯應用程式，如果應用程式外面設定連接字串的 SERVER 關鍵字。<br /><br /> -此選項不適用於需要其連接字串硬式編碼的應用程式。<br /><br /> -此選項不適用於鏡像的伺服器則會以簡單名稱回覆之後使用 資料庫鏡像的應用程式。|  
||加入簡短名稱的別名來對應至 FQDN。<br /><br /> -此選項更適用於需要其連接字串硬式編碼的應用程式。<br /><br /> -此選項不適用於使用資料庫鏡像的提供者不會尋找接收之容錯移轉夥伴名稱的別名，因為應用程式。|  
||擁有針對簡短名稱發出的憑證。<br /><br /> -此選項適用於所有的應用程式。|  
  
##  <a name="Yukon"></a> SQL Server 2005 中的重大變更  
 如需清單的重大變更中導入[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]，請參閱[SQL Server 2005 中的 Database Engine 功能的突破性變更](breaking-changes-to-database-engine-features-in-sql-server-2016.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中已被取代的 Database Engine 功能](deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2014 中的 Database Engine 功能的行為變更](../../2014/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014.md)   
 [SQL Server 2014 中已停止的 Database Engine 功能](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server Database Engine 回溯相容性](sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
