---
title: "CURRENT_TRANSACTION_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURRENT_TRANSACTION_ID
- CURRENT_TRANSACTION_ID_TSQL
- sys.CURRENT_TRANSACTION_ID
- sys.CURRENT_TRANSACTION_ID_TSQL
helpviewer_keywords:
- CURRENT_TRANSACTION_ID function
ms.assetid: 82cd9f92-d935-45a0-a433-620d6e15b467
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ef8f593f50ce1d27642d1d179a57bebb2b4473e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="currenttransactionid-transact-sql"></a>CURRENT_TRANSACTION_ID (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

傳回目前工作階段中的目前交易的交易識別碼。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CURRENT_TRANSACTION_ID( )  
  
```  
  
## <a name="return-types"></a>傳回型別
**bigint**
  
## <a name="return-value"></a>傳回值  
取自目前交易中目前的工作階段中，交易識別碼[sys.dm_tran_current_transaction &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md).
  
## <a name="permissions"></a>Permissions  
任何使用者可能會傳回目前工作階段的交易識別碼。
  
## <a name="examples"></a>範例  
下列範例會傳回目前工作階段的交易識別碼：
  
```sql
SELECT CURRENT_TRANSACTION_ID();  
```  
  
## <a name="see-also"></a>另請參閱
[sp_set_session_context &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)  
[SESSION_CONTEXT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/session-context-transact-sql.md)  
[資料列層級安全性](../../relational-databases/security/row-level-security.md)  
[CONTEXT_INFO &#40;TRANSACT-SQL &#41;](../../t-sql/functions/context-info-transact-sql.md)  
[SET CONTEXT_INFO &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
