---
title: sp_describe_undeclared_parameters & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 07/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_undeclared_parameters
- sp_describe_undeclared_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_undeclared_parameters
ms.assetid: 6f016da6-dfee-4228-8b0d-7cd8e7d5a354
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e4a4a97b4a69aaf68d196833ee56b089a3dadfcf
ms.sourcegitcommit: 046d29e700981594725af698a5e079922cf5dbe7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2018
ms.locfileid: "39331584"
---
# <a name="spdescribeundeclaredparameters-transact-sql"></a>sp_describe_undeclared_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  傳回結果集，其中包含未宣告的參數中的相關中繼資料[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 會考量用於每個參數 **\@tsql**批次，但未在宣告 **\@params**。 傳回的結果集中，針對每一個這類參數包含一個資料列，內含該參數的推算類型資訊。 此程序會傳回空的結果集，如果 **\@tsql**輸入批次沒有任何參數，除了中所宣告 **\@params**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  
  
## <a name="arguments"></a>引數  
 [  **\@tsql =** ] **'***Transact SQL_batch***'**  
 一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 *Transact SQL_batch*可能**nvarchar (***n***)** 或是**nvarchar （max)**。  
  
 [  **\@params =** ] **N'***參數***'**  
 \@params 參數提供的宣告字串[!INCLUDE[tsql](../../includes/tsql-md.md)]批次，同樣地方式 sp_executesql 運作方式。 *參數*可能**nvarchar (***n***)** 或是**nvarchar （max)**。  
  
 是一個字串，其中包含已內嵌在的所有參數的定義*Transact SQL_batch*。 此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 n 是指出其他參數定義的預留位置。 如果 TRANSACT-SQL 陳述式或批次陳述式中的不包含參數， \@params 並非必要。 這個參數的預設值是 NULL。  
  
 資料類型  
 參數的資料類型。  
  
## <a name="return-code-values"></a>傳回碼值  
 **sp_describe_undeclared_parameters**永遠會傳回狀態零成功。 如果此程序擲回錯誤，而且程序被當做 RPC 來呼叫，傳回的狀態會填入的錯誤類型 sys.dm_exec_describe_first_result_set 之 error_type 資料行中所述。 如果程序是從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 所呼叫，即使發生錯誤，傳回值也永遠是零。  
  
## <a name="result-sets"></a>結果集  
 **sp_describe_undeclared_parameters**會傳回下列結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int NOT NULL**|包含結果集中的參數序數位置。 第一個參數的位置將會指定為 1。|  
