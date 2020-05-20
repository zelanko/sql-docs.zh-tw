---
title: sp_describe_first_result_set （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2033ae81a030fa57e2f4aaf962e5dd35f9a9a318
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831178"
---
# <a name="sp_describe_first_result_set-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  傳回批次第一個可能結果集的中繼資料 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 如果批次沒有傳回任何結果，就會傳回空的結果集。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 無法判斷第一個查詢的中繼資料（藉由執行靜態分析來執行），就會引發錯誤。 動態管理檢視[sys.databases dm_exec_describe_first_result_set &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)會傳回相同的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>引數  
`[ \@tsql = ] 'Transact-SQL_batch'`一或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句。 *交易 SQL_batch*可以是**Nvarchar （***n***）** 或**Nvarchar （max）**。  
  
`[ \@params = ] N'parameters'`\@params 會提供批次參數的宣告字串 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，類似于 sp_executesql。 參數可以是**Nvarchar （n）** 或**Nvarchar （max）**。  
  
 這是一個字串，其中包含已內嵌在 _batch 中之所有參數的定義 [!INCLUDE[tsql](../../includes/tsql-md.md)] * *。 此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 *n*是指出其他參數定義的預留位置。 語句中指定的每個參數都必須在 \@ params 中定義。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句中的語句或批次不包含參數， \@ 則不需要 params。 這個參數的預設值是 NULL。  
  
`[ \@browse_information_mode = ] tinyint`指定是否傳回其他索引鍵資料行和來源資料表資訊。 如果設定為 1，就會分析每個查詢，如同查詢上包含 FOR BROWSE 選項一樣。 會傳回其他索引鍵資料行和來源資料表資訊。  
  
-   如果設為 0，則不會傳回資訊。  
  
-   如果設定為 1，就會分析每個查詢，如同查詢上包含 FOR BROWSE 選項一樣。 這會傳回基底資料表名稱做為來源資料行資訊。  
  
-   如果設定為 2，就會分析每個查詢，如同查詢用於準備或執行資料指標一樣。 這會傳回檢視表名稱做為來源資料行資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 **sp_describe_first_result_set**一律會在成功時傳回零的狀態。 如果程式擲回錯誤，並將程式稱為 RPC，則傳回狀態會填入 dm_exec_describe_first_result_set 的 error_type 資料行中所述的錯誤類型。 如果程序是從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 所呼叫，即使發生錯誤，傳回值也永遠是零。  
  
## <a name="result-sets"></a>結果集  
 這個通用的中繼資料會當做結果集來傳回，而結果中繼資料中的每個資料行都會有一個資料列。 每個資料列都會使用下一節所描述的格式來描述資料行的類型和 Null 屬性。 如果每個控制項路徑都沒有第一個陳述式，就會傳回具有零個資料列的結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**位 NOT Null**|指出資料行是為了用來瀏覽資訊而加入的額外資料行，且不會實際顯示在結果集中。|  
