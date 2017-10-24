---
title: "建立安全性原則 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SECURITY_POLICY_TSQL
- CREATE SECURITY
- SECURITY
- CREATE_SECURITY_POLICY_TSQL
- CREATE_SECURITY_TSQL
- SECURITY POLICY
- SECURITY_TSQL
- CREATE SECURITY POLICY
dev_langs:
- TSQL
helpviewer_keywords:
- RLS
- CREATE SECURITY POLICY statement
- Row-Level Security
ms.assetid: d6ab70ee-0fa2-469c-96f6-a3c16d673bc8
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53292dc3f9f5cbd36913276496084d4648f13520
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-security-policy-transact-sql"></a>建立安全性原則 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  建立資料列層級安全性的安全性原則。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | arguments } [ , …n] ) ON table_schema_name. table_name    
      [ <block_dml_operation> ] , [ , …n] 
    [ WITH ( STATE = { ON | OFF }  [,] [ SCHEMABINDING = { ON | OFF } ] ) ]  
    [ NOT FOR REPLICATION ] 
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>引數  
 *security_policy_name*  
 安全性原則的名稱。 安全性原則名稱必須符合識別碼的規則，並且在資料庫內及對於它的結構描述都必須是唯一的。  
  
 *schema_name*  
 這是安全性原則所屬的結構描述名稱。 *schema_name*因為結構描述繫結，所以需要。  
  
 [篩選器 |區塊]  
 正繫結至目標資料表的函式的安全性述詞的類型。 篩選器述詞以無訊息方式篩選可讀取作業的資料列。 封鎖的述詞明確封鎖違反述詞函式的寫入作業。  
  
 *tvf_schema_name.security_predicate_function_name*  
 這是內嵌資料表值函數，可做為述詞使用，並會在查詢目標資料表時強制執行。 針對每個特定資料表的每項特定 DML 作業，最多只能定義一個安全性述詞。 內嵌資料表值函數必須使用 SCHEMABINDING 選項建立。  
  
 { *column_name* | *引數*}  
 做為安全性述詞函數之參數的資料行名稱或運算式。 目標資料表上的任何資料行都可以做為述詞函數的引數。 可以使用包含常值的運算式、內建函數及使用算術運算子的運算式。  
  
 *table_schema_name.table_name*  
 這是套用安全性述詞的目標資料表。 多個已停用的安全性原則可以單一資料表的特定 DML 作業，但只有一個可以啟用在任何指定時間。  
  
 *\<block_dml_operation >* block 述詞會套用特定 DML 作業。 在指定的資料列的值將評估的述詞，DML 作業之後執行 （INSERT 或 UPDATE）。 之前指定的資料列的值將評估的述詞，DML 作業之前執行 （UPDATE 或 DELETE）。 如果未不指定任何作業，則述詞會套用至所有作業。  
  
 [狀態 = {ON |**OFF** }]  
 啟用或停用強制對目標資料表執行其安全性述詞的安全性原則。 如果未指定，則會啟用正在建立的安全性原則。  
  
 [SCHEMABINDING = {ON |關閉}]  
 指出是否必須使用 SCHEMABINDING 選項建立的原則中的所有述詞函式。 根據預設，所有函式必須以 schemabinding 來建立。  
  
 NOT FOR REPLICATION  
 表示當複寫代理程式修改目標物件時，不應執行安全性原則。 如需詳細資訊，請參閱[在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
 [*table_schema_name*。]*table_name*  
 這是套用安全性述詞的目標資料表。 單一資料表可以有多個已停用的安全性原則，但無論何時都只能啟用一個安全性原則。  
  
## <a name="remarks"></a>備註  
 當使用記憶體最佳化資料表的述詞函式，您必須包含**SCHEMABINDING**並用**WITH NATIVE_COMPILATION**編譯提示。  
  
 Block 述詞會評估後會在執行對應的 DML 作業。 因此，讀取未認可的查詢可以查看將會回復的暫時性值。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 ALTER ANY SECURITY POLICY 權限和 ALTER 權限。  
  
 此外，每個加入的述詞還需要下列權限：  
  
-   正做為述詞使用之函數的 SELECT 和 REFERENCES 權限。  
  
-   正繫結至原則之目標資料表的 REFERENCES 權限。  
  
-   目標資料表中做為引數使用之每個資料行的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 **CREATE SECURITY POLICY** 語法。 如需完整的安全性原則案例的範例，請參閱[資料列層級安全性](../../relational-databases/security/row-level-security.md)。  
  
### <a name="a-creating-a-security-policy"></a>A. 建立安全性原則  
 下列語法使用篩選器述詞建立客戶資料表的安全性原則，並保持停用安全性原則。  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate]([CustomerId])   
ON [dbo].[Customer];  
```  
  
### <a name="b-creating-a-policy-that-affects-multiple-tables"></a>B. 建立影響多個資料表的原則  
 下列語法使用三個篩選器述詞建立三種資料表的安全性原則，並啟用安全性原則。  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([CustomerId])   
    ON [dbo].[Customer],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([VendorId])   
    ON [dbo].[ Vendor],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate2]([WingId])   
    ON [dbo].[Patient]  
WITH (STATE = ON);  
```  
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>C. 建立包含多個安全性述詞類型的原則  
 加入 [Sales] 資料表的篩選器述詞及 block 述詞。  
  
```  
CREATE SECURITY POLICY rls.SecPol  
    ADD FILTER PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales,  
    ADD BLOCK PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  


