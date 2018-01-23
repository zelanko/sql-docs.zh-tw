---
title: CREATE DATABASE (SQL Server Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs: TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
caps.latest.revision: "212"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7c6e52f8e36ed40e18c2aeab162a75c39f186c97
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2018
---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE (SQL Server Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立新資料庫和用來儲存資料庫的檔案、建立資料庫快照集，或從先前建立之資料庫的卸離檔案附加資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  

建立資料庫    

```  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
[;]  
  
<option> ::=  
{  
      FILESTREAM ( <filestream_option> [,...n ] )  
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }  
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }  
    | NESTED_TRIGGERS = { OFF | ON }  
    | TRANSFORM_NOISE_WORDS = { OFF | ON}  
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>   
    | DB_CHAINING { OFF | ON }  
    | TRUSTWORTHY { OFF | ON }  
}  
  
<filestream_option> ::=  
{  
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
    | DIRECTORY_NAME = 'directory_name'   
}  
  
<filespec> ::=   
{  
(  
    NAME = logical_file_name ,  
    FILENAME = { 'os_file_name' | 'filestream_path' }   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]  
)  
}  
  
<filegroup> ::=   
{  
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    <filespec> [ ,...n ]  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
}  
  
```  
 
附加資料庫    

```  
CREATE DATABASE database_name   
    ON <filespec> [ ,...n ]   
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }  
        | ATTACH_REBUILD_LOG }  
[;]  
  
<attach_database_option> ::=  
{  
      <service_broker_option>  
    | RESTRICTED_USER  
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )  
}   
```  
  
建立資料庫快照集    

```  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是新資料庫的名稱。 資料庫名稱必須是唯一的執行個體內[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，且必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 *database_name*最多可有 128 個字元，除非記錄檔未指定邏輯名稱。 如果未指定邏輯記錄檔名稱，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生*邏輯檔案名稱*和*os_file_name*藉由附加的後置詞的記錄檔*database_name*. 這會限制*database_name*到 123 個字元，使產生的邏輯檔案名稱不能超過 128 個字元。  
  
 如果未指定資料檔案名稱，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用*database_name*兩者*邏輯檔案名稱*並做為*os_file_name*。 預設路徑是從登錄取得。 可以變更預設路徑使用**伺服器屬性 （資料庫設定頁面）**中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 變更預設路徑需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 CONTAINMENT = { NONE | PARTIAL }  

**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定資料庫的內含項目狀態。 NONE = 非自主資料庫 PARTIAL = 部分自主資料庫  
  
 ON  
 指定必須明確定義用來儲存資料庫之資料區段 (資料檔案) 的磁碟檔案。 後面接著以逗號分隔的清單時，就需要 ON \<filespec > 定義主要檔案群組中的資料檔案的項目。 主要檔案群組中的檔案清單後面可以接著以逗號分隔的選擇性清單\<檔案群組 > 定義使用者檔案群組和其檔案的項目。  
  
 PRIMARY  
 指定相關聯\<filespec > 清單必須定義主要檔案。 第一個檔案中指定\<filespec > 主要檔案群組中的項目會成為主要檔案。 資料庫只能有一個主要檔案。 如需相關資訊，請參閱 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)。  
  
 如果未指定 PRIMARY，CREATE DATABASE 陳述式中列出的第一個檔案會成為主要檔案。  
  
 LOG ON  
 指定必須明確定義用來儲存資料庫記錄 (記錄檔) 的磁碟檔案。 LOG ON 後面的逗號分隔清單\<filespec > 項目定義的記錄檔。 如果未指定 LOG ON，系統會自動建立一個記錄檔，該檔案的大小是資料庫之所有資料檔案的大小總和的 25% 或 512 KB 其中較大者。 這個檔案會放置在預設的記錄檔位置中。 此位置的相關資訊，請參閱[檢視或變更預設位置的資料及記錄檔 &#40;SQL Server Management Studio &#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
 資料庫快照集中無法指定 LOG ON。  
  
 COLLATE *sys.databases*  
 指定資料庫的預設定序。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 若未指定，會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設定序指派給資料庫。 資料庫快照集中無法指定定序名稱。  
  
 定序名稱無法利用 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 子句來指定。 如需如何變更附加資料庫的定序資訊，請參閱此[Microsoft 寍鯚](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335)。  
  
 如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱[COLLATE &#40;TRANSACT-SQL &#41;](~/t-sql/statements/collations.md).  
  
> [!NOTE]  
>  自主資料庫的定序方式不同於非自主資料庫。 請參閱[Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)如需詳細資訊。  
  
 與\<選項 >  
 -   **\<filestream_options>** 
  
     NON_TRANSACTED_ACCESS = { **OFF** |READ_ONLY |完整}  
**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
     指定資料庫層級的非交易式 FILESTREAM 存取層級。  
  
    |Value|Description|  
    |-----------|-----------------|  
    |OFF|已停用非交易式存取|  
    |READONLY|非交易式處理序可以讀取此資料庫中的 FILESTREAM 資料。|  
    |FULL|已啟用 FILESTREAM FileTables 的完整非交易式存取。|  
  
     DIRECTORY_NAME = \<directory_name >**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     Windows 相容的目錄名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有 Database_Directory 名稱之間，此名稱必須是唯一的。 不論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 定序設定為何，唯一性比較不區分大小寫。 在此資料庫中建立 FileTable 之前，應該先設定這個選項。  
  
 只有當 CONTAINMENT 已經設為 PARTIAL 時，才允許下列選項。 如果 CONTAINMENT 設定為 NONE，便會發生錯誤。  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<lcid > |\<語言名稱 > |\<語言別名 >**  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<lcid > |\<語言名稱 > |\<語言別名 >**  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = { OFF | ON}**  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS = { OFF | ON}**  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = {2049年 |\<介於 1753年到 9999 之間的任何年份 >}**  
  
     表示一年的四位數。 2049 是預設值。 請參閱[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)這個選項的完整說明。  
  
-   **DB_CHAINING {關閉 |ON}**  
  
     當指定 ON 時，資料庫可以是跨資料庫擁有權鏈結的來源或目標。  
  
     當指定 OFF 時，資料庫不能參與跨資料庫擁有權鏈結。 預設值為 OFF。  
  
    > [!IMPORTANT]  
    >  當 cross db ownership chaining 伺服器選項為 0 (OFF) 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體可以辨識這項設定。 當 cross db ownership chaining 為 1 (ON) 時，不論這個選項的值為何，所有使用者資料庫都可以參與跨資料庫擁有權鏈結。 使用此選項設定[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
     若要設定這個選項，則需要有系統管理員 (sysadmin) 固定伺服器角色的成員資格。 您不能在下列系統資料庫上設定 DB_CHAINING 選項：master、model、tempdb。  
  
-   **TRUSTWORTHY {關閉 |ON}**  
  
     當指定 ON 時，使用模擬內容的資料庫模組 (例如，檢視表、使用者定義函數或預存程序) 可以存取資料庫外部的資源。  
  
     當指定 OFF 時，模擬內容中的資料庫模組不能存取資料庫外部的資源。 預設值為 OFF。  
  
     每當附加資料庫時，TRUSTWORTHY 都設為 OFF。  
  
     依預設，除了 msdb 資料庫以外，所有的系統資料庫都會將 TRUSTWORTHY 設為 OFF。 model 和 tempdb 資料庫的這個值不可變更。 建議您絕對不要將 master 資料庫的 TRUSTWORTHY 選項設為 ON。  
  
     若要設定這個選項，則需要有系統管理員 (sysadmin) 固定伺服器角色的成員資格。  
  
 FOR ATTACH [WITH \< attach_database_option >] 所建立的資料庫指定[附加](../../relational-databases/databases/database-detach-and-attach-sql-server.md)一組現有的作業系統檔案。 必須要有\<filespec > 項目，指定主要檔案。 只有其他\<filespec > 所需的項目是擁有不同的路徑，從第一個資料庫時的任何檔案建立或最後一次附加。 A \<filespec > 項目必須指定這些檔案。  
  
 FOR ATTACH 需要下列項目：  
  
-   所有資料檔案 (MDF 和 NDF) 都必須是可用的。  
  
-   如果存在多個記錄檔，它們必須全部都是可用的。  
  
 如果讀取/寫入資料庫有目前無法使用的單一記錄檔，且在進行附加作業之前，資料庫因為沒有使用者或開啟的交易而關閉，則 FOR ATTACH 會自動重建記錄檔並更新主要檔案。 反之，如果是唯讀資料庫，則會因為無法更新主要檔案而無法重建記錄。 因此，當您所附加的唯讀資料庫之記錄無法使用時，您必須在 FOR ATTACH 子句中提供記錄檔或檔案。  
  
> [!NOTE]  
>  由較新版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所建立的資料庫無法附加在舊版本中。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，所附加之資料庫中的任何全文檢索檔案，都會隨著資料庫而一起附加。 若要指定全文檢索目錄的新路徑，請指定一個不含全文檢索作業系統檔案名稱的新位置。 如需詳細資訊，請參閱＜範例＞一節。  
  
 附加資料庫，其中包含 [目錄名稱] 的 FILESTREAM 選項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體將會提示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證 Database_Directory 名稱是否唯一。 如果不是，附加作業會失敗，錯誤，「 FILESTREAM Database_Directory 名稱\<名稱 > 不是這個 SQL Server 執行個體中唯一的 」。 若要避免這個錯誤，選擇性參數， *directory_name*，則應傳入給此作業。  
  
 資料庫快照集中無法指定 FOR ATTACH。  
  
 FOR ATTACH 可以指定 RESTRICTED_USER 選項。 RESTRICTED_USER 只允許 db_owner 固定資料庫角色以及資料庫建立者 (dbcreator) 和系統管理員 (sysadmin) 固定伺服器角色的成員連接到資料庫，但並不限制他們的數目。 不合格的使用者嘗試連接遭到拒絕。  
  
 如果資料庫使用[!INCLUDE[ssSB](../../includes/sssb-md.md)]，使用 WITH \<service_broker_option > FOR ATTACH 子句中： 
  
 \<service_broker_option > 控制項[!INCLUDE[ssSB](../../includes/sssb-md.md)]訊息傳遞和[!INCLUDE[ssSB](../../includes/sssb-md.md)]資料庫識別項。 只有在使用 FOR ATTACH 子句的情況下才能指定 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 選項。  
  
 ENABLE_BROKER  
 指定啟用指定之資料庫的 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。 也就是說，訊息傳遞已啟動，且 is_broker_enabled 必須設為 true，在 sys.databases 目錄檢視中。 資料庫會保留現有的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別碼。  
  
 NEW_BROKER   
 在 sys.databases 和還原的資料庫中，建立新的 service_broker_guid 值，並以清除結束所有交談端點。 它會啟用 Broker，但不會傳送任何訊息到遠端交談端點。 您必須使用新的識別碼來重新建立參考舊 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別碼的任何路由。  
  
 ERROR_BROKER_CONVERSATIONS  
 結束所有交談，並顯示一則指出已附加或還原資料庫的錯誤。 Broker 將保持停用，直到這項作業完成之後才會啟用。 資料庫會保留現有的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別碼。  
  
 當您附加的複寫資料庫是複製而非卸離時，請考慮下列各項：  
  
-   如果您要將資料庫附加至與原始資料庫相同的伺服器執行個體和版本，則不需要其他步驟。  
  
-   如果您將資料庫附加至相同的伺服器執行個體，但升級後的版本，您必須執行[sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md)附加作業完成之後，升級複寫。  
  
-   如果您將資料庫附加至不同的伺服器執行個體，不限於任何版本，您必須執行[sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)附加作業完成之後移除複寫。  
  
> [!NOTE]  
> 附加作業可使用**vardecimal**儲存格式，但是[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]必須至少升級為[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]SP2。 您不能將使用 Vardecimal 儲存格式的資料庫附加到舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關**vardecimal**儲存格式，請參閱[資料壓縮](../../relational-databases/data-compression/data-compression.md)。  
  
 當資料庫第一次連接或還原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時，資料庫主要金鑰複本 (由服務主要金鑰加密) 尚未儲存在伺服器中。 您必須利用 **OPEN MASTER KEY** 陳述式來解密資料庫主要金鑰 (DMK)。 DMK 解密之後，您便可以選擇利用 **ALTER MASTER KEY REGENERATE** 陳述式來提供服務主要金鑰 (SMK) 所加密的 DMK 複本給伺服器，以在未來啟用自動解密。 當資料庫從舊版升級時，應該會重新產生 DMK 以使用較新的 AES 演算法。 如需重新產生 DMK 的詳細資訊，請參閱 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新產生 DMK 金鑰以升級至 AES 所需的時間是取決於 DMK 所保護的物件數目而定。 重新產生 DMK 金鑰以升級至 AES 只需執行一次，且不會影響金鑰循環策略中後續的重新產生。 如需如何升級使用的資料庫附加，請參閱[升級資料庫使用卸離和附加 &#40;TRANSACT-SQL &#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md).  
  
> [!IMPORTANT]  
> 建議您不要附加來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 您使用從未知或未受信任來源的資料庫之前，先執行[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)在非生產伺服器上，在資料庫上同時檢查程式碼，例如預存程序或其他使用者定義的程式碼，在資料庫中。  
  
> [!NOTE]  
> **TRUSTWORTHY**和**DB_CHAINING**附加資料庫時，選項會有任何影響。  
  
 FOR ATTACH_REBUILD_LOG  
 指定資料庫是藉由附加一組現有的作業系統檔案所建立。 這個選項只適用於讀取/寫入資料庫。 必須要有 *\<filespec >*指定主要檔案的項目。 如果遺漏一個或多個交易記錄檔，記錄檔就會重建。 ATTACH_REBUILD_LOG 會自動建立新的 1 MB 記錄檔。 這個檔案會放置在預設的記錄檔位置中。 此位置的相關資訊，請參閱[檢視或變更預設位置的資料及記錄檔 &#40;SQL Server Management Studio &#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
> [!NOTE]  
>  如果記錄檔是可用的，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會使用這些檔案，而不會重建記錄檔。  
  
 FOR ATTACH_REBUILD_LOG 需要下列項目：  
  
-   正常關閉資料庫。  
  
-   所有資料檔案 (MDF 和 NDF) 都必須是可用的。  
  
> [!IMPORTANT]  
> 這項作業會中斷記錄備份鏈結。 建議您在作業完成之後執行完整的資料庫備份。 如需詳細資訊，請參閱 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)。  
  
 一般而言，如果您要將一個含有大型記錄的讀/寫資料庫複製到其他伺服器，而該伺服器中，因為資料庫副本大部分用在讀取作業或只用在讀取作業，所以所需的記錄空間比原始資料庫少，在這種情況下，通常就會使用 FOR ATTACH_REBUILD_LOG。  
  
 資料庫快照集中無法指定 FOR ATTACH_REBUILD_LOG。  
  
 如需有關附加及卸離資料庫的詳細資訊，請參閱[資料庫卸離和附加 &#40;SQL Server &#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 \<filespec>  
 控制檔案屬性。  
  
 NAME *logical_file_name*  
 指定檔案的邏輯名稱。 除非指定其中一個 FOR ATTACH 子句，否則指定 FILENAME 時，NAME 是必要的。 FILESTREAM 檔案群組不能命名為 PRIMARY。  
  
 *logical_file_name*  
 這是在參考檔案時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所用的邏輯名稱。 *邏輯檔案名稱*必須在資料庫中是唯一且必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 名稱可以是字元或 Unicode 常數，或是一般識別碼或分隔識別碼。  
  
 檔名 { **'***os_file_name***'** | **'***filestream_path***'** }  
 指定作業系統 (實體) 檔案名稱。  
  
 **'** *os_file_name* **'**  
 這是當您建立檔案時作業系統所使用的路徑和檔案名稱。 該檔案必須位於下列其中一個裝置：從中安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機伺服器、存放區域網路 [SAN] 或 iSCSI 型網路。 執行 CREATE DATABASE 陳述式之前，指定的路徑必須存在。 如需詳細資訊，請參閱＜備註＞一節中的「資料庫檔案和檔案群組」。  
  
 當指定檔案的 UNC 路徑時，可以設定 SIZE、MAXSIZE 和 FILEGROWTH 參數。  
  
 如果檔案在原始的分割區， *os_file_name*必須指定只有現有的未經處理資料分割的磁碟機代號。 每個原始分割區上只能建立一個資料檔案。  
  
 除非檔案是唯讀次要檔案，或者，資料庫是唯讀的，否則資料檔案不應該放在壓縮的檔案系統中。 記錄檔永遠不應放在壓縮的檔案系統中。  
  
 **'** *filestream_path* **'**  
 如果是 FILESTREAM 檔案群組，FILENAME 會參考儲存 FILESTREAM 資料所在的路徑。 到最後一個資料夾為止的路徑必須存在，而最後一個資料夾則不得存在。 例如，如果您指定 C:\MyFiles\MyFilestreamData 路徑，則在您執行 ALTER DATABASE 之前，C:\MyFiles 必須存在，但是 MyFilestreamData 資料夾不得存在。  
  
 檔案群組和檔案 (`<filespec>`) 必須在相同的陳述式中建立。  
  
 SIZE 和 FILEGROWTH 屬性不會套用到 FILESTREAM 檔案群組。  
  
 SIZE *size*  
 指定檔案的大小。  
  
 大小不能指定何時*os_file_name*指定為 UNC 路徑。 SIZE 不會套用到 FILESTREAM 檔案群組。  
  
 *size*  
 這是檔案的初始大小。  
  
 當*大小*未提供主要檔案，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用的模型資料庫中主要檔案大小。 模型的預設大小是 8 MB (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) 或 1 MB （適用於先前的版本）。 當指定了次要資料檔或記錄檔時，但*大小*檔案，未指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]將檔 8 MB (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) 或 1 MB （適用於先前的版本）。 所指定的主要檔案大小至少必須跟 model 資料庫的主要檔案大小一樣大。  
  
 您可以使用千位元組 (KB)、百萬位元組 (MB)、十億位元組 (GB) 或兆位元組 (TB) 後置詞。 預設值是 MB。 請指定一個整數，不包括小數點。 *大小*是整數值。 如果是大於 2147483647 的值，請使用較大的單位。  
  
 MAXSIZE *max_size*  
 指定檔案所能成長的大小上限。 MAXSIZE 不能指定何時*os_file_name*指定為 UNC 路徑。  
  
 *max_size*  
 這是檔案大小上限。 可以使用 KB、MB、GB 及 TB 後置詞。 預設值是 MB。 請指定一個整數，不包括小數點。 如果*max_size*未指定，檔案可成長直到磁碟已滿。 *Max_size*是整數值。 如果是大於 2147483647 的值，請使用較大的單位。  
  
 UNLIMITED  
 指定檔案可成長直到磁碟已滿。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，指定為無限成長的記錄檔，大小上限是 2 TB，資料檔案的大小上限是 16 TB。  
  
> [!NOTE]  
> 為 FILESTREAM 容器指定這個選項時沒有最大大小。 它會繼續成長，直到磁碟已滿。  
  
 FILEGROWTH *growth_increment*  
 指定檔案的自動成長遞增。 檔案的 FILEGROWTH 設定不能超過 MAXSIZE 設定。 FILEGROWTH 不得時指定*os_file_name*指定為 UNC 路徑。 FILEGROWTH 不會套用到 FILESTREAM 檔案群組。  
  
 *growth_increment*  
 這是每次需要新空間時，檔案所增加的空間量。  
  
 您可以利用 MB、KB、GB、TB 或百分比 (%) 來指定這個值。 如果指定的數字不含 MB、KB 或 % 後置詞，預設值是 MB。 當指定 % 時，成長遞增大小便是遞增發生時，檔案大小的指定百分比。 指定的大小會四捨五入到最接近的 64 KB，最小值是 64 KB。  
  
 0 值指出自動成長是關閉的，且不允許其他空間。  
  
 如果未指定 FILEGROWTH，預設值為：  
  
|版本|預設值|  
|-------------|--------------------|  
|開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|資料 64 MB。 記錄檔 64 MB。|  
|開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|資料 1 MB。 記錄檔 10%。|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 之前|資料 10%。 記錄檔 10%。|  
  
 \<filegroup>  
 控制檔案群組屬性。 資料庫快照集中無法指定檔案群組。  
  
 FILEGROUP *filegroup_name*  
 這是檔案群組的邏輯名稱。  
  
 *filegroup_name*  
 *filegroup_name*必須是唯一的資料庫中，而且不能是系統提供的名稱 PRIMARY 和 PRIMARY_LOG。 名稱可以是字元或 Unicode 常數，或是一般識別碼或分隔識別碼。 名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 CONTAINS FILESTREAM  
 指定檔案群組會將 FILESTREAM 二進位大型物件 (BLOB) 儲存在檔案系統中。  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定檔案群組將記憶體最佳化的資料儲存在檔案系統中。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。 每個資料庫只允許一個 MEMORY_OPTIMIZED_DATA 檔案群組。 如需建立來儲存記憶體最佳化資料檔案群組的程式碼範例，請參閱[建立記憶體最佳化資料表和原生編譯預存程序](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
 DEFAULT  
 指定具名的檔案群組必須是資料庫中的預設檔案群組。  
  
 *database_snapshot_name*  
 這是新資料庫快照集的名稱。 資料庫快照集名稱在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內必須是唯一的，且必須符合識別碼的規則。 *database_snapshot_name*最多可有 128 個字元。  
  
 ON **(**名稱 **=***邏輯檔案名稱***，** FILENAME **='***os_file_name***')** [**,**...*n* ]  
 若要建立資料庫快照集，請在來源資料庫中指定檔案清單。 必須個別指定所有資料檔案，快照集才能運作。 不過，記錄檔不能用在資料庫快照集。 資料庫快照集不支援 FILESTREAM 檔案群組。 如果 FILESTREAM 資料檔案包含在 CREATE DATABASE ON 子句中，此陳述式將會失敗，並引發錯誤。  
  
 如需名稱和檔案名稱以及其值的描述，請參閱的對等項目描述\<filespec > 值。  
  
> [!NOTE]  
> 當您建立資料庫快照集，另\<filespec > 不允許選項和關鍵字 PRIMARY。  
  
 AS SNAPSHOT OF *source_database_name*  
 指定正在建立的資料庫是資料庫快照集所指定的來源資料庫的*source_database_name*。 該快照集和來源資料庫必須位於相同的執行個體上。  
  
 如需詳細資訊，請參閱＜備註＞一節中的「資料庫快照集」。  
  
## <a name="remarks"></a>備註  
 [Master 資料庫](../../relational-databases/databases/master-database.md)應該備份每當建立、 修改或卸除使用者資料庫。  
  
 CREATE DATABASE 陳述式必須在自動認可模式 (預設交易管理模式) 下執行，而且不能用於明確或隱含的交易。  
  
 您可使用 CREATE DATABASE 陳述式建立資料庫與儲存資料庫的檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用下列步驟實作 CREATE DATABASE 陳述式：  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會使用一份[model 資料庫](../../relational-databases/databases/model-database.md)初始化資料庫和它的中繼資料。  
  
2.  將 Service Broker GUID 指派給資料庫。  
  
3.  之後，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會在其餘的資料庫中填入空白頁面，但不包括含有記錄資料庫中空間使用方式之內部資料的頁面。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的一個執行個體上，最多可以指定 32,767 個資料庫。  
  
 每個資料庫都有一個可以在資料庫中執行特殊活動的擁有者。 該擁有者就是建立資料庫的使用者。 資料庫擁有者可以透過變更[sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)。  

某些資料庫功能依賴功能或功能存在於資料庫的完整功能的檔案系統。 取決於檔案系統功能集功能的一些範例包括：
- DBCC CHECKDB
- FileStream
- 使用 VSS 和檔案的快照集的線上備份
- 建立資料庫快照集
- 記憶體最佳化資料檔案群組
   
## <a name="database-files-and-filegroups"></a>資料庫檔案與檔案群組  
 每個資料庫都至少兩個檔案，*主要檔案*和*交易記錄檔*，以及至少一個檔案群組。 每個資料庫最多可以指定 32,767 個檔案和 32,767 個檔案群組。  
  
 當您建立資料庫時，請根據資料庫的預期最大資料量，盡可能擴大資料檔案。  
  
 建議您利用存放區域網路 (SAN)、iSCSI 型網路或本機連接的磁碟來儲存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫檔案，因為這個組態可使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 效能和可靠性最佳化。  
  
## <a name="database-snapshots"></a>資料庫快照集  
 您可以使用 CREATE DATABASE 陳述式建立的唯讀、 靜態檢視，*資料庫快照集*的*來源資料庫*。 資料庫快照集在交易上與來源資料庫是一致的，因為它是在快照集建立時即存在。 來源資料庫可以有多個快照集。  
  
> [!NOTE]  
> 當您建立資料庫快照集時，CREATE DATABASE 陳述式無法參考記錄檔、離線檔案、還原檔案及已解除功能的檔案。  
  
 如果建立資料庫快照集失敗，快照集會受到質疑且必須刪除。 如需詳細資訊，請參閱[DROP DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-database-transact-sql.md).  
  
 每個快照集都會繼續保存，直到利用 DROP DATABASE 加以刪除為止。  
  
 如需詳細資訊，請參閱[資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="database-options"></a>資料庫選項  
 每當您建立資料庫時，系統就會自動設定數個資料庫選項。 如需這些選項的清單，請參閱[ALTER DATABASE SET 選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="the-model-database-and-creating-new-databases"></a>model 資料庫和建立新資料庫  
 中的所有使用者定義物件[model 資料庫](../../relational-databases/databases/model-database.md)都會複製到所有新建立的資料庫。 您可以將所有要併入新建立之資料庫中的任何物件 (如資料表、檢視表、預存程序、資料類型等) 加入至 model 資料庫。  
  
 建立資料庫時*database_name*陳述式指定不含其他大小參數 model 資料庫中主要資料檔進行相同的主要檔案的大小。  
  
 除非指定 FOR ATTACH，否則每個新資料庫都會從 model 資料庫繼承資料庫選項設定。 例如，auto shrink 資料庫選項設定為**true**在於模型和您所建立的任何新資料庫。 如果您在 model 資料庫中變更選項，您建立的任何新資料庫也會使用這些新的選項設定。 變更 model 資料庫中的作業不會影響現有的資料庫。 如果在 CREATE DATABASE 陳述式上指定 FOR ATTACH，新資料庫就會繼承原始資料庫的資料庫選項設定。  
  
## <a name="viewing-database-information"></a>檢視資料庫資訊  
 您可以利用目錄檢視、系統函數和系統預存程序，以傳回資料庫、檔案和檔案群組的相關資訊。 如需詳細資訊，請參閱[系統檢視 &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)。  
  
## <a name="permissions"></a>Permissions  
 需要 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 權限。  
  
 為了維護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的磁碟控制，通常只有少數登入帳戶有建立資料庫的權限。  
  
 下列範例會將建立資料庫的權限提供給資料庫使用者 Fay。  
  
```sql  
USE master;  
GO  
GRANT CREATE DATABASE TO [Fay];  
GO  
```  
  
### <a name="permissions-on-data-and-log-files"></a>資料和記錄檔的權限  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，某些權限是針對每個資料庫的資料檔案和記錄檔所設定。 每當在資料庫上套用下列作業時，都會設定下列權限：  
  
|||  
|-|-|  
|建立日期|修改以加入新檔案|  
|已附加|已備份|  
|已卸離|已還原|  
  
 檔案所在的目錄如有開放權限，上述權限可防止檔案遭到意外竄改。  
  
> [!NOTE]  
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 不會設定資料和記錄檔的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-database-without-specifying-files"></a>A. 建立資料庫但不指定檔案  
 下列範例會建立資料庫 `mytest` 並建立相對應的主要記錄檔和交易記錄檔。 因為陳述式沒有\<filespec > 項目，主要資料庫檔案是 model 資料庫主要檔案的大小。 交易記錄設為下列兩個值中之較大者：512KB 或主要資料檔案大小的 25%。 因為沒有指定 MAXSIZE，所以檔案會成長，直到填滿所有可用的磁碟空間為止。 此範例也會示範如何在建立 `mytest` 資料庫之前，卸除名為 `mytest` 的資料庫 (若存在)。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;  
GO  
-- Verify the database files and sizes  
SELECT name, size, size*1.0/128 AS [Size in MBs]   
FROM sys.master_files  
WHERE name = N'mytest';  
GO  
```  
  
### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>B. 建立指定資料檔案和交易記錄檔的資料庫  
 下列範例會建立資料庫 `Sales`。 因為未使用關鍵字 PRIMARY，所以第一個檔案 (`Sales_dat`) 會成為主要檔案。 因為 `Sales_dat` 檔的 SIZE 參數中沒有指定 MB 或 KB，所以它會使用 MB 並 MB 來配置。 每當建立、修改或卸除使用者資料庫時，都應該備份 `Sales_log` 檔會以 MB 為單位配置，因為 `MB` 參數中明確陳述 `SIZE` 後置詞。  
  
```sql  
USE master;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. 利用指定多個資料檔案和交易記錄檔的方式建立資料庫  
 下列範例會建立資料庫 `Archive`，這個資料庫有三個 `100-MB` 的資料檔案和兩個 `100-MB` 的交易記錄檔。 主要檔案是清單中的第一個檔案，並以關鍵字 `PRIMARY` 明確指定。 交易記錄檔是以關鍵字 `LOG ON` 指定的。 請注意 `FILENAME` 選項中之檔案的副檔名：`.mdf` 用於主要資料庫，`.ndf` 用於次要資料檔案，`.ldf` 則用於交易記錄檔。 此範例會將此資料庫放在 `D:` 磁碟機上，而不是與 `master` 資料庫放在一起。  
  
```sql  
USE master;  
GO  
CREATE DATABASE Archive   
ON  
PRIMARY    
    (NAME = Arch1,  
    FILENAME = 'D:\SalesData\archdat1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch2,  
    FILENAME = 'D:\SalesData\archdat2.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch3,  
    FILENAME = 'D:\SalesData\archdat3.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20)  
LOG ON   
   (NAME = Archlog1,  
    FILENAME = 'D:\SalesData\archlog1.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
   (NAME = Archlog2,  
    FILENAME = 'D:\SalesData\archlog2.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20) ;  
GO  
```  
  
### <a name="d-creating-a-database-that-has-filegroups"></a>D. 建立含有檔案群組的資料庫  
 下列範例會建立含有下列檔案群組的資料庫 `Sales`：  
  
-   主要檔案群組與檔案`Spri1_dat`和`Spri2_dat`。 這些檔案的 FILEGROWTH 遞增指定為 `15%`。  
  
-   名為 `SalesGroup1` 的檔案群組，該檔案群組含有檔案 `SGrp1Fi1` 和 `SGrp1Fi2`。  
  
-   名為 `SalesGroup2` 的檔案群組，該檔案群組含有檔案 `SGrp2Fi1` 和 `SGrp2Fi2`。  
  
 此範例將資料和記錄檔放在不同的磁碟上，藉此改進效能。  
  
```sql  
USE master;  
GO  
CREATE DATABASE Sales  
ON PRIMARY  
( NAME = SPri1_dat,  
    FILENAME = 'D:\SalesData\SPri1dat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
( NAME = SPri2_dat,  
    FILENAME = 'D:\SalesData\SPri2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
FILEGROUP SalesGroup1  
( NAME = SGrp1Fi1_dat,  
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp1Fi2_dat,  
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
FILEGROUP SalesGroup2  
( NAME = SGrp2Fi1_dat,  
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp2Fi2_dat,  
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'E:\SalesLog\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="e-attaching-a-database"></a>E. 附加資料庫  
 下列範例會先卸離在範例 D 中建立的資料庫 `Archive`，再利用 `FOR ATTACH` 子句附加該資料庫。 `Archive` 定義為具有多個資料檔案和記錄檔。 不過，因為檔案建立之後並未改變位置，所以在 `FOR ATTACH` 子句中只需要指定主要檔案。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，所附加之資料庫中的任何全文檢索檔案，都會隨著資料庫而一起附加。  
  
```sql  
USE master;  
GO  
sp_detach_db Archive;  
GO  
CREATE DATABASE Archive  
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')   
      FOR ATTACH ;  
GO  
```  
  
### <a name="f-creating-a-database-snapshot"></a>F. 建立資料庫快照集  
 下列範例會建立資料庫快照集`sales_snapshot0600`。 因為資料庫快照集是唯讀的，所以不能指定記錄檔。 依照語法規定，會指定來源資料庫中的每個檔案，但不會指定檔案群組。  
  
 這個範例中的來源資料庫就是在範例 D 中建立的資料庫 `Sales`。  
  
```sql  
USE master;  
GO  
CREATE DATABASE sales_snapshot0600 ON  
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),  
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),  
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),  
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),  
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),  
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')  
AS SNAPSHOT OF Sales ;  
GO  
```  
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. 建立資料庫並指定定序名稱和選項  
 下列範例會建立資料庫 `MyOptionsTest`。 它指定定序名稱，並將 `TRUSTYWORTHY` 和 `DB_CHAINING` 選項設為 `ON`。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE French_CI_AI  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO  
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. 附加已移動的全文檢索目錄  
 下列範例會附加全文檢索目錄 `AdvWksFtCat` 以及 `AdventureWorks2012` 資料檔案和記錄檔。 在這個範例中，全文檢索目錄會從預設位置移至新的位置 `c:\myFTCatalogs`。 資料檔案和記錄檔仍保留在它們的預設位置中。  
  
```sql  
USE master;  
GO  
--Detach the AdventureWorks2012 database  
sp_detach_db AdventureWorks2012;  
GO  
-- Physically move the full text catalog to the new location.  
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.  
CREATE DATABASE AdventureWorks2012 ON   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),  
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')  
FOR ATTACH;  
GO  
```  
  
### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>I. 建立可指定一個資料列檔案群組和兩個 FILESTREAM 檔案群組的資料庫  
 下列範例會建立 `FileStreamDB` 資料庫。 此資料庫是使用一個資料列檔案群組和兩個 FILESTREAM 檔案群組所建立。 每個檔案群組都包含一個檔案：  
  
-   `FileStreamDB_data` 包含資料列資料， 它包含一個檔案 `FileStreamDB_data.mdf` (具有預設路徑)。  
  
-   `FileStreamPhotos` 包含 FILESTREAM 資料。 其也包含兩個 FILESTREAM 資料容器：一個是位於 `FSPhotos` 的 `C:\MyFSfolder\Photos`，一個是位於 `FSPhotos2` 的 `D:\MyFSfolder\Photos`。 它會標示為預設的 FILESTREAM 檔案群組。  
  
-   `FileStreamResumes` 包含 FILESTREAM 資料。 其包含一個 FILESTREAM 資料容器 `FSResumes` (位於 `C:\MyFSfolder\Resumes`)。  
  
```sql  
USE master;  
GO  
-- Get the SQL Server data path.  
DECLARE @data_path nvarchar(256);  
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)  
                  FROM master.sys.master_files  
                  WHERE database_id = 1 AND file_id = 1);  
  
 -- Execute the CREATE DATABASE statement.   
EXECUTE ('CREATE DATABASE FileStreamDB  
ON PRIMARY   
    (  
    NAME = FileStreamDB_data   
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''  
    ,SIZE = 10MB  
    ,MAXSIZE = 50MB  
    ,FILEGROWTH = 15%  
    ),  
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT  
    (  
    NAME = FSPhotos  
    ,FILENAME = ''C:\MyFSfolder\Photos''  
-- SIZE and FILEGROWTH should not be specified here.  
-- If they are specified an error will be raised.  
, MAXSIZE = 5000 MB  
    ),  
    (  
      NAME = FSPhotos2  
      , FILENAME = ''D:\MyFSfolder\Photos''  
      , MAXSIZE = 10000 MB  
     ),  
FILEGROUP FileStreamResumes CONTAINS FILESTREAM  
    (  
    NAME = FileStreamResumes  
    ,FILENAME = ''C:\MyFSfolder\Resumes''  
    )   
LOG ON  
    (  
    NAME = FileStream_log  
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''  
    ,SIZE = 5MB  
    ,MAXSIZE = 25MB  
    ,FILEGROWTH = 5MB  
    )'  
);  
GO  
```  
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. 建立包含多個檔案之 FILESTREAM 檔案群組的資料庫  
 下列範例會建立 `BlobStore1` 資料庫。 此資料庫是使用一個資料列檔案群組和一個 FILESTREAM 檔案群組 `FS` 所建立。 FILESTREAM 檔案群組包含兩個檔案：`FS1` 和 `FS2`。 然後，此範例會將第三個檔案 `FS3` 加入至 FILESTREAM 檔案群組，藉以改變資料庫。  
  
```sql  
USE master;  
GO  
  
CREATE DATABASE [BlobStore1]  
CONTAINMENT = NONE  
ON PRIMARY   
(   
    NAME = N'BlobStore1',   
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = UNLIMITED,  
    FILEGROWTH = 1MB  
),   
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT   
(  
    NAME = N'FS1',  
    FILENAME = N'C:\BlobStore\FS1',  
    MAXSIZE = UNLIMITED  
),   
(  
    NAME = N'FS2',  
    FILENAME = N'C:\BlobStore\FS2',  
    MAXSIZE = 100MB  
)  
LOG ON   
(  
    NAME = N'BlobStore1_log',  
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 1GB,  
    FILEGROWTH = 1MB  
);  
GO  
  
ALTER DATABASE [BlobStore1]  
ADD FILE  
(  
    NAME = N'FS3',  
    FILENAME = N'C:\BlobStore\FS3',  
    MAXSIZE = 100MB  
)  
TO FILEGROUP [FS];  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_changedbowner &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [移動資料庫檔案](../../relational-databases/databases/move-database-files.md)   
 [資料庫](../../relational-databases/databases/databases.md)   
 [二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  

