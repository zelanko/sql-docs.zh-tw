---
title: "變更安全性原則 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs: TSQL
helpviewer_keywords: ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0b420b7b73af8f32d2de9dac39cc4f57b41680c7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-security-policy-transact-sql"></a>變更安全性原則 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  改變安全性原則。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```tsql  
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>引數  
 security_policy_name  
 安全性原則的名稱。 安全性原則名稱必須符合識別碼的規則，並且在資料庫內及對於它的結構描述都必須是唯一的。  
  
 schema_name  
 這是安全性原則所屬的結構描述名稱。 *schema_name*因為結構描述繫結，所以需要。  
  
 [篩選器 |區塊]  
 正繫結至目標資料表的函式的安全性述詞的類型。 篩選器述詞以無訊息方式篩選可讀取作業的資料列。 封鎖的述詞明確封鎖違反述詞函式的寫入作業。  
  
 tvf_schema_name.security_predicate_function_name  
 這是內嵌資料表值函數，可做為述詞使用，並會在查詢目標資料表時強制執行。 針對每個特定資料表的每項特定 DML 作業，最多只能定義一個安全性述詞。 內嵌資料表值函數必須使用 SCHEMABINDING 選項建立。  
  
 { column_name | arguments }  
 做為安全性述詞函數之參數的資料行名稱或運算式。 目標資料表上的任何資料行都可以做為述詞函數的引數。 可以使用包含常值的運算式、內建函數及使用算術運算子的運算式。  
  
 *table_schema_name.table_name*  
 這是套用安全性述詞的目標資料表。 多個已停用的安全性原則可以單一資料表的特定 DML 作業，但只有一個可以啟用在任何指定時間。  
  
 *\<block_dml_operation >*  
 Block 述詞會套用特定 DML 作業。 在指定的資料列的值將評估的述詞，DML 作業之後執行 （INSERT 或 UPDATE）。 之前指定的資料列的值將評估的述詞，DML 作業之前執行 （UPDATE 或 DELETE）。 如果未不指定任何作業，則述詞會套用至所有作業。  
  
 您無法改變的 block 述詞會套用的操作，因為作業用來唯一識別此述詞。 相反地，您必須卸除此述詞，並加入一個新的新作業。  
  
 WITH ( STATE = { ON | OFF } )  
 啟用或停用強制對目標資料表執行其安全性述詞的安全性原則。 如果未指定，則會停用正在建立的安全性原則。  
  
 NOT FOR REPLICATION  
 表示當複寫代理程式修改目標物件時，不應執行安全性原則。 如需詳細資訊，請參閱[在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
 table_schema_name.table_name  
 這是套用安全性述詞的目標資料表。 單一資料表可以有多個已停用的安全性原則，但無論何時都只能啟用一個安全性原則。  
  
## <a name="remarks"></a>備註  
 ALTER SECURITY POLICY 陳述式位於交易的範圍內。 如果回復交易，也會回復此陳述式。  
  
 當使用記憶體最佳化資料表的述詞函式，安全性原則必須包含**SCHEMABINDING**並用**WITH NATIVE_COMPILATION**編譯提示。 無法以 ALTER 陳述式變更 SCHEMABINDING 引數，因為它套用到所有述詞。 若要變更結構描述繫結中，您必須卸除並重新建立安全性原則。  
  
 Block 述詞會評估後會在執行對應的 DML 作業。 因此，讀取未認可的查詢可以查看將會回復的暫時性值。  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY SECURITY POLICY 權限。  
  
 此外，每個加入的述詞還需要下列權限：  
  
-   正做為述詞使用之函數的 SELECT 和 REFERENCES 權限。  
-   正繫結至原則之目標資料表的 REFERENCES 權限。  
-   目標資料表中做為引數使用之每個資料行的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用**ALTER SECURITY POLICY**語法。 如需完整的安全性原則案例的範例，請參閱[資料列層級安全性](../../relational-databases/security/row-level-security.md)。  
  
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
  
### <a name="e-changing-a-block-predicate"></a>E. 變更的區塊述詞  
 變更資料表上的作業的區塊述詞函式。  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
