---
title: "建立函式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
caps.latest.revision: 162
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: c74e3a3322dcc2268fa8e386fda5d55f59be98c5
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中建立使用者定義函數。 使用者定義函數是一種 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 Common Language Runtime (CLR) 常式，它會接受參數、執行動作 (例如複雜計算) 並且將該動作的結果傳回成值。 傳回值可以是純量 (單一) 值或資料表。 您可以使用這個陳述式來建立可用下列方式使用的可重複使用常式：  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，例如 SELECT  
  
-   在呼叫函數的應用程式中  
  
-   在另一個使用者自訂函數的定義中  
  
-   若要將檢視參數化，或改善索引檢視的功能  
  
-   若要在資料表中定義資料行  
  
-   若要在資料行上定義 CHECK 條件約束  
  
-   取代預存程序  
  
-   做為篩選器述詞的內嵌函式用於安全性原則  
  
> [!NOTE]  
>  在本主題討論.NET Framework CLR 整合 SQL Server。 CLR 整合不適用於 Azure SQL Database。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
```  
  
```  
-- Transact-SQL Inline Table-Valued Function Syntax   
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
  
```  
  
```  
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
  
```  

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  
  
<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```  
  
```  
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
<method_specifier>::=  
    assembly_name.class_name.method_name  
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>引數
*或 ALTER*  
 **適用於**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1)。  
  
 只有當它已經存在，有條件地改變函式。 
 
> [!NOTE]  
>  CLR 的選擇性 [或 ALTER] 的語法就是開始可用之[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 CU1。   
 
 *schema_name*  
 這是使用者定義函數所屬的結構描述名稱。  
  
 *function_name*  
 這是使用者定義函數的名稱。 函數名稱必須符合的規則[識別碼](../../relational-databases/databases/database-identifiers.md)而且必須是唯一的資料庫內及對於它的結構描述。  
  
> [!NOTE]  
>  即使沒有指定參數，函數名稱後面仍需要括號。  
  
 @*parameter_name*  
 這是使用者定義函數中的參數。 您可以宣告一個或多個參數。  
  
 函數最多可以有 2,100 個參數。 除非定義了參數的預設值，否則在執行函數時，使用者必須提供每個已宣告之參數的值。  
  
 使用 @ 記號當做第一個字元來指定參數名稱。 參數名稱必須符合識別碼的規則。 對函數而言，參數必須是本機參數；相同的參數名稱可以用在其他函數中。 參數只能取代常數，不能用來取代資料表名稱、資料行名稱或其他資料庫物件的名稱。  
  
> [!NOTE]  
>  在預存程序或使用者定義函數中傳遞參數，或在批次陳述式中宣告和設定變數時，不接受 ANSI_WARNINGS。 例如，如果變數定義為**char （3)**，然後設定為超過 3 個字元，資料會截斷成定義的大小，而 INSERT 或 UPDATE 陳述式會成功。  
  
 [ *type_schema_name*。 ] *parameter_data_type*  
 這是參數資料類型，對於其所屬的結構描述而言為選擇性。 如[!INCLUDE[tsql](../../includes/tsql-md.md)]函式，所有的資料類型，包括 CLR 使用者定義型別和使用者定義資料表類型，除了允許**時間戳記**資料型別。 若是 CLR 函數，所有的資料類型，包括 CLR 使用者定義型別，允許除了**文字**， **ntext**，**映像**、 使用者定義資料表類型和**時間戳記**資料型別。 非純量類型，**游標**和**資料表**，不能指定中的參數資料類型為[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函數。  
  
 如果*type_schema_name*未指定，[!INCLUDE[ssDE](../../includes/ssde-md.md)]尋找*scalar_parameter_data_type*順序如下：  
  
-   內含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型名稱的結構描述。  
  
-   目前資料庫中之目前使用者的預設結構描述。  
  
-   目前資料庫中的 **dbo** 結構描述。  
  
 [=*預設*]  
 這是參數的預設值。 如果*預設*值定義、 可執行函式，但未指定該參數的值。  
  
> [!NOTE]  
>  針對 CLR 函數以外，可以指定預設參數值**varchar （max)**和**varbinary （max)**資料型別。  
  
 如果函數的參數有預設值，則必須在呼叫函數來擷取該預設值時指定關鍵字 DEFAULT。 這個行為與使用預存程序中具有預設值的參數不一樣，因為在預存程序中，省略參數也意味著使用預設值。 不過，使用 EXECUTE 陳述式來叫用純量函數時，不需要 DEFAULT 關鍵字。  
  
 READONLY  
 指示無法在函數的定義內更新或修改參數。 如果參數類型是使用者定義資料表類型，應該指定 READONLY。  
  
 *return_data_type*  
 這是純量使用者定義函數的傳回值。 如[!INCLUDE[tsql](../../includes/tsql-md.md)]函式，所有的資料類型，包括 CLR 使用者定義型別，允許除了**時間戳記**資料型別。 若是 CLR 函數，所有的資料類型，包括 CLR 使用者定義型別，允許除了**文字**， **ntext**，**映像**，和**時間戳記**資料型別。 非純量類型，**游標**和**資料表**，不能指定中的傳回資料類型為[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函數。  
  
 *function_body*  
 指定一系列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (並用這些陳述式並不會造成任何副作用，例如修改資料表等) 定義函數的值。 *function_body*只適用於純量函數和多重陳述式資料表值函式。  
  
 在純量函數， *function_body*是一系列的[!INCLUDE[tsql](../../includes/tsql-md.md)]一起評估純量值的陳述式。  
  
 在多重陳述式資料表值函數中， *function_body*是一系列的[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式會擴展 TABLE 傳回變數。  
  
 *scalar_expression*  
 指定純量函數傳回的純量值。  
  
 TABLE  
 指定資料表值函式的傳回值是資料表。 只有常數和 @*local_variables*可以傳遞至資料表值函式。  
  
 在內嵌資料表值函式中，TABLE 傳回值是利用單一 SELECT 陳述式所定義。 內嵌函數沒有相關聯的傳回變數。  
  
 在多重陳述式資料表值函數中，@*return_variable*是一個 TABLE 變數，用來儲存及累積應該當做函數值來傳回的資料列。 @*return_variable*可以指定僅適用於[!INCLUDE[tsql](../../includes/tsql-md.md)]函式並不能為 CLR 函數。  
  
> [!WARNING]  
>  加入多重陳述式資料表值函式中的**FROM**子句，但可提供效能不佳。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法針對可包含在多重陳述式函數中的某些陳述式使用所有最佳化技術，因此會產生次佳查詢計劃。 若要獲得最佳效能，請盡可能在基底資料表而非函數之間使用聯結。  
  
 *select_stmt*  
 這是單一 SELECT 陳述式，可定義嵌入資料表值函式的傳回值。  
  
 順序 (\<order_clause >) 會指定的順序中所傳回結果的資料表值函式。 如需詳細資訊，請參閱本主題稍後的＜使用排序次序的指引＞一節。  
  
 EXTERNAL NAME \<called > *assembly_name*。*class_name*。*method_name* **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定建立函式名稱時應該要參考的組件和方法。  
  
-   *assembly_name* -必須符合值的`name`資料行   
    `SELECT * FROM sys.assemblies;`。  
    這是 `CREATE ASSEMBLY` 陳述式中所使用的名稱。  
  
-   *class_name* -必須符合值的`assembly_name`資料行  
    `SELECT * FROM sys.assembly_modules;`。  
    值常包含內嵌的句號或點。 在此情況下 TRANSACT-SQL 語法需要使用一組直線方括號 []，，或以雙引號括住的一組一致值""。  
  
-   *method_name* -必須符合值的`method_name`資料行   
    `SELECT * FROM sys.assembly_modules;`。  
    方法必須為靜態。  
  
 在典型的範例中，針對所有類型皆位於 MyFood 命名空間的 MyFood.DLL，`EXTERNAL NAME` 的值可能是：   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
>  依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能執行 CLR 程式碼。 您可以建立、 修改和卸除參考 common language runtime 模組; 的資料庫物件不過，您無法執行這些參考在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直到您啟用[clr enabled 選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。 若要啟用此選項，使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
 *\<*table_type_definition *>*  ({ \<column_definition > \<column_constraint > |\<computed_column_definition >}   [ \<table_constraint >] [，... *n*  ]) 的資料表資料類型的定義[!INCLUDE[tsql](../../includes/tsql-md.md)]函式。 資料表宣告包括資料行定義和資料行或資料表條件約束。 資料表一律放在主要檔案群組中。  
  
 \<clr_table_type_definition > ({ *column_name**data_type* } [，... *n*  ])**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([某些區域處於預覽](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。 |  
  
 定義 CLR 函數的資料表資料類型。 資料表宣告只包含資料行名稱和資料類型。 資料表一律放在主要檔案群組中。  
  
 NULL |不是 NULL  
 僅支援原生編譯純量使用者定義函數。 如需詳細資訊，請參閱[記憶體內部 OLTP 的純量使用者定義函式](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
 NATIVE_COMPILATION  
 指出是否為原生編譯使用者定義函式。 原生編譯純量使用者定義函數需要這個引數。  
  
 開始使用不可部分完成  
 原生編譯的純量使用者定義函式，而無須才支援。 如需詳細資訊，請參閱 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  
  
 SCHEMABINDING  
 原生編譯純量使用者定義函數需要 SCHEMABINDING 引數。  
  
 EXECUTE AS  
 EXECUTE AS 則需要原生編譯純量使用者定義函數。  
  
 **\<function_option >:: = 和\<clr_function_option >:: =** 
  
 指定此函數將會有下列其中一個或多個選項。  
  
 ENCRYPTION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指出 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將 CREATE FUNCTION 陳述式的原始文字轉換為模糊化格式。 無法直接從任何目錄檢視中看見模糊化的輸出。 對系統資料表或資料庫檔案沒有存取權的使用者，無法擷取混亂格式的文字。 不過，將特殊權限可以存取系統資料表上的使用者可以使用文字[DAC 通訊埠](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)或直接存取資料庫檔案。 另外，可將偵錯工具附加至伺服器處理序的使用者，可以在執行階段從記憶體擷取原始程序。 如需有關存取系統中繼資料的詳細資訊，請參閱[中繼資料可見性組態](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
 使用此選項可防止在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫中發行這個函數。 無法為 CLR 函數指定此選項。  
  
 SCHEMABINDING  
 指定函數必須繫結到它所參考的資料庫物件。 當指定 SCHEMABINDING 時，無法依照會影響函數定義的方式來修改基底物件。 您必須先修改或卸除函數定義才能移除對於要修改之物件的相依性。  
  
 只有在下發生下列其中一個動作時，才會移除函數與其參考的物件之間的繫結： 
  
-   已卸除這個函數。  
  
-   您可以利用未指定 SCHEMABINDING 選項的 ALTER 陳述式來修改函數。  
  
 只有當下列條件成立時，函數才可繫結結構描述：  
  
-   函數是一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數。  
  
-   函數參考的使用者定義函數和檢視表也繫結結構描述。  
  
-   函數參考的物件是利用兩部分名稱來參考。  
  
-   函數及其參考的物件屬於相同的資料庫。  
  
-   執行 CREATE FUNCTION 陳述式的使用者在函數參考的資料庫物件上有 REFERENCES 權限。  
  
 NULL 輸入上傳回 NULL |**NULL 輸入上呼叫**  
 指定**OnNULLCall**純量值函式的屬性。 若未指定，預設情況下意味著 CALLED ON NULL INPUT。 這表示，即使傳遞 NULL 做為引數，函數主體仍會執行。  
  
 如果在 CLR 函數中指定 RETURNS NULL ON NULL INPUT，它會指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在它接收的任何引數是 NULL 時傳回 NULL，而不必實際叫用函數主體。 如果在指定的 CLR 函數方法\<called > 已經有一個指出 RETURNS NULL ON NULL INPUT，自訂屬性，但 CREATE FUNCTION 陳述式指出 ON NULL INPUT，CREATE FUNCTION 陳述式會採用優先順序。 **OnNULLCall**屬性不能指定為 CLR 資料表值函式。 
  
 EXECUTE AS 子句  
 指定執行使用者定義函數時所在的安全性內容。 因此，您可以控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 要利用哪個使用者帳戶來驗證在函數參考的任何資料庫物件上的權限。  
  
> [!NOTE]  
>  無法為內嵌使用者定義函數指定 EXECUTE AS。  
  
 如需詳細資訊，請參閱 [EXECUTE AS 子句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)。  
  
 **\<column_definition >:: =** 
  
 定義資料表資料類型。 資料表宣告包括資料行定義和條件約束。 若是 CLR 函數，僅*column_name*和*data_type*可以指定。  
  
 *column_name*  
 這是資料表中的資料行名稱。 資料行名稱必須符合識別碼規則，在資料表中也必須是唯一的。 *column_name*可以包含 1 到 128 個字元。  
  
 *data_type*  
 指定資料行資料類型。 如[!INCLUDE[tsql](../../includes/tsql-md.md)]函式，所有的資料類型，包括 CLR 使用者定義型別，允許除了**時間戳記**。 若是 CLR 函數，所有的資料類型，包括 CLR 使用者定義型別，允許除了**文字**， **ntext**，**映像**， **char**， **varchar**， **varchar （max)**，和**時間戳記**。非純量型別**游標**不能指定中的資料行資料類型為[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函數。  
  
 預設*constant_expression*  
 指定在插入期間未明確提供值時，提供給資料行的值。 *constant_expression*是常數、 NULL 或系統函數值。 除了含有 IDENTITY 屬性的資料行之外，任何資料行都可以套用 DEFAULT 定義。 無法為 CLR 資料表值函式指定 DEFAULT。  
  
 COLLATE *sys.databases*  
 指定資料行的定序。 若未指定，就會將資料庫的預設定序指派給資料行。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 清單和定序的詳細資訊，請參閱[Windows 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 COLLATE 子句可以用來變更的資料行的定序**char**， **varchar**， **nchar**，和**nvarchar**資料型別。  
  
 無法為 CLR 資料表值函式指定 COLLATE。  
  
 ROWGUIDCOL  
 指出新資料行是一個資料列全域唯一識別碼資料行。 只有一個**uniqueidentifier**每個資料表的資料行可以指定為 ROWGUIDCOL 資料行。 ROWGUIDCOL 屬性指派給只**uniqueidentifier**資料行。  
  
 ROWGUIDCOL 屬性不會強制執行資料行中所儲存之值的唯一性。 它也不會自動為插入資料表中的新資料列產生值。 若要為每個資料行產生唯一值，請在 INSERT 陳述式上使用 NEWID 函數。 可以指定預設值；不過，NEWID 不能指定為預設值。  
  
 IDENTITY  
 指出新資料行是識別欄位。 新資料列加入至資料表時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供資料行的唯一累加值。 識別欄位通常用來搭配 PRIMARY KEY 條件約束一起使用，當做資料表的唯一資料列識別碼。 IDENTITY 屬性可以指派給**tinyint**， **smallint**， **int**， **bigint**， **decimal(p,0)**，或**numeric(p,0)**資料行。 每份資料表都只能建立一個識別欄位。 繫結的預設值和 DEFAULT 條件約束無法搭配識別欄位使用。 您必須同時指定*種子*和*遞增*或兩者都關閉。 如果同時不指定這兩者，預設值便是 (1,1)。  
  
 無法為 CLR 資料表值函式指定 IDENTITY。  
  
 *種子*  
 這是要指派給資料表中第一個資料列的整數值。  
  
 *遞增*  
 要加入的整數值*種子*資料表中的後續資料列的值。  
  
 **\<column_constraint >:: = 和\<table_constraint >:: =** 
  
 定義指定之資料行或資料表的條件約束。 就 CLR 函數而言，唯一允許的條件約束類型是 NULL。 不允許具名條件約束。  
  
 NULL | NOT NULL  
 判斷資料行中是否允許 Null 值。 嚴格來說，NULL 並不算是條件約束，但是您可以如同指定 NOT NULL 一樣加以指定。 無法為 CLR 資料表值函式指定 NOT NULL。  
  
 PRIMARY KEY  
 這是一項條件約束，它利用唯一索引強制執行指定之資料行的實體完整性。 在資料表值使用者定義函數中，PRIMARY KEY 條件約束只能建立在每份資料表的一個資料行上。 無法為 CLR 資料表值函式指定 PRIMARY KEY。  
  
 UNIQUE  
 這是一項條件約束，它透過唯一索引為指定的一個或多個資料行提供實體完整性。 一份資料表可以有多個 UNIQUE 條件約束。 無法為 CLR 資料表值函式指定 UNIQUE。  
  
 CLUSTERED | NONCLUSTERED  
 指出針對 PRIMARY KEY 或 UNIQUE 條件約束建立叢集或非叢集索引。 PRIMARY KEY 條件約束使用 CLUSTERED，UNIQUE 條件約束則使用 NONCLUSTERED。  
  
 只能為一個條件約束指定 CLUSTERED。 如果針對 UNIQUE 條件約束指定 CLUSTERED，且指定了 PRIMARY KEY 條件約束，則 PRIMARY KEY 會使用 NONCLUSTERED。  
  
 無法為 CLR 資料表值函式指定 CLUSTERED 和 NONCLUSTERED。  
  
 CHECK  
 這是一個條件約束，藉由限制可能輸入一個或多個資料行的值，強制執行範圍完整性。 無法為 CLR 資料表值函式指定 CHECK 條件約束。  
  
 *logical_expression*  
 這是一個傳回 TRUE 或 FALSE 的邏輯運算式。  
  
 **\<computed_column_definition >:: =**  
  
 指定計算資料行。 如需有關計算資料行的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *column_name*  
 這是計算資料行的名稱。  
  
 *computed_column_expression*  
 這是定義計算資料行值的運算式。  
  
 **\<index_option >:: =**  
  
 指定 PRIMARY KEY 或 UNIQUE 索引的索引選項。 如需有關索引選項的詳細資訊，請參閱[CREATE INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = {ON |**OFF** }  
 指定索引填補。 預設值為 OFF。  
  
 填滿因數 =*填滿因數*  
 指定指出在建立或變更索引期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 各索引頁面之分葉層級填滿程度的百分比。 *填滿因數*必須是介於 1 到 100 之間的整數值。 預設值是 0。  
  
 IGNORE_DUP_KEY = {ON |**OFF** }  
 指定當插入作業嘗試將重複的索引鍵值插入唯一索引時所產生的錯誤回應。 IGNORE_DUP_KEY 選項只適用於在建立或重建索引之後所發生的插入作業。 預設值為 OFF。  
  
 STATISTICS_NORECOMPUTE = {ON |**OFF** }  
 指定是否要重新計算散發統計資料。 預設值為 OFF。  
  
 ALLOW_ROW_LOCKS = { **ON** |OFF}  
 指定是否允許資料列鎖定。 預設值是 ON。  
  
 ALLOW_PAGE_LOCKS = { **ON** |OFF}  
 指定是否允許頁面鎖定。 預設值是 ON。  
  
## <a name="best-practices"></a>最佳作法  
 如果未以 SCHEMABINDING 子句建立使用者定義函數，叫用該函數時，對基礎物件所進行的變更可能會影響函數的定義並產生非預期的結果。 建議您實作下列其中一個方法，以確保函數不會因為其基礎物件的變更而變成過期：  
  
-   當您要建立函數時，指定 WITH SCHEMABINDING 子句。 這可以確保系統無法修改函數定義中參考的物件 (除非同時修改函數)。  
  
-   執行[sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md)預存程序，在修改函式定義中指定任何物件之後。  
  
## <a name="data-types"></a>資料型別  
 如果 CLR 函數中指定的參數，則應該[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類型做為先前定義為*scalar_parameter_data_type*。 如需比較[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系統資料類型與 CLR 整合資料類型或[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]common language runtime 資料類型，請參閱[對應 CLR 參數資料](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]類別中多載時，請參考正確的方法，該方法所示\<called > 必須具有下列特性： 
  
-   接收相同數目的參數中所指定 [，...*n* ].  
  
-   依值 (而不是依參考) 接收所有參數。  
  
-   使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函數中指定之類型相容的參數類型。  
  
 如果傳回的資料類型的 CLR 函數指定資料表類型 (RETURNS TABLE) 中之方法的傳回資料類型\<called > 的類型應為**IEnumerator**或**IEnumerable**，且假設介面由函數建立者實作。 不同於[!INCLUDE[tsql](../../includes/tsql-md.md)]函式，CLR 函數不能包含主索引鍵、 UNIQUE 或 CHECK 條件約束，在\<table_type_definition >。 指定之資料行的資料型別\<table_type_definition > 必須符合對應的資料行中的方法所傳回的結果集的型別\<called > 在執行階段。 這項類型檢查作業不會在建立函數時執行。 
  
 如需如何編寫 CLR 函數的詳細資訊，請參閱[clr 使用者定義函數](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)。  
  
## <a name="general-remarks"></a>一般備註  
 純量值函式可在使用純量運算式的情況下進行叫用。 這包括計算資料行和 CHECK 條件約束定義。 純量值函式也可以執行使用[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)陳述式。 叫用純量值函式必須至少使用函數的兩部分名稱。 如需有關多部分名稱的詳細資訊，請參閱[TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 在 SELECT、INSERT、UPDATE 或 DELETE 陳述式的 FROM 子句中允許資料表運算式的情況下，就可以叫用資料表值函式。 如需詳細資訊，請參閱[執行使用者定義函數](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)。  
  
## <a name="interoperability"></a>互通性  
 以下是函數中的有效陳述式：  
  
-   指派陳述式。  
  
-   流程控制陳述式 (但不包括 TRY...CATCH 陳述式)。  
  
-   DECLARE 陳述式 - 定義本機資料變數和本機資料指標。  
  
-   SELECT 陳述式 - 包含選取清單，清單中含有指派值給區域變數的運算式。  
  
-   資料指標作業 - 參考函數中之已宣告、已開啟、已關閉及已取消配置的本機資料指標。 只允許利用 INTO 子句指派值給本機變數的 FETCH 陳述式，不允許將資料傳送至用戶端的 FETCH 陳述式。  
  
-   修改本機資料表變數的 INSERT、UPDATE 及 DELETE 陳述式。  
  
-   呼叫擴充預存程序的 EXECUTE 陳述式。  
  
-   如需詳細資訊，請參閱[建立使用者定義函數 &#40; Database Engine &#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)。  
  
### <a name="computed-column-interoperability"></a>計算資料行的互通性  
 函數具有下列屬性。 這些屬性的值會決定是否可以在可保存或索引的計算資料行中使用函數。  
  
|屬性|Description|注意|  
|--------------|-----------------|-----------|  
|**Columnproperty**|函數可分為具決定性或不具決定性。|具決定性函數中允許本機資料存取。 例如，每當利用一組特定輸入值來呼叫函數時都一律傳回相同結果且含有相同資料庫狀態的函數，就會被標示為具決定性。|  
|**IsPrecise**|函數可分為精確或不精確。|不精確函數內含浮點作業之類的作業。|  
|**IsSystemVerified**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以驗證函數的有效位數和決定性屬性。||  
|**SystemDataAccess**|函數會存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之本機執行個體中的系統資料 (系統目錄或虛擬系統資料表)。||  
|**UserDataAccess**|函數會存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之本機執行個體中的使用者資料。|包含使用者定義資料表和暫存資料表，但不包含資料表變數。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會自動判斷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函數的有效位數和決定性屬性。 使用者可以指定 CLR 函數的資料存取和決定性屬性。 如需詳細資訊，請參閱[概觀的 CLR 整合自訂屬性](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)。  
  
 若要顯示這些屬性的目前值，請使用[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)。  
  
 建立函數時，必須使用具決定性的結構描述繫結來建立。  
  
 當使用者定義函數有下列屬性值時，可以在索引中使用可叫用使用者定義函數的計算資料行。  
  
-   **Columnproperty** = true  
  
-   **IsSystemVerified** = true （除非保存計算資料行）  
  
-   **UserDataAccess** = false  
  
-   **SystemDataAccess** = false  
  
 如需詳細資訊，請參閱 [計算資料行的索引](../../relational-databases/indexes/indexes-on-computed-columns.md)。  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>從函數呼叫擴充預存程序  
 從函數內呼叫擴充預存程序時，擴充預存程序無法將結果集傳回用戶端。 任何將結果集傳回用戶端的 ODS API 都會傳回 FAIL。 擴充預存程序可能會連回到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體；不過，它不應該嘗試將相同的交易聯結為叫用擴充預存程序的函數。  
  
 與從批次或預存程序進行的引動過程相似，擴充預存程序會在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Windows 安全性帳戶所在的內容中執行。 當預存程序的擁有者將預存程序上的 EXECUTE 權限提供給使用者時，該擁有者應考量前述的情形。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 使用者定義函數不能用來執行修改資料庫狀態的動作。  
  
 使用者定義函數不得包含具有資料表當做其目標的 OUTPUT INTO 子句。  
  
 下列 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 陳述式不能併入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用者定義函數的定義中：  
  
-   BEGIN DIALOG CONVERSATION  
  
-   END CONVERSATION  
  
-   GET CONVERSATION GROUP  
  
-   MOVE CONVERSATION  
  
-   RECEIVE  
  
-   SEND  
  
 使用者定義函數可以具有巢狀結構；也就是說，某個使用者定義函數可以呼叫另一個使用者定義函數。 被呼叫的函數開始執行時，巢狀層級會遞增；被呼叫的函數完成執行時，巢狀層級會遞減。 使用者定義函數所建立的巢狀結構最多可以有 32 個層級。 超過巢狀層級上限會導致整個呼叫函數鏈結失敗。 依照 32 個層級巢狀限制，[!INCLUDE[tsql](../../includes/tsql-md.md)] 使用者定義函數之 Managed 程式碼的任何參考都算是一個層級。 從 Managed 程式碼內叫用的方法，不列入這項限制。  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>在 CLR 資料表值函式中使用排序次序  
 當您在 CLR 資料表值函式中使用 ORDER 子句時，請遵循以下指導方針：  
  
-   您必須確保結果一定會以指定的順序來排序。 如果結果未以指定的順序來排序，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會在執行查詢時產生錯誤訊息。  
  
-   如果指定了 ORDER 子句，資料表值函式的輸出必須根據資料行的定序 (明確或隱含) 來排序。 例如，如果資料行定序為中文 (指定在資料表值函式的 DDL 中或是從資料庫定序取得)，傳回的結果必須根據中文排序規則來排序。  
  
-   如果指定了 ORDER 子句，一定會在傳回結果時由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來加以驗證，不論查詢處理器是否會使用它來執行進一步的最佳化。 只有在您知道 ORDER 子句對查詢處理器很有用時，才能使用它。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器會在以下情況下自動利用 ORDER 子句：  
  
    -   當 ORDER 子句與索引相容時的插入查詢。  
  
    -   與 ORDER 子句相容的 ORDER BY 子句。  
  
    -   當 GROUP BY 與 ORDER 子句相容時的彙總。  
  
    -   當相異資料行與 ORDER 子句相容時的 DISTINCT 彙總。  
  
 除非同時在查詢內指定 ORDER BY 子句，否則 ORDER 子句並不保證在執行 SELECT 查詢時會傳回排序的結果。 請參閱[sys.function_order_columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md)如需有關如何查詢的資料行包含資料表值函式在排序次序資訊。  
  
## <a name="metadata"></a>中繼資料  
 下表列出您可以用來傳回使用者定義函數之中繼資料的系統目錄檢視表。  
  
|系統檢視表|Description|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|請參閱下面的範例 > 一節中的範例 E。|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|顯示 CLR 使用者定義函數的相關資訊。|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|顯示使用者定義函數中定義之參數的相關資訊。|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|顯示函數所參考的基礎物件。|  
  
## <a name="permissions"></a>Permissions  
 需要資料庫中的 CREATE FUNCTION 權限，以及此函數建立所在之結構描述上的 ALTER 權限。 如果此函數指定使用者定義型別，則需要該型別的 EXECUTE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>A. 使用計算 ISO 週的純量值使用者定義函數  
 下列範例會建立使用者定義函數 `ISOweek`。 這個函數採用日期引數並計算 ISO 週數。 若要使函數能夠正確計算，必須先叫用 `SET DATEFIRST 1`，才能呼叫該函數。  
  
 此範例也示範使用[EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md)子句來指定可以執行預存程序的安全性內容。 在這個範例中，選項 `CALLER` 會指定將在呼叫程序之使用者的內容中執行程序。 您可以指定其他選項包括 SELF、 OWNER 和*user_name*。  
  
 以下是函數呼叫。 請注意，`DATEFIRST` 是設為 `1`。  
  
```tsql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. 建立內嵌資料表值函式  
 下列範例會傳回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的內嵌資料表值函式。 它會傳回三個資料行`ProductID`，`Name`和依商店的年度迄今總計的彙總`YTD Total`每項產品銷售給商店。  
  
