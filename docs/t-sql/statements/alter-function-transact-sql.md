---
title: "ALTER FUNCTION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4b1008715d9cfd3e48945d0651f454253bc4e4bc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  改變先前執行 CREATE FUNCTION 陳述式所建立的現有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 CLR 函數，而不變更權限及不影響任何相依的函數、預存程序或觸發程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
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
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
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
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是使用者定義函數所屬的結構描述名稱。  
  
 *function_name*  
 這是要變更的使用者定義函數。  
  
> [!NOTE]  
>  即使沒有指定參數，函數名稱後面仍需要括號。  
  
 **@***parameter_name*  
 這是使用者定義函數中的參數。 您可以宣告一個或多個參數。  
  
 函數最多可以有 2,100 個參數。 除非定義了參數的預設值，否則在執行函數時，使用者必須提供每個已宣告之參數的值。  
  
 使用指定的參數名稱 @ 記號 (**@**) 作為第一個字元。 參數名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 對函數而言，參數必須是本機參數；相同的參數名稱可以用在其他函數中。 參數只能取代常數，不能用來取代資料表名稱、資料行名稱或其他資料庫物件的名稱。  
  
> [!NOTE]  
>  當在預存程序或使用者自訂函數中傳遞參數時，或在批次陳述式中宣告和設定變數時，會忽略 ANSI_WARNINGS。 例如，如果變數定義為**char （3)**，然後設定為超過 3 個字元，資料會截斷成定義的大小，而 INSERT 或 UPDATE 陳述式會成功。  
  
 [ *type_schema_name。* ] *parameter_data_type*  
 這是參數資料類型，對於其所屬的結構描述而言為選擇性。 如[!INCLUDE[tsql](../../includes/tsql-md.md)]函式，所有的資料類型，包括 CLR 使用者定義型別，允許除了**時間戳記**資料型別。 若是 CLR 函數，所有的資料類型，包括 CLR 使用者定義型別，允許除了**文字**， **ntext**，**映像**，和**時間戳記**資料型別。 非純量類型**游標**和**資料表**不能指定中的參數資料類型為[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函數。  
  
 如果*type_schema_name*未指定，[!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)]尋找*parameter_data_type*順序如下：  
  
-   內含 SQL Server 系統資料類型的結構描述。  
  
-   目前資料庫中之目前使用者的預設結構描述。  
  
-   目前資料庫中的 **dbo** 結構描述。  
  
 [  **=** *預設*]  
 這是參數的預設值。 如果*預設*值定義、 可執行函式，但未指定該參數的值。  
  
