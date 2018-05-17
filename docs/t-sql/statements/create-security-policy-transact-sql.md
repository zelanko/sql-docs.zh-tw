---
title: CREATE SECURITY POLICY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3270e3e74eb11c2caace27137c8492ecea3e6e93
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-security-policy-transact-sql"></a>CREATE SECURITY POLICY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  建立資料列層級安全性的安全性原則。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | expression } [ , …n] ) ON table_schema_name. table_name    
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
 這是安全性原則所屬的結構描述名稱。 因為結構描述繫結，*schema_name* 是必要的。  
  
 [ FILTER | BLOCK ]  
 繫結至目標資料表之函式的安全性述詞類型。 FILTER 述詞會以無訊息方式篩選讀取作業可用的資料列。 BLOCK 述詞會明確封鎖違反述詞函式的寫入作業。  
  
 *tvf_schema_name.security_predicate_function_name*  
 這是內嵌資料表值函數，可做為述詞使用，並會在查詢目標資料表時強制執行。 針對每個特定資料表的每項特定 DML 作業，最多只能定義一個安全性述詞。 內嵌資料表值函數必須使用 SCHEMABINDING 選項建立。  
  
 { *column_name* | *expression* }  
 做為安全性述詞函數參數的資料行名稱或運算式。 可以使用目標資料表上的任何資料行。 [運算式](../../t-sql/language-elements/expressions-transact-sql.md)只可包含目標資料表的常數、內建純量函數、運算子和資料行中。 必須針對函式的各個參數指定資料行名稱或運算式。  
  
 *table_schema_name.table_name*  
 這是套用安全性述詞的目標資料表。 您可以將多個已停用的安全性原則目標設為特定 DML 作業的單一資料表，但無論何時都只能啟用一個安全性原則。  
  
 *\<block_dml_operation>* 要套用封鎖述詞的特定 DML 作業。 AFTER 可指定在 DML 作業 (INSERT 或 UPDATE) 執行之後，根據資料列的值來評估述詞。 BEFORE 可指定在 DML 作業 (UPDATE 或 DELETE) 執行之前，根據資料列的值來評估述詞。 如果沒有指定作業，則會將述詞套用至所有作業。  
  
 [ STATE = { ON | **OFF** } ]  
 啟用或停用強制對目標資料表執行其安全性述詞的安全性原則。 如果未指定，則會啟用正在建立的安全性原則。  
  
 [ SCHEMABINDING = { ON | OFF } ]  
 指出是否必須使用 SCHEMABINDING 選項來建立原則中的所有述詞函式。 根據預設，所有函式都必須以 SCHEMABINDING 來建立。  
  
 NOT FOR REPLICATION  
 表示當複寫代理程式修改目標物件時，不應執行安全性原則。 如需詳細資訊，請參閱[在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
 [*table_schema_name*.] *table_name*  
 這是套用安全性述詞的目標資料表。 單一資料表可以有多個已停用的安全性原則，但無論何時都只能啟用一個安全性原則。  
  
## <a name="remarks"></a>Remarks  
 搭配使用述詞函式與記憶體最佳化資料表時，您必須包含 **SCHEMABINDING** 並使用 **WITH NATIVE_COMPILATION** 編譯提示。  
  
 系統會在執行對應的 DML 作業後評估封鎖述詞。 因此，READ UNCOMMITTED 查詢可以查看之後會回復的暫時性值。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 ALTER ANY SECURITY POLICY 權限和 ALTER 權限。  
  
 此外，每個加入的述詞還需要下列權限：  
  
-   正做為述詞使用之函數的 SELECT 和 REFERENCES 權限。  
  
-   正繫結至原則之目標資料表的 REFERENCES 權限。  
  
-   目標資料表中做為引數使用之每個資料行的 REFERENCES 權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 **CREATE SECURITY POLICY** 語法。 如需完整安全性原則案例的範例，請參閱[資料列層級安全性](../../relational-databases/security/row-level-security.md)。  
  
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
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>C. 建立包含多種安全性述詞類型的原則  
 將篩選述詞和封鎖述詞新增至 Sales 資料表。  
  
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
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  

