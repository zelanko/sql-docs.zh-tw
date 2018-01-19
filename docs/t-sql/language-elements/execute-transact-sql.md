---
title: "執行 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXEC
- EXECUTE_TSQL
- EXECUTE
- EXEC_TSQL
dev_langs: TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- command strings [SQL Server]
- extended stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- Transact-SQL statements, executing
- strings [SQL Server], executing
- statements [SQL Server], executing
- context switching [SQL Server], execution context
- user-defined functions [SQL Server], executing
- character strings [SQL Server], executing
- switching execution context
- EXECUTE statement
ms.assetid: bc806b71-cc55-470a-913e-c5f761d5c4b7
caps.latest.revision: "104"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5c9081d53346bda14d507688547f37589bd153da
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="execute-transact-sql"></a>EXECUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

執行命令字串或字元字串內[!INCLUDE[tsql](../../includes/tsql-md.md)]批次或其中一個下列模組： 系統預存程序、 使用者定義預存程序、 CLR 預存程序、 純量值使用者定義函數或擴充預存程序。 EXECUTE 陳述式可用來將傳遞命令傳送到連結伺服器。 另外，執行字串或命令所在的內容也可以明確設定。 結果集的中繼資料可透過 WITH RESULT SETS 來定義。
  
> [!IMPORTANT]  
>  在您利用字元字串呼叫 EXECUTE 之前，請先驗證該字元字串。 千萬不要執行從未經驗證的使用者輸入所建構的命令。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
  
```  
-- In-Memory OLTP   

Execute a natively compiled, scalar user-defined function  
[ { EXEC | EXECUTE } ]   
    {   
      [ @return_status = ]   
      { module_name | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable   
                           | [ DEFAULT ]   
                           }  
        ]   
      [ ,...n ]   
      [ WITH <execute_option> [ ,...n ] ]   
    }  
<execute_option>::=  
{  
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}  
```  
  
```  
-- Syntax for Azure SQL Database   
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name  | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH RECOMPILE ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS {  USER } = ' name ' ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML  
  
```  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Execute a stored procedure  
[ { EXEC | EXECUTE } ]  
    procedure_name   
        [ { value | @variable [ OUT | OUTPUT ] } ] [ ,...n ] }  
[;]  
  