|**column_ordinal**|**int NOT NULL**|包含資料行在結果集中的序數位置。 第一個資料行的位置將會指定為1。|  
|**name**|**sysname Null**|如果可以判別名稱，則包含資料行名稱。 否則，它將會包含 NULL。|  
|**is_nullable**|**位 NOT Null**|如果資料行允許 NULL 則包含值 1，如果資料行不允許 NULL 則包含 0，此外，如果無法判別資料行是否允許 NULL，則為 1。|  
|**system_type_id**|**int NOT NULL**|包含 sys.databases 中所指定之資料行的資料類型 system_type_id。 針對 CLR 類型，即使 system_type_name 資料行將傳回 NULL，這個資料行將會傳回值 240。|  
|**system_type_name**|**Nvarchar （256） Null**|包含名稱和引數 (例如長度、有效位數、小數位數)，已指定給資料行的資料類型。 如果資料類型是使用者定義的別名類型，這裡就會指定基礎系統類型。 如果它是 CLR 使用者定義類型，這個資料行就會傳回 NULL。|  
|**max_length**|**Smallint NOT Null**|資料行的最大長度 (以位元組為單位)。<br /><br /> -1 = 資料行資料類型是**Varchar （max）**、 **Nvarchar （max）**、 **Varbinary （max）** 或**xml**。<br /><br /> 若為**文字**資料行， **max_length**值會是16，或**sp_tableoption ' text in row '** 所設定的值。|  
|**有效位數**|**Tinyint NOT Null**|如果以數值為基礎，就是資料行的有效位數。 否則傳回 0。|  
|**scale**|**Tinyint NOT Null**|如果是以數值為基礎，便是資料行的小數位數。 否則傳回 0。|  
|**collation_name**|**sysname Null**|如果是以字元為基礎，便是資料行的定序名稱。 否則，便傳回 NULL。|  
|**user_type_id**|**int NULL**|針對 CLR 和別名類型，會如同 sys.types 中所指定，包含資料行資料類型的 user_type_id。 否則，便為 NULL。|  
|**user_type_database**|**sysname Null**|針對 CLR 和別名類型，會包含定義類型之資料庫的名稱。 否則，便為 NULL。|  
|**user_type_schema**|**sysname Null**|針對 CLR 和別名類型，會包含定義類型之結構描述的名稱。 否則，便為 NULL。|  
|**user_type_name**|**sysname Null**|針對 CLR 和別名類型，會包含類型的名稱。 否則，便為 NULL。|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|針對 CLR 類型，會傳回定義類型之組件與類別的名稱。 否則，便為 NULL。|  
|**xml_collection_id**|**int NULL**|包含 sys.columns 中所指定資料行之資料類型的 xml_collection_id。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**xml_collection_database**|**sysname Null**|包含定義與這個類型相關聯之 XML 結構描述集合的資料庫。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**xml_collection_schema**|**sysname Null**|包含定義與這個類型相關聯之 XML 結構描述集合的結構描述。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**xml_collection_name**|**sysname Null**|包含與這個類型相關聯之 XML 結構描述集合的名稱。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**is_xml_document**|**位 NOT Null**|如果正要傳回的資料類型是 XML，而且該類型保證是完整 XML 文件 (包含根節點)，而不是 XML 片段，則傳回 1， 否則傳回 0。|  
|**is_case_sensitive**|**位 NOT Null**|如果資料行是區分大小寫的字串類型，則傳回 1；否則，便傳回 0。|  
|**is_fixed_length_clr_type**|**位 NOT Null**|如果資料行是固定長度的 CLR 類型，則傳回 1；否則，便傳回 0。|  
|**source_server**|**sysname**|在這個結果中的資料行所傳回的原始伺服器名稱 (如果它來自遠端伺服器)。 系統會提供名稱，因為它會出現在 sys.databases 中。 如果資料行來自本機伺服器，或是如果無法判別其原始伺服器，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_database**|**sysname**|這個結果中的資料行所傳回之原始資料庫名稱。 如果無法判別資料庫，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_schema**|**sysname**|這個結果中的資料行所傳回之原始結構描述名稱。 如果無法判別結構描述，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_table**|**sysname**|這個結果的資料行所傳回之原始資料表名稱。 如果無法判別資料表，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_column**|**sysname**|結果資料行所傳回之原始資料行名稱。 如果無法判別資料行，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**is_identity_column**|**位 Null**|如果資料行是識別欄位，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否為識別欄位，則傳回 NULL。|  
|**is_part_of_unique_key**|**位 Null**|如果資料行是唯一索引 (包括唯一和主要的條件約束) 的一部分，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否為唯一索引的一部分，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**is_updateable**|**位 Null**|如果資料行是可更新的，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否可更新，則傳回 NULL。|  
|**is_computed_column**|**位 Null**|如果資料行是計算資料行，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否為計算資料行，則傳回 NULL。|  
|**is_sparse_column_set**|**位 Null**|如果資料行是疏鬆資料行，則傳回 1，否則傳回 0。 如果它無法判別資料行是否為疏鬆資料行集的一部分，則傳回 NULL。|  
|**ordinal_in_order_by_list**|**Smallint Null**|這個資料行在 ORDER BY 清單中的位置。 如果資料行不會顯示在 ORDER BY 清單中，或如果無法唯一判別 ORDER BY 清單，則傳回 NULL。|  
|**order_by_list_length**|**Smallint Null**|ORDER BY 清單的長度。 如果沒有 ORDER BY 清單，或如果無法唯一判別 ORDER BY 清單，則傳回 NULL。 請注意，sp_describe_first_result_set 傳回的所有資料列的這個值都相同 **。**|  
|**order_by_is_descending**|**Smallint Null**|如果 ordinal_in_order_by_list 不是 NULL，**order_by_is_descending** 資料行會回報此資料行的 ORDER BY 子句方向。 否則，它會回報 NULL。|  
|**tds_type_id**|**int NOT NULL**|供內部使用。|  
|**tds_length**|**int NOT NULL**|供內部使用。|  
|**tds_collation_id**|**int NULL**|供內部使用。|  
|**tds_collation_sort_id**|**Tinyint Null**|供內部使用。|  
  
