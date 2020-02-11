---
title: sp_set_session_coNtext （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_session_context
- sp_set_session_context_TSQL
- sys.sp_set_session_context
- sys.sp_set_session_context_TSQL
helpviewer_keywords:
- sp_set_session_context
ms.assetid: 7a3a3b2a-1408-4767-a376-c690e3c1fc5b
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a57bf4acff6f8d0d08f86852de5ecc0411211c67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104396"
---
# <a name="sp_set_session_context-transact-sql"></a>sp_set_session_coNtext （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

在會話內容中設定索引鍵/值組。  
  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_set_session_context [ @key= ] N'key', [ @value= ] 'value'  
    [ , [ @read_only = ] { 0 | 1 } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 [ @key= ]N'key'  
 要設定的索引鍵，屬於**sysname**類型。 金鑰大小上限為128個位元組。  
  
 [ @value= ]value  
 指定之索引鍵的值，其類型為**SQL_variant**。 將值設為 Null 會釋出記憶體。 大小上限是 8,000 位元組。  
  
 [ @read_only= ]{0 | 1}  
 **Bit**類型的旗標。 如果是1，則無法在此邏輯連接上再次變更指定之索引鍵的值。 如果為0（預設值），則可以變更此值。  
  
## <a name="permissions"></a>權限  
 任何使用者都可以設定其會話的會話內容。  
  
## <a name="remarks"></a>備註  
 和其他預存程式一樣，只有常值和變數（非運算式或函式呼叫）可以當做參數來傳遞。  
  
 會話內容的總大小限制為 1 MB。 如果您設定的值會導致超過此限制，則語句會失敗。 您可以監視 sys.databases 中的整體記憶體使用量[dm_os_memory_objects &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)。  
  
 您可以藉由查詢[sys.databases dm_os_memory_cache_counters &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)監視整體記憶體使用量，如下所示：`SELECT * FROM sys.dm_os_memory_cache_counters WHERE type = 'CACHESTORE_SESSION_CONTEXT';`  
  
## <a name="examples"></a>範例  
 下列範例顯示如何設定，然後傳回名為 language 且值為英文的會話內容索引鍵。  
  
```  
EXEC sys.sp_set_session_context @key = N'language', @value = 'English';  
SELECT SESSION_CONTEXT(N'language');  
```  
  
 下列範例示範選擇性唯讀旗標的用法。  
  
```  
EXEC sys.sp_set_session_context @key = N'user_id', @value = 4, @read_only = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-sql&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