-- Execute a SQL string  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'tsql_string' } [ +...n ] )  
[;]  
```  
  
## <a name="arguments"></a>引數  
 @*return_status*  
 這是儲存模組傳回狀態的選擇性整數變數。 這個變數必須先在批次、預存程序或函數中宣告之後，才能用在 EXECUTE 陳述式。  
  
 當用來叫用純量值使用者定義函數時，@*return_status*變數可以是任何純量資料類型。  
  
 *module_name*  
 這是您要呼叫的預存程序或純量值使用者定義函數的完整或不完整名稱。 模組名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 無論伺服器定序為何，擴充預存程序的名稱一定有大小寫區分。  
  
 已在另一個資料庫建立的模組，如果執行它的使用者擁有它，或者具有適當的權限可以在該資料庫執行它，就可以執行這個模組。 如果執行某個模組的使用者，具有適當的權限可以使用該伺服器 (遠端存取)，以及在該資料庫中執行該模組，就可以在另一個執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的伺服器上執行該模組。 如果指定了伺服器名稱，但沒有指定資料庫名稱，則 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會在該使用者的預設資料庫中尋找該模組。  
  
 ;*number*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 這是用來將同名程序分組的選擇性整數。 這個參數不用於擴充預存程序。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 如需程序群組的詳細資訊，請參閱[CREATE PROCEDURE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 @*module_name_var*  
 這是在本機定義的變數名稱，它代表模組名稱。  
  
 這可以是保存的原生編譯純量使用者定義函數名稱的變數。  
  
 @*parameter*  
 是參數*適於*，如在模組中定義。 參數名稱前面必須加上 @ 記號 (@)。 當搭配 @*parameter_name*=*值*表單，參數名稱和常數不必提供模組中定義的順序。 不過，如果 @*parameter_name*=*值*表單會使用任何參數，必須用於所有後續的參數。  
  
 依預設，參數可為 Null。  
  
 *value*  
 這是要傳遞到模組或傳遞命令的參數值。 如果未指定參數名稱，參數值就必須依照模組所定義的順序來提供。  
  
 在對連結伺服器執行傳遞命令時，參數值的順序會隨著連結伺服器的 OLE DB 提供者而不同。 大部分的 OLE DB 提供者，都會將值由左到右繫結到參數。  
  
 如果參數值是物件名稱、字元字串或者由資料庫名稱或結構描述名稱所限定，則必須以單引號括住整個名稱。 如果參數值是關鍵字，則必須以雙引號括住關鍵字。  
  
 如果預設值是在模組中定義，使用者就可以直接執行該模組，不必指定參數。  
  
 預設值也可以是 NULL。 通常，模組定義會指定當參數值為 NULL 時，應該採取什麼動作。  
  
 @*variable*  
 這是儲存參數或傳回參數的變數。  
  
 OUTPUT  
 指定讓模組或命令字串傳回參數。 模組或命令字串中的相符參數也必須先利用 OUTPUT 關鍵字加以建立。 當您把資料指標變數當做參數使用時，請使用這個關鍵字。  
  
 如果*值*定義為針對連結的伺服器時，對應的任何變更執行模組的輸出*參數*執行 OLE db 提供者將會複製到結尾的變數執行模組。  
  
 如果 OUTPUT 參數使用，目的是要呼叫的批次或模組內的其他陳述式中使用傳回值參數的值必須傳遞為變數，例如*參數*= @*變數*. 您不可以針對未在模組中定義為 OUTPUT 參數的參數指定 OUTPUT 來執行模組。 您不可以使用 OUTPUT 將常數傳遞到模組；傳回參數需要一個變數名稱。 在執行該程序之前，必須先宣告該變數的資料類型，並且指定一個值。  
  
 當 EXECUTE 針對遠端預存程序使用時，或者針對連結伺服器執行傳遞命令時，OUTPUT 參數就不能是任何一種大型物件 (LOB) 資料類型。  
  
 傳回參數可以是 LOB 資料類型以外的任何資料類型。  
  
 DEFAULT  
 提供模組所定義的參數預設值。 如果該模組所預期的參數值並沒有定義的預設值，而且不是遺漏一個參數，就是指定了 DEFAULT 關鍵字，此時就會發生錯誤。  
  
 @*string_variable*  
 這是區域變數的名稱。 @*string_variable*可以是任何**char**， **varchar**， **nchar**，或**nvarchar**資料型別。 這些包括**(max)**資料型別。  
  
 [N] '*tsql_string*'  
 常數字串。 *tsql_string*可以是任何**nvarchar**或**varchar**資料型別。 如果包含 N，則字串會解譯為**nvarchar**資料型別。  
  
 AS \<context_specification>  
 指定執行陳述式的內容。  
  
 登入  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定您要模擬的內容是登入。 模擬範圍是伺服器。  
  
 USER  
 指定您要模擬的內容是目前資料庫中的使用者。 模擬範圍僅限於目前資料庫。 通往資料庫使用者的內容切換不會繼承該使用者的伺服器層級權限。  
  
> [!IMPORTANT]  
>  如果通往資料庫使用者的內容切換在使用中，任何人想要存取資料庫以外的資源，都會導致陳述式失敗。 這包括使用*資料庫*陳述式、 分散式的查詢和使用三或四部分識別碼來參考另一個資料庫的查詢。  
  
 '*name*'  
 有效的使用者或登入名稱。 *名稱*必須是 sysadmin 固定的伺服器角色的成員，或者以主體形式存在於[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)或[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)分別。  
  
 *名稱*不得為內建帳戶，例如 NT AUTHORITY\LocalService、 NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
 如需詳細資訊，請參閱[指定使用者或登入名稱](#_user)本主題稍後。  
  
 [N] '*command_string*'  
 這是包含要傳遞到連結伺服器之命令的常數字串。 如果包含 N，則字串會解譯為**nvarchar**資料型別。  
  
 [?]  
 指出的參數的值中提供\<引數清單 > EXEC('...', \<arg-list>) 在中使用的傳遞命令的\<at > 陳述式。  
  
 AT *linked_server_name*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定*command_string*針對執行*linked_server_name*和結果，如果有的話，會傳回至用戶端。 *linked_server_name*必須參考本機伺服器中現有的連結的伺服器定義。 您可以使用連結的伺服器定義[sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)。  
  
 WITH \<execute_option>  
 可能的執行選項。 INSERT…EXEC 陳述式中不可指定 RESULT SETS 選項。  
  
|詞彙|定義|  
|----------|----------------|  
|RECOMPILE|在執行模組之後，強制編譯、使用和捨棄新計畫。 如果該模組有現有的查詢計畫，這個計畫便會保留在快取中。<br /><br /> 如果您所提供的參數不合規則，或者如果資料已經大幅變更，請使用這個選項。 這個選項不適用於擴充預存程序。 我們建議您少用這個選項，因為它的成本很高。<br /><br /> **注意：**您無法使用 WITH RECOMPILE 時呼叫的預存程序會使用 OPENDATASOURCE 語法。 指定物件名稱四部分時，會忽略 WITH RECOMPILE 選項。<br /><br /> **注意：**原生編譯純量使用者定義函數不支援 RECOMPILE。 如果您需要重新編譯時，使用[sp_recompile &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md).|  
|**未定義的結果集**|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 這個選項不保證會傳回何種結果 (如果有的話)，也不提供定義。 如果傳回任何結果或未傳回結果，陳述式會正確無誤地執行。 如果未提供 result_sets_option，RESULT SETS UNDEFINED 是預設行為。<br /><br /> 進行解譯純量使用者定義函式和原生編譯純量使用者定義函數，這個選項不是操作因為函式永遠不會傳回結果集。|  
|RESULT SETS NONE|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 保證 Execute 陳述式不會傳回任何結果。 如果傳回任何結果，會中止批次。<br /><br /> 進行解譯純量使用者定義函式和原生編譯純量使用者定義函數，這個選項不是操作因為函式永遠不會傳回結果集。|  
|*\<result_sets_definition>*|**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 保證結果會依 result_sets_definition 中所指定傳回。 針對陳述式傳回多個結果集，提供多個*result_sets_definition*區段。 將每個*result_sets_definition*括弧括住，以逗號分隔。 如需詳細資訊，請參閱\<result_sets_definition > 本主題稍後。<br /><br /> 此選項一律會產生錯誤，而原生編譯純量使用者定義函數，因為函式永遠不會傳回結果集。|
  
\<result_sets_definition >**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 描述執行的陳述式所傳回的結果集。 result_sets_definition 子句有下列的意義  
  
|詞彙|定義|  
|----------|----------------|  
|{<br /><br /> column_name<br /><br /> data_type<br /><br /> [ COLLATE collation_name]<br /><br /> [NULL &#124;NOT NULL]<br /><br /> }|請參閱下表。|  
|db_name|包含資料表、檢視表或資料表值函式的資料庫名稱。|  
|schema_name|擁有資料表、檢視表或資料表值函式的結構描述名稱。|  
|table_name &#124;view_name &#124;table_valued_function_name|指定傳回的資料行將會是具名資料表、檢視表或資料表值函式中所指定的資料行。 AS 物件語法不支援資料表變數、暫存資料表和同義字。|  
|AS TYPE [schema_name.]table_type_name|指定傳回的資料行將會是資料表類型中所指定的資料行。|  
|AS FOR XML|指定 EXECUTE 陳述式所呼叫的陳述式或預存程序產生的 XML 結果將會轉換成格式，如同 SELECT …  FOR XML … 所產生。 陳述式。 來自原始陳述式中型別指示詞的所有格式都會移除，而傳回的結果會如同未指定任何型別指示詞。 AS FOR XML 不會將非 XML 表格式結果從執行的陳述式或預存程序轉換為 XML。|  
  
|詞彙|定義|  
|----------|----------------|  
|column_name|每個資料行的名稱。 如果資料行數目不同於結果集，就會發生錯誤並且中止批次。 如果資料行名稱不同於結果集，傳回的資料行名稱會設為已定義的名稱。|  
|data_type|每個資料行的資料類型。 如果資料類型不同，則會隱含轉換成已定義的資料類型。 如果轉換失敗，則會中止批次。|  
|COLLATE collation_name|每個資料行的定序。 如果定序不符，則會嘗試隱含定序。 如果定序失敗，則會中止批次。|  
|NULL &#124;不是 NULL|每個資料行的 Null 屬性。 如果已定義的 Null 屬性是 NOT NULL，而且傳回的資料包含 NULL，則會發生錯誤並且中止批次。 如果未指定，預設值就會符合 ANSI_NULL_DFLT_ON 和 ANSI_NULL_DFLT_OFF 選項的設定值。|  
  
 執行期間傳回的實際結果集可能在下列方面不同於透過 WITH RESULT SETS 選項所定義的結果：結果集數目、資料行數目、資料行名稱、Null 屬性和資料類型。 如果結果集數目不同，就會發生錯誤並且中止批次。  
  
## <a name="remarks"></a>備註  
 參數可以使用提供*值*或使用*parameter_name*=*值。* 來提供參數。參數不是交易的一部分；因此，如果交易中的參數變更之後再回復，參數值並不會還原為之前的值。 傳回呼叫端的值一定是模組傳回時的值。  
  
 當一個模組呼叫另一個模組，或者參考 Common Language Runtime (CLR) 模組、使用者定義類型或彙總來執行 Managed 程式碼時，就會產生巢狀結構。 當被呼叫的模組或 Managed 程式碼參考開始執行時，巢狀層級便開始累加；而當被呼叫的模組或 Managed 程式碼參考完成時，就開始遞減。 如果超過 32 個巢狀層級上限，完整的呼叫鏈便會失敗。 目前的巢狀層級會儲存在 @@NESTLEVEL系統函數。  
  
 由於遠端預存程序和擴充預存程序不在交易範圍內 (除非在 BEGIN DISTRIBUTED TRANSACTION 陳述式中發出，或者搭配各種組態選項使用)，因此透過呼叫它們來執行的命令將無法回復。 如需詳細資訊，請參閱[系統預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)和[開始分散式交易 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 當您使用資料指標變數時，如果您執行的程序所傳遞的資料指標變數配置了一個資料指標，此時就會發生錯誤。  
  
 在執行模組時，如果陳述式是批次中的第一個陳述式，則不必指定 EXECUTE 關鍵字。  
  
 如需 CLR 預存程序特定的詳細資訊，請參閱＜CLR 預存程序＞。  
  
## <a name="using-execute-with-stored-procedures"></a>搭配預存程序使用 EXECUTE  
 當您執行預存程序時，如果陳述式是批次中的第一個陳述式，則不必指定 EXECUTE 關鍵字。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統預存程序是以 sp_ 字元開頭。 它們實際上儲存在[Resource 資料庫](../../relational-databases/databases/resource-database.md)，但邏輯上會出現在每個系統和使用者定義資料庫的 sys 結構描述。 當您在批次或模組內 (例如，使用者定義的預存程序或函數) 執行系統預存程序時，我們建議您以 sys 結構描述名稱來限定預存程序名稱。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統擴充預存程序是以 xp_ 字元開頭，而且這些字元包含在 master 資料庫的 dbo 結構描述中。 當您在批次或模組內 (例如，使用者定義的預存程序或函數) 執行系統擴充預存程序時，我們建議您以 master.dbo 來限定預存程序的名稱。  
  
 當您在批次或模組內 (例如，使用者定義的預存程序或函數) 執行使用者定義的預存程序時，我們建議您以結構描述名稱來限定預存程序名稱。 我們不建議您使用與系統預存程序相同的名稱，為使用者定義預存程序命名。 如需有關如何執行預存程序的詳細資訊，請參閱[執行預存程序](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)。  
  
## <a name="using-execute-with-a-character-string"></a>搭配字元字串使用 EXECUTE  
 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，字元字串不能超過 8,000 位元組。 這需要串連大型字串來進行動態執行工作。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 **varchar （max)**和**nvarchar （max)**字元字串最多為 2 gb 的資料可讓您可以指定資料型別。  
  
 您對資料庫內容所做的變更，只會維持到 EXECUTE 陳述式結束為止。 例如，當下面這個陳述式中的 `EXEC` 執行之後，資料庫內容為 master。  
  
```sql  
USE master; EXEC ('USE AdventureWorks2012; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');  
```  
  
## <a name="context-switching"></a>內容切換  
 您可以使用 `AS { LOGIN | USER } = ' name '` 子句來切換動態陳述式的執行內容。 當內容切換被指定為 `EXECUTE ('string') AS <context_specification>` 時，內容切換的持續時間就限於目前所執行的查詢範圍內。  
  
###  <a name="_user"></a>指定使用者或登入名稱  
 `AS { LOGIN | USER } = ' name '` 中所指定的使用者或登入名稱，必須以主體形式分別存在於 sys.database_principals 或  sys.server_principal 中，否則陳述式就會失敗。 此外，還必須授與主體的 IMPERSONATE 權限。 除非呼叫端是資料庫擁有者或是系統管理員 (sysadmin) 固定伺服器角色的成員，否則主體必須存在，即使當使用者透過 Windows 群組成員資格存取資料庫或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時也一樣。 例如，假設有下列情況：  
  
-   CompanyDomain\SQLUsers 群組擁有 Sales 資料庫的存取權。  
  
-   CompanyDomain\SqlUser1 是 SQLUsers 的成員，因此對 Sales 資料庫具有隱含的存取權。  
  
 雖然 CompanyDomain\SqlUser1 有權存取透過成員資格資料庫 SQLUsers 群組，請在陳述式`EXECUTE @string_variable AS USER = 'CompanyDomain\SqlUser1'`會失敗，因為`CompanyDomain\SqlUser1`做為主體資料庫中不存在。  
  
### <a name="best-practices"></a>最佳作法  
 指定一個登入或使用者，它具有執行在陳述式或模組中定義的作業時所需要的最低權限。 例如，如果只需要資料庫層級權限，就不要指定具有伺服器層級權限的登入名稱；或者除非需要其權限，否則不要指定資料庫擁有者帳戶。  
  
## <a name="permissions"></a>Permissions  
 執行 EXECUTE 陳述式不需要任何權限。 不過，您必須對 EXECUTE 字串內所參考的安全性實體具備權限。 例如，如果字串包含 INSERT 陳述式，EXECUTE 陳述式的呼叫端就必須有目標資料表的 INSERT 權限。 遇到 EXECUTE 陳述式時會檢查權限，即使模組內包含 EXECUTE 陳述式也一樣。  
  
 模組的 EXECUTE 權限預設會授與模組的擁有者，這位擁有者可以將這些權限轉讓給其他使用者。 當您執行某個模組來執行字串時，將會檢查執行此模組之使用者內容中的權限，不過不會檢查建立模組之使用者內容中的權限。 然而，如果同一位使用者擁有呼叫模組，而該模組正被呼叫時，第二個模組就不會再檢查一次 EXECUTE 權限。  
  
 如果模組要存取其他資料庫物件，只要您具有該模組的 EXECUTE 權限，而且下列一項為真，就可以順利執行：  
  
-   模組被標示為 EXECUTE AS USER 或 SELF，而且模組擁有者具有參考物件的對應權限。 如需模組中模擬的詳細資訊，請參閱[EXECUTE AS 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
-   模組被標示為 EXECUTE AS CALLER，而且您具有物件的對應權限。  
  
-   模組標示為 EXECUTE AS *user_name*，和*user_name*具有對應的權限的物件。  
  
### <a name="context-switching-permissions"></a>內容切換權限  
 若要指定某項登入的 EXECUTE AS 權限，則這位呼叫端必須具有指定之登入名稱的 IMPERSONATE 權限。 若要指定資料庫使用者的 EXECUTE AS 權限，則這位呼叫端必須具有指定之使用者名稱的 IMPERSONATE 權限。 如果未指定任何執行內容，或者沒有指定 EXECUTE AS CALLER，就不需要 IMPERSONATE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-execute-to-pass-a-single-parameter"></a>A. 使用 EXECUTE 傳遞單一參數  
 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的 `uspGetEmployeeManagers` 預存程序預期需要一個參數 (`@EmployeeID`)。 下列範例會執行`uspGetEmployeeManagers`預存程序與`Employee ID 6`做為其參數值。  
  
```  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
 此變數可以在執行作業中明確命名：  
  
