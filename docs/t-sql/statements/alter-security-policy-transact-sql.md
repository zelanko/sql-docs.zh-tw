---
title: ALTER SECURITY POLICY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0696b96e83aac5ca66b43d38c11adceab702c10f
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87112560"
---
# <a name="alter-security-policy-transact-sql"></a>ALTER SECURITY POLICY (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

改變安全性原則。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , ...n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , ...n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ) ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  

## <a name="arguments"></a>引數
security_policy_name  
安全性原則的名稱。 安全性原則名稱必須滿足識別碼的規則，而且在資料庫內及對其結構描述而言都必須是唯一的。  
  
schema_name  
這是安全性原則所屬的結構描述名稱。 因為結構描述繫結，*schema_name* 是必要的。  
  
[ FILTER | BLOCK ]  
繫結至目標資料表之函數的安全性述詞類型。 FILTER 述詞會以無訊息方式篩選讀取作業可用的資料列。 BLOCK 述詞會明確封鎖違反述詞函式的寫入作業。  
  
tvf_schema_name.security_predicate_function_name  
這是內嵌資料表值函式，可用來作為述詞，並且在對目標資料表進行查詢時強制執行。 您最多可以針對特定資料表的特定 DML 作業定義一個安全性述詞。 使用 SCHEMABINDING 選項建立內嵌資料表值函式。  
  
{ column_name | arguments }  
做為安全性述詞函數之參數的資料行名稱或運算式。 目標資料表上的任何資料行都可以做為述詞函數的引數。 可以使用包含常值的運算式、內建運算式及使用算術運算子的運算式。  
  
*table_schema_name.table_name*  
這是適用於安全性述詞的目標資料表。 您可以將多個已停用的安全性原則目標設為特定 DML 作業的單一資料表，但無論何時都只能啟用一個安全性原則。  
  
*\<block_dml_operation>*  
適用於已套用封鎖述詞的特定 DML 作業。 AFTER 會指定在執行 DML 作業 (INSERT 或 UPDATE) 之後，根據資料列值評估述詞。 BEFORE 會指定在執行 DML 作業 (INSERT 或 UPDATE) 之前，根據資料列值評估述詞。 如果沒有指定作業，則會將述詞套用至所有作業。  
  
您無法改變 (ALTER) 已套用封鎖述詞的作業，因為該作業會用來唯一識別該述詞。 相反地，您必須卸除該述詞，並針對新的作業加入一個新的述詞。  
  
WITH ( STATE = { ON | OFF } )  
啟用或停用強制對目標資料表執行其安全性述詞的安全性原則。 如果未指定，則會啟用正在建立的安全性原則。  
  
NOT FOR REPLICATION  
表示當複寫代理程式修改目標物件時，不應執行安全性原則。 如需詳細資訊，請參閱[在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
table_schema_name.table_name  
這是適用於已套用安全性述詞的目標資料表。 單一資料表可以有多個已停用的安全性原則，但無論何時都只能啟用一個安全性原則。  
  
## <a name="remarks"></a>備註  
ALTER SECURITY POLICY 陳述式位於交易的範圍內。 如果回復交易，也會回復此陳述式。  
  
當使用述詞函數與記憶體最佳化資料表時，安全性原則必須包含 **SCHEMABINDING** 並使用 **WITH NATIVE_COMPILATION** 編譯提示。 SCHEMABINDING 引數無法使用 ALTER 陳述式來變更，因為它會套用到所有述詞。 若要變更結構描述繫結，您必須卸除並重新建立安全性原則。  
  
BLOCK 述詞會在執行對應的 DML 作業後加以評估。 因此，READ UNCOMMITTED 查詢可以查看將回復的暫時值。  
  
## <a name="permissions"></a>權限  
需要 ALTER ANY SECURITY POLICY 權限。  
  
此外，每個加入的述詞還需要下列權限：  
  
-   正做為述詞使用之函數的 SELECT 和 REFERENCES 權限。  
-   正繫結至原則之目標資料表的 REFERENCES 權限。  
-   目標資料表中做為引數使用之每個資料行的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
下列範例示範如何使用 **ALTER SECURITY POLICY** 語法。 如需完整安全性原則案例的範例，請參閱[資料列層級安全性](../../relational-databases/security/row-level-security.md)。  
  
### <a name="a-adding-an-additional-predicate-to-a-policy"></a>A. 將額外的述詞加入原則  
下列語法會改變安全性原則，在 `mytable` 資料表上加入篩選器述詞。  
  
```  
ALTER SECURITY POLICY pol1   
    ADD FILTER PREDICATE schema_preds.SecPredicate(column1)   
    ON myschema.mytable;  
```  
  
### <a name="b-enabling-an-existing-policy"></a>B. 啟用現有的原則  
下列範例使用 ALTER 語法，來啟用安全性原則。  
  
```  
ALTER SECURITY POLICY pol1 WITH ( STATE = ON );  
```  
  
### <a name="c-adding-and-dropping-multiple-predicates"></a>C. 加入及卸除多個述詞  
下列語法會改變安全性原則，在 `mytable1` 和 `mytable3` 資料表上加入篩選器述詞，並移除 `mytable2` 資料表上的篩選器述詞。  
  
```  
ALTER SECURITY POLICY pol1  
ADD FILTER PREDICATE schema_preds.SecPredicate1(column1)   
    ON myschema.mytable1,  
DROP FILTER PREDICATE   
    ON myschema.mytable2,  
ADD FILTER PREDICATE schema_preds.SecPredicate2(column2, 1)   
    ON myschema.mytable3;  
```  
  
### <a name="d-changing-the-predicate-on-a-table"></a>D. 變更資料表上的述詞  
下列語法會將 mytable 資料表上的現有篩選述詞變更為 SecPredicate2 函數。  
  
```  
ALTER SECURITY POLICY pol1  
    ALTER FILTER PREDICATE schema_preds.SecPredicate2(column1)  
        ON myschema.mytable;  
```  
  
### <a name="e-changing-a-block-predicate"></a>E. 變更 BLOCK 述詞  
變更資料表上作業的 BLOCK 述詞函數。  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>另請參閱  
[資料列層級安全性](../../relational-databases/security/row-level-security.md)   
[CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
[DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
[sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
[sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
