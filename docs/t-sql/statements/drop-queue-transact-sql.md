---
description: DROP QUEUE (Transact-SQL)
title: DROP QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4bf41bb420ddaaccd0f1899c641a30a17bbb8fcd
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380340"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  卸除現有的佇列。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *database_name*  
 要卸除之佇列所在的資料庫名稱。 若未提供 *database_name*，預設為目前的資料庫。  
  
 *schema_name (object)*  
 擁有要卸除之佇列的結構描述名稱。 若未提供 *schema_name*，預設為目前使用者的預設結構描述。  
  
 *queue_name*  
 要卸除的佇列名稱。  
  
## <a name="remarks"></a>備註  
 如果有任何服務參考佇列，您便不能卸除這個佇列。  
  
## <a name="permissions"></a>權限  
 卸除佇列的權限預設為佇列的擁有者、**db_ddladmin** 或 **db_owner** 固定資料庫角色的成員，以及 **sysadmin** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會從目前的資料庫中卸除 **ExpenseQueue** 佇列。  
  
```sql  
DROP QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
