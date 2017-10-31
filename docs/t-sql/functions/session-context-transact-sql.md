---
title: "SESSION_CONTEXT (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSION_CONTEXT
- sys.SESSION_CONTEXT
- SESSION_CONTEXT_TSQL
- sys.SESSION_CONTEXT_TSQL
helpviewer_keywords:
- SESSION_CONTEXT function
ms.assetid: b6bdbc54-331a-43cc-ab3d-3872d6a12100
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 23eea4b51009272ae06987ee2e9c1730750b3d6d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="sessioncontext-transact-sql"></a>SESSION_CONTEXT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回目前工作階段內容中的指定之索引鍵的值。 值會設定使用[sp_set_session_context &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SESSION_CONTEXT(N'key')  
```  
  
## <a name="arguments"></a>引數  
 ' key'  
 索引鍵 (sysname 類型) 所擷取的值。  
  
## <a name="return-type"></a>傳回類型  
 **sql_variant**  
  
## <a name="return-value"></a>傳回值  
 如果已不設定任何值，該金鑰的使用中的工作階段內容或為 NULL 的指定索引鍵關聯的值。  
  
## <a name="permissions"></a>Permissions  
 任何使用者可以讀取他們的工作階段的工作階段內容。  
  
## <a name="remarks"></a>備註  
 相似的 CONTEXT_INFO SESSION_CONTEXT 的 MARS 行為。 如果 MARS 批次將索引鍵-值組，則新值將不會傳回其他 MARS 批次中相同的連接上除非它們啟動設定的新值之批次完成後。 如果多個 MARS 批次的連接上作用中，值不能設為"read_only。 」 這可避免競爭條件和不具決定性有關哪些值為"wins"。  
  
## <a name="examples"></a>範例  
 下列簡單範例會設定索引鍵的工作階段內容值`user_id`至 4，然後使用**SESSION_CONTEXT**函式可擷取的值。  
  
```  
EXEC sp_set_session_context 'user_id', 4;  
SELECT SESSION_CONTEXT(N'user_id');  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [CURRENT_TRANSACTION_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/current-transaction-id-transact-sql.md)   
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [CONTEXT_INFO &#40;TRANSACT-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)   
 [SET CONTEXT_INFO &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)  
  
  