|**name**|**sysname NOT NULL**|包含參數的名稱。|  
|**suggested_system_type_id**|**int NOT NULL**|包含**system_type_id** sys.types 中所指定為參數的資料類型。<br /><br /> 針對 CLR 類型，即使**system_type_name**資料行將傳回 NULL，這個資料行將傳回值 240。|  
|**suggested_system_type_name**|**nvarchar (256) NULL**|包含資料類型名稱。 包含指定給參數之資料類型的引數 (例如長度、有效位數、小數位數)。 如果資料類型是使用者定義的別名類型，這裡就會指定基礎系統類型。 如果它是 CLR 使用者定義資料類型，這個資料行就會傳回 NULL。 如果無法推算參數的類型，則傳回 NULL。|  
|**suggested_max_length**|**smallint 非 NULL**|請參閱 sys.columns。 針對**max_length**資料行描述。|  
|**suggested_precision**|**tinyint NOT NULL**|請參閱 sys.columns。 以查看 precision 資料行的說明。|  
|**suggested_scale**|**tinyint NOT NULL**|請參閱 sys.columns。 以查看 scale 資料行的說明。|  
|**suggested_user_type_id**|**int NULL**|針對 CLR 和別名類型，會如同 sys.types 中所指定，包含資料行資料類型的 user_type_id。 否則，便為 NULL。|  
|**suggested_user_type_database**|**sysname 為 NULL**|針對 CLR 和別名類型，會包含定義類型之資料庫的名稱。 否則，便為 NULL。|  
|**suggested_user_type_schema**|**sysname 為 NULL**|針對 CLR 和別名類型，會包含定義類型之結構描述的名稱。 否則，便為 NULL。|  
|**suggested_user_type_name**|**sysname 為 NULL**|針對 CLR 和別名類型，會包含類型的名稱。 否則，便為 NULL。|  
|**suggested_assembly_qualified_type_name**|**nvarchar (4000) NULL**|針對 CLR 類型，會傳回定義類型之組件與類別的名稱。 否則，便為 NULL。|  
|**suggested_xml_collection_id**|**int NULL**|包含 sys.columns 中所指定參數的資料類型的 xml_collection_id。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**suggested_xml_collection_database**|**sysname 為 NULL**|包含定義與這個類型相關聯之 XML 結構描述集合的資料庫。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**suggested_xml_collection_schema**|**sysname 為 NULL**|包含定義與這個類型相關聯之 XML 結構描述集合的結構描述。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**suggested_xml_collection_name**|**sysname 為 NULL**|包含與這個類型相關聯之 XML 結構描述集合的名稱。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**suggested_is_xml_document**|**位元 NOT NULL**|如果正要傳回的類型是 XML，而且該類型保證是 XML 文件，則傳回 1。 否則傳回 0。|  
|**suggested_is_case_sensitive**|**位元 NOT NULL**|如果資料行是區分大小寫的字串類型，則傳回 1，否則傳回 0。|  
|**suggested_is_fixed_length_clr_type**|**位元 NOT NULL**|如果資料行是固定長度的 CLR 類型，則傳回 1，否則傳回 0。|  
|**suggested_is_input**|**位元 NOT NULL**|如果參數用於指派左邊以外的任何地方，則傳回 1。 否則傳回 0。|  
|**suggested_is_output**|**位元 NOT NULL**|如果參數用在指派的左邊，或傳遞至預存程序的輸出參數，則傳回 1。 否則傳回 0。|  
|**formal_parameter_name**|**sysname 為 NULL**|如果參數是預存程序或使用者定義函數的引數，則傳回對應型式參數的名稱。 否則，便傳回 NULL。|  
|**suggested_tds_type_id**|**int NOT NULL**|供內部使用。|  
|**suggested_tds_length**|**int NOT NULL**|供內部使用。|  
  
## <a name="remarks"></a>備註  
 **sp_describe_undeclared_parameters**永遠會傳回狀態零。  
  
 最常見的用法是在應用程式中提供可能包含參數且必須以特定方式處理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 舉例來說，使用者介面 （例如 ODBCTest 或 RowsetViewer），其中使用者會提供使用 ODBC 參數語法的查詢。 應用程式必須動態探索參數數目，並提示使用者提供每個參數值。  
  
 另一個例子是，當沒有使用者輸入的情況下，應用程式必須在參數上執行迴圈，並從其他位置 (例如資料表) 為它們取得資料。 在這種情況下，應用程式不必一次傳遞所有參數資訊。 相反地，應用程式可以從提供者取得所有參數資訊，並自行從資料表取得資料。 使用程式碼**sp_describe_undeclared_parameters**更泛用且較不需要修改，如果資料結構稍後變更。  
  
 **sp_describe_undeclared_parameters**任何下列的情況下會傳回錯誤。  
  