## <a name="remarks"></a>備註  
 **sp_describe_first_result_set**保證如果程式傳回（a 假設）批次 a 的第一個結果集中繼資料，而且後續執行該批次（a），則批次將會引發優化時間錯誤，（2）引發執行階段錯誤、（3）不傳回任何結果集，或（4）傳回具有**sp_describe_first_result_set**所描述之相同中繼資料的第一個結果集。  
  
 名稱、Null 屬性和資料類型可以不同。 如果**sp_describe_first_result_set**傳回空的結果集，保證批次執行將不會傳回任何結果集。  
  
 這保證會假設伺服器上沒有相關的架構變更。 伺服器上的相關架構變更不包括在呼叫**sp_describe_first_result_set**的時間，以及在執行期間傳回結果集的時間（包括批次 B 所做的架構變更），在批次中建立臨時表或資料表變數。  
  
 **sp_describe_first_result_set**在下列任何情況下都會傳回錯誤。  
  
-   如果輸入 \@ tsql 不是有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次。 有效性是藉由剖析和分析 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次來判斷。 判斷批次是否有效時，批次在查詢優化期間或執行期間所造成的任何錯誤都不會列入考慮 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
-   如果 \@ params 不是 Null，而且包含的字串不是語法有效的參數宣告字串，或包含的字串會宣告任何參數一次以上，則為。  
  
-   如果輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次宣告的區域變數與 params 中宣告的參數名稱相同 \@ 。  
  
-   如果陳述式使用暫存資料表。  
  
-   查詢包含建立隨後要查詢的永久資料表。  
  
 如果其他所有檢查已成功，就會將輸入批次內所有可能的控制流程路徑列入考量。 這會將所有控制流程語句納入考慮（GOTO、IF/ELSE、WHILE 和 [!INCLUDE[tsql](../../includes/tsql-md.md)] TRY/CATCH 區塊） [!INCLUDE[tsql](../../includes/tsql-md.md)] ，以及由 EXEC 語句從輸入批次叫用的任何程式、動態批次或觸發程式、導致 ddl 觸發程式引發的 ddl 語句，或是導致在目標資料表上引發觸發程式的 DML 語句，或因為外鍵條件約束的串聯動作而修改的資料表。 在具有許多可能的控制路徑之情況下，有時候，演算將會停止。  
  
 針對每個控制流程路徑，傳回結果集的第一個語句（如果有的話）取決於**sp_describe_first_result_set**。  
  
 在單一批次中找到多個可能的第一個陳述式時，其結果可能會在資料行數目、資料行名稱、Null 屬性和資料類型等方面有所不同。 這裡將會詳細說明這些差異的處理方式：  
  
-   如果資料行數目不同，就會擲回錯誤，且不會傳回任何結果。  
  
-   如果資料行名稱不同，傳回的資料行名稱就會設定為 NULL。  
  
-   如果 Null 屬性不同，傳回的 Null 屬性將會允許 NULL。  
  