```tsql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 若要叫用函數，請執行這項查詢。    

```tsql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>C. 建立多重陳述式資料表值函式  
 下列範例會在 AdventureWorks2012 資料庫中建立資料表值函式 `fn_FindReports(InEmpID)`。 當提供有效的員工識別碼時，此函數會傳回對應於所有員工的資料表，該資料表會直接或間接報告給員工。 此函數會利用遞迴通用資料表運算式 (CTE) 來產生階層式員工清單。 如需有關遞迴 Cte 的詳細資訊，請參閱[common_table_expression &#40; 與TRANSACT-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
```tsql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>D. 建立 CLR 函數  
 此範例會建立 CLR 函數`len_s`。 在建立這個函數之前，已在本機資料庫中註冊組件 `SurrogateStringFunction.dll`。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```tsql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 如需如何建立 CLR 資料表值函式的範例，請參閱[CLR Table-Valued 函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)。  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>E. 顯示的定義[!INCLUDE[tsql](../../includes/tsql-md.md)]使用者定義函式  
  
```tsql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 利用 ENCRYPTION 選項建立的函數定義無法利用 sys.sql_modules 來檢視，但是會顯示有關加密函數的其他資訊。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [卸除函數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CLR 使用者定義函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [建立安全性原則 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-security-policy-transact-sql.md)  
  
 