```  
EXEC dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
 如果符合下列條件的批次中的第一個陳述式或**osql**或**sqlcmd**指令碼，即不需要 EXEC。  
  
```  
dbo.uspGetEmployeeManagers 6;  
GO  
--Or  
dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
### <a name="b-using-multiple-parameters"></a>B. 使用多個參數  
 下列範例會執行 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的 `spGetWhereUsedProductID` 預存程序。 它會傳遞兩個參數：第一個參數是產品識別碼 (`819`)，第二個參數 `@CheckDate,` 則是 `datetime` 值。  
  
```  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
### <a name="c-using-execute-tsqlstring-with-a-variable"></a>C. 使用 EXECUTE 'tsql_string' 與變數  
 下列範例會示範 `EXECUTE` 如何處理含有變數的動態建立字串。 這個範例會建立 `tables_cursor` 資料指標來保存一份 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中所有使用者定義資料表的清單，然後再利用這份清單在資料表上重建所有的索引。  
  
```  
DECLARE tables_cursor CURSOR  
   FOR  
   SELECT s.name, t.name   
   FROM sys.objects AS t  
   JOIN sys.schemas AS s ON s.schema_id = t.schema_id  
   WHERE t.type = 'U';  
OPEN tables_cursor;  
DECLARE @schemaname sysname;  
DECLARE @tablename sysname;  
FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN;  
   EXECUTE ('ALTER INDEX ALL ON ' + @schemaname + '.' + @tablename + ' REBUILD;');  
   FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