-   如果輸入\@tsql 不是有效[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 有效性取決於的剖析和分析[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 決定時，不會考慮任何批次在查詢最佳化期間，或在執行期間造成的錯誤是否[!INCLUDE[tsql](../../includes/tsql-md.md)]批次是否有效。  
  
-   如果\@參數不是 NULL，並且包含字串不是句法有效的參數宣告字串，或如果它包含的字串，宣告任何參數一次以上。  
  
-   如果輸入[!INCLUDE[tsql](../../includes/tsql-md.md)]批次中宣告的參數，宣告相同名稱的本機變數\@params。  
  
-   如果陳述式建立暫存資料表。  
  
 如果\@tsql 沒有任何參數，除了中所宣告\@params 中，程序會傳回空的結果集。  
  
## <a name="parameter-selection-algorithm"></a>參數選取演算法  
 針對具有未宣告之參數的查詢，在三個步驟中進行未宣告之參數的資料類型推算。  
  
 **步驟 1**  
  
 針對具有未宣告之參數的查詢，資料類型推算的第一步是找出資料類型不相依於未宣告的參數之所有子運算式的資料類型。 可判斷下列運算式的類型：  
  
-   資料行、常數、變數和宣告的參數。  
  
-   使用者定義函數 (UDF) 呼叫的結果。  
  
-   資料類型不相依於所有輸入中未宣告的參數之運算式。  
  
 例如，請考量 `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2` 查詢。 運算式 dbo.tbl (\@p1) + c1 和 c2 具有資料類型和運算式\@p1 和\@p2 + 2 則否。  
  
 在此步驟之後，如果任何運算式 (UDF 呼叫以外) 有兩個不含資料類型的引數，類型推算會失敗並出現錯誤。 例如，下列範例都會產生錯誤：  
  
```sql
SELECT * FROM t1 WHERE @p1 = @p2  
SELECT * FROM t1 WHERE c1 = @p1 + @p2  
SELECT * FROM t1 WHERE @p1 = SUBSTRING(@p2, 2, 3)  
```  
  
 下列範例不會產生錯誤：  
  
```sql
SELECT * FROM t1 WHERE @p1 = dbo.tbl(c1, @p2, @p3)  
```
  
 **步驟 2**  
  
 指定未宣告的參數\@p，類型推算演算法會尋找最內側運算式 E (\@p)，其中包含\@p 和是下列其中之一：  
  
-   比較或指派運算子的引數。  
  
-   使用者定義函數 (包括資料表值 UDF)、程序或方法的引數。  
  
-   引數**值**子句**插入**陳述式。  
  
-   引數**CAST**或是**轉換**。  
  
 類型推算演算法會尋找的目標資料類型 TT (\@p) e (\@p)。 上述範例的目標資料類型如下所示：  
  
-   比較或指派另一端的資料類型。  
  
-   傳遞此引數之目標參數的已宣告資料類型。  
  
-   插入此值之資料行的資料類型。  
  
-   陳述式轉型或轉換成的資料類型。  
  
 例如，請考量 `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)` 查詢。 然後 E (\@p1) = \@p1，E (\@p2) = \@p2 + c1，TT (\@p1) 是 dbo.tbl 和 TT 的宣告傳回資料類型 (\@p2) 是 dbo.tbl 的已宣告的參數資料類型。  
  
 如果\@p 未包含在任何運算式中所列開頭的步驟 2，類型推算演算法會判斷該 E (\@p) 是最大的純量運算式，包含\@p，類型推算演算法並不會計算的目標資料類型 TT (\@p) e (\@p)。 例如，如果查詢是 SELECT`@p + 2`然後 E (\@p) = \@p + 2，且沒有 TT (\@p)。  
  
 **步驟 3**  
  
 現在該 E (\@p) 和 TT (\@p) 會識別，類型推算演算法會推算的資料類型\@p 在下列兩種方式之一：  
  
-   簡單推算  
  
     如果 E (\@p) = \@p 和 TT (\@p) 存在，亦即，如果\@p 是直接在步驟 2 的開頭所列的其中一個運算式的引數，類型推算演算法會推算的資料型別\@設為 TT （p\@p)。 例如：  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     資料型別\@p1 \@p2 和\@p3 會是 c1、 dbo.tbl 的傳回資料類型的資料型別和參數資料類型 dbo.tbl 分別。  
  
     為特殊情況下，如果\@p 是的引數\<，>， \<= 或 > = 運算子，簡單推算規則不會套用。 類型推算演算法會使用下一節所述的一般推算規則。 例如，如果 c1 是資料類型 char(30) 的資料行，請考慮下列兩個查詢：  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     在第一個案例中，類型推算演算法會推算**char(30)** 的資料型別為\@p 根據稍早在本主題中的規則。 在第二個案例中，類型推算演算法會推算**varchar （8000)** 根據下一節中的一般推算規則。  
  
