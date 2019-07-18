---
title: SESSION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 59aa8de6752ead8e8b8dbef92035ad59e5995307
ms.sourcegitcommit: 869d4de6c807a37873b66e5479d2c5ceff9efb85
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2019
ms.locfileid: "67559453"
---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  傳回目前工作階段內容中指定索引鍵的值。 會使用 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md) 程序來設定值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>引數  
 'key'  
 要擷取之值的索引鍵 (類型為 sysname)。  
  
## <a name="return-type"></a>傳回類型  
 **sql_variant**  
  
## <a name="return-value"></a>傳回值  
 為與工作階段內容中指定索引鍵建立關聯的值，或為 NULL (當該索引鍵沒有設定值時)。  
  
## <a name="permissions"></a>權限  
 任何使用者都可以讀取其工作階段的工作階段內容。  
  
## <a name="remarks"></a>Remarks  
 SESSION_CONTEXT 的 MARS 行為與 CONTEXT_INFO 相似。 若 MARS 批次設定索引鍵值組，則新的值將不會在相同連線中的另外一個 MARS 批次中傳回，除非它們是在設定新值的批次完成之後才啟動。 若在連線上有多個 MARS 作用中，值將無法設為「唯讀」(read_only)。 這可防止競爭條件以及針對哪個值「會獲勝」的不確定性。  
  
## <a name="examples"></a>範例  
 下面這個簡單的範例會先將索引鍵 `user_id` 的工作階段值設為 4，再使用 **SESSION_CONTEXT** 函式來擷取該值。  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;Transact-SQL&#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO  &#40;Transact-SQL&#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  