> [!NOTE]  
>  針對 CLR 函數以外，可以指定預設參數值**varchar （max)**和**varbinary （max)**資料型別。  
  
 如果函數的參數有預設值，則必須在呼叫函數來擷取該預設值時指定關鍵字 DEFAULT。 這個行為與使用預存程序中具有預設值的參數不一樣，因為在預存程序中，省略參數也意味著使用預設值。  
  
 *return_data_type*  
 這是純量使用者定義函數的傳回值。 如[!INCLUDE[tsql](../../includes/tsql-md.md)]函式，所有的資料類型，包括 CLR 使用者定義型別，允許除了**時間戳記**資料型別。 若是 CLR 函數，所有的資料類型，包括 CLR 使用者定義型別，允許除了**文字**， **ntext**，**映像**，和**時間戳記**資料型別。 非純量類型**游標**和**資料表**不能指定中的傳回資料類型為[!INCLUDE[tsql](../../includes/tsql-md.md)]或 CLR 函數。  
  
 *function_body*  
 指定一系列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (並用這些陳述式並不會造成任何副作用，例如修改資料表等) 定義函數的值。 *function_body*只適用於純量函數和多重陳述式資料表值函式。  
  
 在純量函數， *function_body*是一系列的[!INCLUDE[tsql](../../includes/tsql-md.md)]一起評估純量值的陳述式。  
  
 在多重陳述式資料表值函數中， *function_body*是一系列的[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式會擴展 TABLE 傳回變數。  
  
 *scalar_expression*  
 指定純量函數傳回純量值。  
  
 TABLE  
 指定資料表值函式的傳回值是資料表。 只有常數和 **@**  *local_variables*可以傳遞至資料表值函式。  
  
 在內嵌資料表值函式中，TABLE 傳回值是利用單一 SELECT 陳述式所定義。 內嵌函數沒有相關聯的傳回變數。  
  
 在多重陳述式資料表值函數中，  **@**  *return_variable*是一個 TABLE 變數，用來儲存及累積應該當做函數值來傳回的資料列。 **@***return_variable*可以指定僅適用於[!INCLUDE[tsql](../../includes/tsql-md.md)]函式並不能為 CLR 函數。  
  
 *select 陳述式*  
 這是單一 SELECT 陳述式，可定義嵌入資料表值函式的傳回值。  
  
 EXTERNAL NAME \<called >*assembly_name.class_name*。*method_name*  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定繫結函數之組件的方法。 *assembly_name*必須符合中的現有組件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的可見性的目前資料庫中。 *class_name*必須是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別項且必須是組件中的類別。 如果該類別具有命名空間限定的名稱是使用句號 (**。**) 來分隔命名空間的各個部分，必須分隔類別名稱使用方括號 (**[]**) 或引號 (**""**). *method_name*必須是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別項和必須存在於指定的類別中的靜態方法。  
  
> [!NOTE]  
>  依預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能執行 CLR 程式碼。 您可以建立、 修改和卸除參考 common language runtime 模組; 的資料庫物件不過，您無法執行這些參考在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直到您啟用[clr enabled 選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)。 若要啟用此選項，請使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
 *\<*table_type_definition*>***(** { \<column_definition > \<column_constraint > |\<computed_column_definition >}[ \<table_constraint >] [ **，**...*n* ]**)**  
 定義 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數的資料表資料類型。 資料表宣告包括資料行定義和資料行或資料表條件約束。  
  
\<clr_table_type_definition > **(** { *column_name**data_type* } [ **，**... *n*  ] **)** **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([部分中的預覽區域](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。  
  
 定義 CLR 函數的資料表資料類型。 資料表宣告只包含資料行名稱和資料類型。  
  
 NULL |不是 NULL  
 僅支援原生編譯純量使用者定義函數。 如需詳細資訊，請參閱[記憶體內部 OLTP 的純量使用者定義函式](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
 NATIVE_COMPILATION  
 指出是否為原生編譯使用者定義函式。 原生編譯純量使用者定義函數需要這個引數。  
  
 NATIVE_COMPILATION 引數時需要您變更函式，並僅適用於，如果函式已建立具有 NATIVE_COMPILATION 引數。  
  
 開始使用不可部分完成  
 原生編譯的純量使用者定義函式，而無須才支援。 如需詳細資訊，請參閱 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  
  
 SCHEMABINDING  
 原生編譯純量使用者定義函數需要 SCHEMABINDING 引數。  
  
 **\<function_option >:: = 和\<clr_function_option >:: =**  
  
 指定函數必須有下列其中一個或多個選項。  
  
 ENCRYPTION  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指出 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會對包含 ALTER FUNCTION 陳述式文字的目錄檢視表資料行進行加密。 使用 ENCRYPTION 可防止在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫中發行這個函數。 無法為 CLR 函數指定 ENCRYPTION。  
  
 SCHEMABINDING  
 指定函數必須繫結到它所參考的資料庫物件。 如果其他結構描述繫結的物件正在參考函數，這個條件可防止對函數進行變更。  
  
 只有在下發生下列其中一個動作時，才會移除函數與其參考的物件之間的繫結：  
  
-   已卸除這個函數。  
  
-   您可以利用未指定 SCHEMABINDING 選項的 ALTER 陳述式來修改函數。  
  
如需函數可以繫結的結構描述之前，必須符合的條件，請參閱[CREATE FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 指定**OnNULLCall**純量值函式的屬性。 若未指定，預設情況下意味著 CALLED ON NULL INPUT。 這表示，即使傳遞 NULL 做為引數，函數主體仍會執行。  
  
 如果在 CLR 函數中指定 RETURNS NULL ON NULL INPUT，它會指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在它接收的任何引數是 NULL 時傳回 NULL，而不必實際叫用函數主體。 如果此方法中指定\<called > 已經有一個指出 RETURNS NULL ON NULL INPUT，但 ALTER FUNCTION 陳述式表示 ON NULL INPUT，優先使用 ALTER FUNCTION 陳述式自訂屬性。 **OnNULLCall**屬性不能指定為 CLR 資料表值函式。  
  
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
 指定資料行的定序。 若未指定，就會將資料庫的預設定序指派給資料行。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 清單和詳細資訊，請參閱[Windows 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)和[SQL Server 定序名稱 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
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
  
 PAD_INDEX = { ON | OFF }  
 指定索引填補。 預設值為 OFF。  
  
 填滿因數 =*填滿因數*  
 指定指出在建立或變更索引期間，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 各索引頁面之分葉層級填滿程度的百分比。 *填滿因數*必須是介於 1 到 100 之間的整數值。 預設值是 0。  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 指定當插入作業嘗試將重複的索引鍵值插入唯一索引時所產生的錯誤回應。 IGNORE_DUP_KEY 選項只適用於在建立或重建索引之後所發生的插入作業。 預設值為 OFF。  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 指定是否要重新計算散發統計資料。 預設值為 OFF。  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 指定是否允許資料列鎖定。 預設值是 ON。  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 指定是否允許頁面鎖定。 預設值是 ON。  
  
## <a name="remarks"></a>備註  
 ALTER FUNCTION 不能用來將純量值函式變更為資料表值函式，反之亦然。 另外，ALTER FUNCTION 也不能用來將內嵌函數變更為多重陳述式函數，反之亦然。 ALTER FUNCTION 不能用來將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數變更為 CLR 函數，反之亦然。  
  
 下列 Service Broker 陳述式不能包含在定義[!INCLUDE[tsql](../../includes/tsql-md.md)]使用者定義函數：  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>Permissions  
 需要函數或結構描述的 ALTER 權限。 如果此函數指定使用者定義型別，則需要該型別的 EXECUTE 權限。  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [卸除函數 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