-   一般推算  
  
     如果不適用簡單推算，針對未宣告的參數，下列資料類型會列入考量：  
  
    -   整數資料類型 (**位元**， **tinyint**， **smallint**， **int**， **bigint**)  
  
    -   Money 資料類型 (**smallmoney**， **money**)  
  
    -   浮點資料類型 (**浮點數**，**實際**)  
  
    -   **數值 （38，19）** -不考慮其他數值或十進位資料類型。  
  
    -   **varchar （8000)**， **varchar （max)**， **nvarchar(4000)**，和**nvarchar （max)** -其他字串資料類型 (例如**文字**， **char(8000)**， **nvarchar(30)** 等等) 不會考慮。  
  
    -   **varbinary(8000)** 並**varbinary （max)** -不考慮其他二進位資料類型 (例如**映像**， **binary(8000)**， **varbinary(30)**，依此類推。)。  
  
    -   **日期**， **time(7)**， **smalldatetime**， **datetime**， **datetime2(7)**， **datetimeoffset(7)** -其他日期和時間類型，例如**time(4)**，不會考慮。  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   CLR 系統定義的型別 (**hierarchyid**， **geometry**， **geography**)  
  
    -   CLR 使用者定義型別  
  
### <a name="selection-criteria"></a>選取準則  
 在候選資料類型中，會導致查詢失效的任何資料類型都會遭到拒絕。 在剩餘的候選資料類型中，類型推算演算法會根據下列規則來選取其中一個資料類型。  
  
1.  會產生隱含轉換在 E 最小數目的資料類型 (\@p) 已選取。 如果特定的資料類型會產生的資料類型 e (\@p) 不同於 TT (\@p)，類型推算演算法會認為這是從 E 的資料類型的額外隱含轉換 (\@p) 到 TT (\@p)。  
  
     例如：  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     在此案例中，E (\@p) 是 Col_Int + \@p 和 TT (\@p) 會**int**。**int**為選擇\@p 因為它會不產生任何隱含的轉換。 任何其他資料類型選擇會產生至少一個隱含轉換。  
  
2.  如果多個資料類型有相同的最小轉換數目，則會使用具有較高優先順序的資料類型。 例如：  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     在此情況下， **int**並**smallint**產生一個轉換。 所有其他的資料類型都會產生一個以上的轉換。 因為**int**優先於**smallint**， **int**用於\@p。 如需有關資料類型優先順序的詳細資訊，請參閱 <<c0> [ 資料類型優先順序&#40;TRANSACT-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md)。</c0>  
  
     只有在依據規則 1 每個候選資格相同的資料類型與具有最高優先順序的資料類型之間發生隱含轉換時，才會套用此規則。 如果沒有隱含轉換，資料類型推算會失敗並出現錯誤。 例如在查詢`SELECT @p FROM t`，資料類型推算會失敗，因為任何資料類型\@p 是一樣好。 比方說，沒有任何隱含的轉換，從**int**要**xml**。  
  
3.  如果兩個類似的資料類型將依據規則 1，例如**varchar （8000)** 並**varchar （max)** 較小資料類型 (**varchar （8000)**) 選擇。 相同原則適用於**nvarchar**並**varbinary**資料型別。  
  
4.  為執行規則 1，類型推算演算法會偏好特定轉換。 從最佳到最差的轉換順序如下：  
  
    1.  不同長度的同一個基本資料類型之間的轉換。  
  
    2.  固定長度和可變長度版本相同的資料類型之間的轉換 (例如**char**要**varchar**)。  
  
    3.  之間的轉換**NULL**並**int**。  
  
    4.  任何其他轉換。  
  
 例如，對於查詢`SELECT * FROM t WHERE [Col_varchar(30)] > @p`， **varchar （8000)** 因為轉換 (a) 是最佳選擇。 查詢`SELECT * FROM t WHERE [Col_char(30)] > @p`， **varchar （8000)** 仍會選擇，因為它會導致類型 (b) 轉換，而且另一個選擇 (例如**varchar(4000)**) 會導致類型 (d) 轉換。  
  
 最後一個範例中，指定查詢`SELECT NULL + @p`， **int**為選擇\@p 因為它會導致類型 (c) 轉換。  
  
## <a name="permissions"></a>[權限]  
 需要權限來執行\@tsql 引數。  
  
## <a name="examples"></a>範例  
 下列範例會傳回未宣告之 `@id` 和 `@name` 參數的預期資料類型相關資訊。  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR name = @name'  
  
```  
  
 當提供 `@id` 參數做為 `@params` 參考時，結果集中會省略 `@id` 參數，而只描述 `@name` 參數。  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR NAME = @name',  
@params = N'@id int'  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_describe_first_result_set &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)