END;  
PRINT 'The indexes on all tables have been rebuilt.';  
CLOSE tables_cursor;  
DEALLOCATE tables_cursor;  
GO  
  
```  
  
### <a name="d-using-execute-with-a-remote-stored-procedure"></a>D. 使用 EXECUTE 與遠端預存程序  
 下列範例會在遠端伺服器 `uspGetEmployeeManagers` 中執行 `SQLSERVER1` 預存程序，並且儲存傳回狀態，指出 `@retstat` 是成功還是失敗。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
DECLARE @retstat int;  
EXECUTE @retstat = SQLSERVER1.AdventureWorks2012.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;  
```  
  
### <a name="e-using-execute-with-a-stored-procedure-variable"></a>E. 使用 EXECUTE 與預存程序變數  
 下列範例會建立一個代表預存程序名稱的變數。  
  
```sql  
DECLARE @proc_name varchar(30);  
SET @proc_name = 'sys.sp_who';  
EXEC @proc_name;  
  
```  
  
### <a name="f-using-execute-with-default"></a>F. 使用 EXECUTE 與 DEFAULT  
 下列範例會針對第一個和第三個參數採用預設值來建立預存程序。 在執行程序時，如果呼叫中沒有傳遞任何值，或者如果未指定預設值，就會針對第一個和第三個參數插入這些預設值。 請注意各種可以使用 `DEFAULT` 關鍵字的方法。  
  