-   如果資料類型不同，將會擲回錯誤，且不會傳回任何結果，除非遇到下列情況：  
  
    -   **Varchar （a）** 到**Varchar （a '）** ，其中 ' >。  
  
    -   **Varchar （a）** 至**Varchar （max）**  
  
    -   Nvarchar **（a）** 到**Nvarchar （a '）** ，其中 ' >。  
  
    -   Nvarchar **（a）** 到**Nvarchar （max）**  
  
    -   **Varbinary （a）** 至**Varbinary （a '）** ，其中 ' >。  
  
    -   Varbinary **（a）** 到**Varbinary （max）**  
  
 **sp_describe_first_result_set**不支援間接遞迴。  
  
## <a name="permissions"></a>權限  
 需要執行 \@ tsql 引數的許可權。  
  
## <a name="examples"></a>範例  
  
### <a name="typical-examples"></a>一般範例  
  
#### <a name="a-simple-example"></a>A. 簡單範例  
 下列範例描述從單一查詢傳回的結果集。  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 下列範例會顯示從包含參數之單一查詢傳回的結果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>B. 瀏覽模式範例  
 下列三個範例說明不同瀏覽資訊模式之間的主要差異。 只有相關的資料行包含在查詢結果中。  
  
 下列範例使用 0，表示未傳回任何資訊。  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 下列範例使用 1，表示它傳回資訊，就如同在查詢中包含 FOR BROWSE 選項一樣。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 下列範例使用 2，表示已分析，就如同準備資料指標一樣。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|name|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>問題範例  
 下列範例會針對所有範例使用兩個資料表。 請執行下列陳述式以建立範例資料表。  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>因為資料行數目不同而發生錯誤  
 在這個範例中，第一個可能的結果集中之資料行數目不同。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>因為資料類型不同而發生錯誤  
 不同的第一個可能的結果集中之資料行類型不同。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 結果：錯誤，類型不相符（**int**與**Smallint**）。  
  
#### <a name="column-name-cannot-be-determined"></a>無法判別資料行名稱  
 在第一個可能的結果集中，在相同的變數長度類型、Null 屬性與資料行名稱等情況下，資料行的長度不同：  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 結果： \< 未知的資料行名稱> **Varchar （20） Null**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>透過別名強制資料行名稱必須相同  
 與先前相同，但是資料行透過資料行別名而具有相同名稱。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 結果： b **Varchar （20） Null**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>因為無法比對資料行類型而發生錯誤  
 在不同的第一個可能的結果集中，資料行類型彼此不同。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 結果：錯誤，類型不相符（**Varchar （10）** 與**Nvarchar （10）**）。  
  
#### <a name="result-set-can-return-an-error"></a>結果集可以傳回錯誤  
 第一個結果集為錯誤或結果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 結果： **intNull**  
  
#### <a name="some-code-paths-return-no-results"></a>部分程式碼路徑沒有傳回任何結果  
 第一個結果集為 Null 或結果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 結果： **intNull**  
  
#### <a name="result-from-dynamic-sql"></a>來自動態 SQL 的結果  
 第一個結果集為可探索的動態 SQL，因為本身屬於文字字串。  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 結果： **INT Null**  
  
#### <a name="result-failure-from-dynamic-sql"></a>來自動態 SQL 的失敗結果  
 第一個結果集因為動態 SQL 而未定義。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 結果：錯誤。 因為可探索的動態 SQL，導致結果不是可探索的。  
  
#### <a name="result-set-specified-by-user"></a>由使用者指定的結果集  
 第一個結果集是由使用者手動指定的。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 結果： Column1 **BIGINT NOT Null**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>因位結果集模稜兩可而發生錯誤  
 這個範例假設名為 user1 的另一個使用者在預設的架構 s1 中，有一個名為 t1 的資料表，其中包含資料行（ **INT NOT Null**）。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 結果：錯誤。 t1 可以是 dbo 或 s1，每個都有不同的資料行數目。  
  
#### <a name="result-even-with-ambiguous-result-set"></a>即使結果集模稜兩可的結果  
 使用與先前範例相同的假設。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 結果： **INT Null** ，因為 dbo 和 s1. a 都具有類型**int**和不同的 null 屬性。  
  
## <a name="see-also"></a>另請參閱  
 [sp_describe_undeclared_parameters &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [dm_exec_describe_first_result_set &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [dm_exec_describe_first_result_set_for_object &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
