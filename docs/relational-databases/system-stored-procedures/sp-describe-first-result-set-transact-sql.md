---
title: sp_describe_first_result_set & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d0e6452ce0b49b20cb4ec75b2a5a21e7c0400000
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536408"
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  第一個可能結果集傳回的中繼資料[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 如果批次沒有傳回任何結果，就會傳回空的結果集。 如果引發錯誤[!INCLUDE[ssDE](../../includes/ssde-md.md)]無法判別將透過執行靜態分析來執行的第一個查詢的中繼資料。 動態管理檢視[sys.dm_exec_describe_first_result_set &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)傳回的相同資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>引數  
 [  **\@tsql =** ] **'***Transact SQL_batch***'**  
 一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 *Transact SQL_batch*可能**nvarchar (***n***)** 或是**nvarchar （max)**。  
  
 [  **\@params =** ] **N'***參數***'**  
 \@params 參數提供的宣告字串[!INCLUDE[tsql](../../includes/tsql-md.md)]批次，也就是類似於 sp_executesql。 參數可能**nvarchar （n)** 或是**nvarchar （max)**。  
  
 是一個字串，其中包含已內嵌在的所有參數的定義[!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch&lt*。 此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 *n*是指出其他參數定義的預留位置。 陳述式中指定的每個參數必須定義在\@params。 如果[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或陳述式中的批次不包含參數， \@params 並非必要。 這個參數的預設值是 NULL。  
  
 [  **\@browse_information_mode =** ] *tinyint*  
 指定是否會傳回其他索引鍵資料行和來源資料表資訊。 如果設定為 1，就會分析每個查詢，如同查詢上包含 FOR BROWSE 選項一樣。 會傳回其他索引鍵資料行和來源資料表資訊。  
  
-   如果設為 0，則不會傳回資訊。  
  
-   如果設定為 1，就會分析每個查詢，如同查詢上包含 FOR BROWSE 選項一樣。 這會傳回基底資料表名稱做為來源資料行資訊。  
  
-   如果設定為 2，就會分析每個查詢，如同查詢用於準備或執行資料指標一樣。 這會傳回檢視表名稱做為來源資料行資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 **sp_describe_first_result_set**一律會傳回狀態零成功。 如果此程序擲回錯誤，而且程序被當做 RPC 來呼叫，傳回的狀態會填入 sys.dm_exec_describe_first_result_set 之 error_type 資料行中所述的錯誤類型。 如果程序是從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 所呼叫，即使發生錯誤，傳回值也永遠是零。  
  
## <a name="result-sets"></a>結果集  
 這個通用的中繼資料會當做結果集來傳回，而結果中繼資料中的每個資料行都會有一個資料列。 每個資料列都會使用下一節所描述的格式來描述資料行的類型和 Null 屬性。 如果每個控制項路徑都沒有第一個陳述式，就會傳回具有零個資料列的結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**位元 NOT NULL**|指出資料行是為了用來瀏覽資訊而加入的額外資料行，且不會實際顯示在結果集中。|  
|**column_ordinal**|**int NOT NULL**|包含資料行在結果集中的序數位置。 第一個資料行的位置將會指定為 1。|  
|**name**|**sysname 為 NULL**|如果可以判別名稱，則包含資料行名稱。 否則，它將會包含 NULL。|  
|**is_nullable**|**位元 NOT NULL**|如果資料行允許 NULL 則包含值 1，如果資料行不允許 NULL 則包含 0，此外，如果無法判別資料行是否允許 NULL，則為 1。|  
|**system_type_id**|**int NOT NULL**|包含 sys.types 中所指定的資料行的資料類型的 system_type_id。 針對 CLR 類型，即使 system_type_name 資料行將傳回 NULL，這個資料行將會傳回值 240。|  
|**system_type_name**|**nvarchar(256) NULL**|包含名稱和引數 (例如長度、有效位數、小數位數)，已指定給資料行的資料類型。 如果資料類型是使用者定義的別名類型，這裡就會指定基礎系統類型。 如果它是 CLR 使用者定義類型，這個資料行就會傳回 NULL。|  
|**max_length**|**smallint 非 NULL**|資料行的最大長度 (以位元組為單位)。<br /><br /> -1 = 資料行資料類型是**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，或**xml**。<br /><br /> 針對**文字**資料行**max_length**值會是 16，或是所設定的值**sp_tableoption 'text in row'**。|  
|**有效位數**|**tinyint NOT NULL**|如果以數值為基礎，就是資料行的有效位數。 否則傳回 0。|  
|**scale**|**tinyint NOT NULL**|如果是以數值為基礎，便是資料行的小數位數。 否則傳回 0。|  
|**collation_name**|**sysname 為 NULL**|如果是以字元為基礎，便是資料行的定序名稱。 否則，便傳回 NULL。|  
|**user_type_id**|**int NULL**|針對 CLR 和別名類型，會如同 sys.types 中所指定，包含資料行資料類型的 user_type_id。 否則，便為 NULL。|  
|**user_type_database**|**sysname 為 NULL**|針對 CLR 和別名類型，會包含定義類型之資料庫的名稱。 否則，便為 NULL。|  
|**user_type_schema**|**sysname 為 NULL**|針對 CLR 和別名類型，會包含定義類型之結構描述的名稱。 否則，便為 NULL。|  
|**user_type_name**|**sysname 為 NULL**|針對 CLR 和別名類型，會包含類型的名稱。 否則，便為 NULL。|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|針對 CLR 類型，會傳回定義類型之組件與類別的名稱。 否則，便為 NULL。|  
|**xml_collection_id**|**int NULL**|包含 sys.columns 中所指定資料行之資料類型的 xml_collection_id。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**xml_collection_database**|**sysname 為 NULL**|包含定義與這個類型相關聯之 XML 結構描述集合的資料庫。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**xml_collection_schema**|**sysname 為 NULL**|包含定義與這個類型相關聯之 XML 結構描述集合的結構描述。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**xml_collection_name**|**sysname 為 NULL**|包含與這個類型相關聯之 XML 結構描述集合的名稱。 如果傳回的類型沒有與 XML 結構描述集合相關聯，這個資料行將傳回 NULL。|  
|**is_xml_document**|**位元 NOT NULL**|如果正要傳回的資料類型是 XML，而且該類型保證是完整 XML 文件 (包含根節點)，而不是 XML 片段，則傳回 1， 否則傳回 0。|  
|**is_case_sensitive**|**位元 NOT NULL**|如果資料行是區分大小寫的字串類型，則傳回 1；否則，便傳回 0。|  
|**is_fixed_length_clr_type**|**位元 NOT NULL**|如果資料行是固定長度的 CLR 類型，則傳回 1；否則，便傳回 0。|  
|**source_server**|**sysname**|在這個結果中的資料行所傳回的原始伺服器名稱 (如果它來自遠端伺服器)。 給定的名稱會出現在 sys.servers 中。 如果資料行來自本機伺服器，或是如果無法判別其原始伺服器，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_database**|**sysname**|這個結果中的資料行所傳回之原始資料庫名稱。 如果無法判別資料庫，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_schema**|**sysname**|這個結果中的資料行所傳回之原始結構描述名稱。 如果無法判別結構描述，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_table**|**sysname**|這個結果的資料行所傳回之原始資料表名稱。 如果無法判別資料表，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**source_column**|**sysname**|結果資料行所傳回之原始資料行名稱。 如果無法判別資料行，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**is_identity_column**|**位元 NULL**|如果資料行是識別欄位，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否為識別欄位，則傳回 NULL。|  
|**is_part_of_unique_key**|**位元 NULL**|如果資料行是唯一索引 (包括唯一和主要的條件約束) 的一部分，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否為唯一索引的一部分，則傳回 NULL。 只會在要求瀏覽資訊時填入。|  
|**is_updateable**|**位元 NULL**|如果資料行是可更新的，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否可更新，則傳回 NULL。|  
|**is_computed_column**|**位元 NULL**|如果資料行是計算資料行，則傳回 1；如果不是，則傳回 0。 如果它無法判別資料行是否為計算資料行，則傳回 NULL。|  
|**is_sparse_column_set**|**位元 NULL**|如果資料行是疏鬆資料行，則傳回 1，否則傳回 0。 如果它無法判別資料行是否為疏鬆資料行集的一部分，則傳回 NULL。|  
|**ordinal_in_order_by_list**|**smallint NULL**|這個資料行在 ORDER BY 清單中的位置。 如果資料行不會顯示在 ORDER BY 清單中，或如果無法唯一判別 ORDER BY 清單，則傳回 NULL。|  
|**order_by_list_length**|**smallint NULL**|ORDER BY 清單的長度。 如果沒有 ORDER BY 清單，或如果無法唯一判別 ORDER BY 清單，則傳回 NULL。 請注意，這個值會是所傳回的所有資料列相同**sp_describe_first_result_set。**|  
|**order_by_is_descending**|**smallint NULL**|如果 ordinal_in_order_by_list 不是 NULL， **order_by_is_descending**資料行則報告此資料行的 ORDER BY 子句方向。 否則，它會回報 NULL。|  
|**tds_type_id**|**int NOT NULL**|供內部使用。|  
|**tds_length**|**int NOT NULL**|供內部使用。|  
|**tds_collation_id**|**int NULL**|供內部使用。|  
|**tds_collation_sort_id**|**tinyint NULL**|供內部使用。|  
  
## <a name="remarks"></a>備註  
 **sp_describe_first_result_set** ，如果此程序傳回的第一個結果集 （假設） 中繼資料批次 A 並且如果該批次 （A） 之後執行然後批次的保證會 (1) 引發最佳化時間錯誤，(2)會引發執行階段錯誤，(3) 會傳回任何結果集，或 (4) 傳回第一個結果集，使用相同的中繼資料所描述**sp_describe_first_result_set**。  
  
 名稱、Null 屬性和資料類型可以不同。 如果**sp_describe_first_result_set**傳回空的結果集，就可以保證批次執行會傳回任何結果集。  
  
 這項保證會假設伺服器上沒有任何相關的結構描述變更。 在伺服器上的相關結構描述變更不包括建立暫存資料表或資料表之間的時間於批次 A 中的變數， **sp_describe_first_result_set**稱為和期間傳回的結果集的時間執行，包括由批次 b 進行的結構描述變更  
  
 **sp_describe_first_result_set**任何下列的情況下會傳回錯誤。  
  
-   如果輸入\@tsql 不是有效[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 有效性取決於的剖析和分析[!INCLUDE[tsql](../../includes/tsql-md.md)]批次。 決定時，不會考慮任何批次在查詢最佳化期間，或在執行期間造成的錯誤是否[!INCLUDE[tsql](../../includes/tsql-md.md)]批次是否有效。  
  
-   如果\@參數不是 NULL，並且包含字串不是句法有效的參數宣告字串，或如果它包含的字串，宣告任何參數一次以上。  
  
-   如果輸入[!INCLUDE[tsql](../../includes/tsql-md.md)]批次中宣告的參數，宣告相同名稱的本機變數\@params。  
  
-   如果陳述式使用暫存資料表。  
  
-   查詢包含建立隨後要查詢的永久資料表。  
  
 如果其他所有檢查已成功，就會將輸入批次內所有可能的控制流程路徑列入考量。 此採用考慮到所有的控制流程陳述式 (GOTO、 IF/ELSE、 WHILE 及[!INCLUDE[tsql](../../includes/tsql-md.md)]TRY/CATCH 區塊) 以及任何程序，動態[!INCLUDE[tsql](../../includes/tsql-md.md)]批次或從輸入批次叫用 EXEC 陳述式時，DDL 陳述式而引發的觸發程序要引發的 DDL 觸發程序或 DML 陳述式會造成要引發的觸發程序，因為上的外部索引鍵條件約束的串聯式動作而遭到修改的資料表或目標資料表上。 在具有許多可能的控制路徑之情況下，有時候，演算將會停止。  
  
 針對每個控制流程路徑中，第一個陳述式 （如果有的話），傳回結果集由**sp_describe_first_result_set**。  
  
 在單一批次中找到多個可能的第一個陳述式時，其結果可能會在資料行數目、資料行名稱、Null 屬性和資料類型等方面有所不同。 這裡將會詳細說明這些差異的處理方式：  
  
-   如果資料行數目不同，就會擲回錯誤，且不會傳回任何結果。  
  
-   如果資料行名稱不同，傳回的資料行名稱就會設定為 NULL。  
  
-   如果 Null 屬性不同，傳回的 Null 屬性將會允許 NULL。  
  
-   如果資料類型不同，將會擲回錯誤，且不會傳回任何結果，除非遇到下列情況：  
  
    -   **varchar(a)** 要**varchar(a')** 其中 ' >。  
  
    -   **varchar(a)** 至**varchar （max)**  
  
    -   **nvarchar(a)** 要**nvarchar(a')** 其中 ' >。  
  
    -   **nvarchar(a)** 至**nvarchar （max)**  
  
    -   **varbinary(a)** 要**varbinary(a')** 其中 ' >。  
  
    -   **varbinary(a)** 至**varbinary （max)**  
  
 **sp_describe_first_result_set**不支援間接遞迴。  
  
## <a name="permissions"></a>Permissions  
 需要權限來執行\@tsql 引數。  
  
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
  
|is_hidden|column_ordinal|NAME|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 下列範例使用 1，表示它傳回資訊，就如同在查詢中包含 FOR BROWSE 選項一樣。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|NAME|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 下列範例使用 2，表示已分析，就如同準備資料指標一樣。  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|NAME|source_schema|source_table|source_column|is_part_of_unique_key|  
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
  
 結果： 錯誤，類型不相符 (**int**與**smallint**)。  
  
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
  
 結果：\<未知的資料行名稱 > **varchar （20) NULL**  
  
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
  
 結果： b **varchar (20) NULL**  
  
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
  
 結果： 錯誤，類型不相符 (**varchar(10)** 與**nvarchar(10**)。  
  
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
  
 結果： **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>部分程式碼路徑沒有傳回任何結果  
 第一個結果集為 Null 或結果集。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 結果： **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>來自動態 SQL 的結果  
 第一個結果集為可探索的動態 SQL，因為本身屬於文字字串。  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 結果： **INT NULL**  
  
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
  
 結果： Column1 **bigint NOT NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>因位結果集模稜兩可而發生錯誤  
 此範例假設名為 user1 的另一位使用者具有資料行的預設結構描述 s1 中名為 t1 的資料表 ( **int NOT NULL**)。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 結果：錯誤。 dbo.t1 或 s1.t1，各自具有不同數目的資料行，可以是 t1。  
  
#### <a name="result-even-with-ambiguous-result-set"></a>即使結果集模稜兩可的結果  
 使用與先前範例相同的假設。  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 結果： **int NULL**因為 dbo.t1.a 和 s1.t1.a 都有型別**int**和不同的 null 屬性。  
  
## <a name="see-also"></a>另請參閱  
 [sp_describe_undeclared_parameters &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