```  
IF OBJECT_ID(N'dbo.ProcTestDefaults', N'P')IS NOT NULL  
   DROP PROCEDURE dbo.ProcTestDefaults;  
GO  
-- Create the stored procedure.  
CREATE PROCEDURE dbo.ProcTestDefaults (  
@p1 smallint = 42,   
@p2 char(1),   
@p3 varchar(8) = 'CAR')  
AS   
   SET NOCOUNT ON;  
   SELECT @p1, @p2, @p3  
;  
GO  
  
```  
  
 您可以利用多種組合執行 `Proc_Test_Defaults` 預存程序。  
  
```  
-- Specifying a value only for one parameter (@p2).  
EXECUTE dbo.ProcTestDefaults @p2 = 'A';  
-- Specifying a value for the first two parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'B';  
-- Specifying a value for all three parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'C', 'House';  
-- Using the DEFAULT keyword for the first parameter.  
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';  
-- Specifying the parameters in an order different from the order defined in the procedure.  
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';  
-- Using the DEFAULT keyword for the first and third parameters.  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'I', @p3 = DEFAULT;  
  
```  
  
### <a name="g-using-execute-with-at-linkedservername"></a>G. 使用 EXECUTE 與 AT linked_server_name  
 下列範例會傳遞一個命令字串到遠端伺服器。 它會建立一個連結伺服器 `SeattleSales`，指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一個執行個體，然後針對該連結伺服器執行 DDL 陳述式 (`CREATE TABLE`)。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
EXECUTE ( 'CREATE TABLE AdventureWorks2012.dbo.SalesTbl   
(SalesID int, SalesName varchar(10)) ; ' ) AT SeattleSales;  
GO  
```  
  
### <a name="h-using-execute-with-recompile"></a>H. 使用 EXECUTE WITH RECOMPILE  
 下列範例會執行`Proc_Test_Defaults`預存程序，強制編譯、 新的查詢計劃使用，而且執行模組之後捨棄。  
  
```  
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;  
GO  
```  
  
### <a name="i-using-execute-with-a-user-defined-function"></a>I. 使用 EXECUTE 與使用者定義函數  
 下列範例會執行 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的 `ufnGetSalesOrderStatusText` 純量使用者定義函數。 它會使用變數 `@returnstatus` 來儲存該函數所傳回的值。 該函數會預期接受一個輸入參數 `@Status`。 這定義為**tinyint**資料型別。  
  
```  
DECLARE @returnstatus nvarchar(15);  
SET @returnstatus = NULL;  
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;  
PRINT @returnstatus;  
GO  
```  
  
### <a name="j-using-execute-to-query-an-oracle-database-on-a-linked-server"></a>J. 使用 EXECUTE 查詢連結伺服器上的 Oracle 資料庫  
 下列範例會執行遠端 Oracle 伺服器上的幾個 `SELECT` 陳述式。 這個範例一開始就加入 Oracle 伺服器當做連結伺服器，並且建立連結伺服器登入。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver    
        @server='ORACLE',  
        @srvproduct='Oracle',  
        @provider='OraOLEDB.Oracle',   
        @datasrc='ORACLE10';  
  
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname='ORACLE',  
    @useself='false',   
    @locallogin=null,   
    @rmtuser='scott',   
    @rmtpassword='tiger';  
  
EXEC sp_serveroption 'ORACLE', 'rpc out', true;  
GO  
  
-- Execute several statements on the linked Oracle server.  
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;  
GO  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;  
GO  
DECLARE @v INT;   
SET @v = 7902;  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;  
GO   
```  
  
### <a name="k-using-execute-as-user-to-switch-context-to-another-user"></a>K. 使用 EXECUTE AS USER 將內容切換到其他使用者  
 下列範例會執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 字串來建立一個資料表，以及指定 `AS USER` 子句，將陳述式的執行內容從呼叫端切換到 `User1`。 執行陳述式時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會檢查 `User1` 的權限。 `User1` 必須是資料庫中的使用者，並須具備在 `Sales` 結構描述中建立資料表的權限，否則陳述式將會失敗。  
  
```  
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')  
AS USER = 'User1';  
GO  
```  
  
### <a name="l-using-a-parameter-with-execute-and-at-linkedservername"></a>L. 使用 EXECUTE 與 AT linked_server_name  
 下列範例會使用問號 (`?`) 預留位置代表參數，將命令字串傳遞至遠端伺服器。 它會建立一個連結伺服器 `SeattleSales`，指向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一個執行個體，然後對該連結伺服器執行 `SELECT` 陳述式。 `SELECT` 陳述式會使用問號當做 `ProductID` 參數 (`952`) 的預留位置，而這會在陳述式之後提供。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
-- Execute the SELECT statement.  
EXECUTE ('SELECT ProductID, Name   
    FROM AdventureWorks2012.Production.Product  
    WHERE ProductID = ? ', 952) AT SeattleSales;  
GO  
```  
  
### <a name="m-using-execute-to-redefine-a-single-result-set"></a>M. 使用 EXECUTE 重新定義單一結果集  
 先前某些範例執行 `EXEC dbo.uspGetEmployeeManagers 6;`，傳回 7 個資料行。 下列範例示範如何使用 `WITH RESULT SET` 語法來變更傳回結果集的名稱和資料類型。  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
EXEC uspGetEmployeeManagers 16  
WITH RESULT SETS  
(   
   ([Reporting Level] int NOT NULL,  
    [ID of Employee] int NOT NULL,  
    [Employee First Name] nvarchar(50) NOT NULL,  
    [Employee Last Name] nvarchar(50) NOT NULL,  
    [Employee ID of Manager] nvarchar(max) NOT NULL,  
    [Manager First Name] nvarchar(50) NOT NULL,  
    [Manager Last Name] nvarchar(50) NOT NULL )  
);  
  
```  
  
### <a name="n-using-execute-to-redefine-a-two-result-sets"></a>N. 使用 EXECUTE 重新定義兩個結果集  
 當執行一個會傳回多個結果集的陳述式時，請定義每個預期的結果集。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的下列範例會建立一個可傳回兩個結果集的程序。 然後使用執行程序**WITH RESULT SETS**子句，並指定兩個結果集定義。  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
--Create the procedure  
CREATE PROC Production.ProductList @ProdName nvarchar(50)  
AS  
-- First result set  
SELECT ProductID, Name, ListPrice  
    FROM Production.Product  
    WHERE Name LIKE @ProdName;  
-- Second result set   
SELECT Name, COUNT(S.ProductID) AS NumberOfOrders  
    FROM Production.Product AS P  
    JOIN Sales.SalesOrderDetail AS S  
        ON P.ProductID  = S.ProductID   
    WHERE Name LIKE @ProdName  
    GROUP BY Name;  
GO  
  
-- Execute the procedure   
EXEC Production.ProductList '%tire%'  
WITH RESULT SETS   
(  
    (ProductID int,   -- first result set definition starts here  
    Name Name,  
    ListPrice money)  
    ,                 -- comma separates result set definitions  
    (Name Name,       -- second result set definition starts here  
    NumberOfOrders int)  
);  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="example-o-basic-procedure-execution"></a>範例 o： 基本的程序執行  
 執行預存程序：  
  
```  
EXEC proc1;  
```  
  
 在執行階段決定的名稱，以呼叫預存程序：  
  
```  
EXEC ('EXEC ' + @var);  
```  
  
 呼叫預存程序中的預存程序：  
  
```  
CREATE sp_first AS EXEC sp_second; EXEC sp_third;  
```  
  
### <a name="example-p-executing-strings"></a>範例 p： 執行字串  
 正在執行 SQL 字串：  
  
```  
EXEC ('SELECT * FROM sys.types');  
```  
  
 正在執行的巢狀的字串：  
  
```  
EXEC ('EXEC (''SELECT * FROM sys.types'')');  
```  
  
 正在執行的字串變數：  
  
```  
DECLARE @stringVar nvarchar(100);  
SET @stringVar = N'SELECT name FROM' + ' sys.sql_logins';  
EXEC (@stringVar);  
```  
  
### <a name="example-q-procedures-with-parameters"></a>問： 範例具有參數的程序  
 下列範例會建立具有參數的程序，並示範執行程序的 3 種方式：  
  
```  
-- Uses AdventureWorks  
  
CREATE PROC ProcWithParameters  
    @name nvarchar(50),  
@color nvarchar (15)  
AS   
SELECT ProductKey, EnglishProductName, Color FROM [dbo].[DimProduct]  
WHERE EnglishProductName LIKE @name  
AND Color = @color;  
GO  
  
-- Executing using positional parameters  
EXEC ProcWithParameters N'%arm%', N'Black';  
-- Executing using named parameters in order  
EXEC ProcWithParameters @name = N'%arm%', @color = N'Black';  
-- Executing using named parameters out of order  
EXEC ProcWithParameters @color = N'Black', @name = N'%arm%';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [@@NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE AS 子句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [osql 公用程式](../../tools/osql-utility.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [還原 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [SUSER_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [USER_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [OPENDATASOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [記憶體內部 OLTP 的純量使用者定義函數](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
  
  
