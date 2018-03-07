---
title: "卸除訊息類型 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_MESSAGE_TYPE_TSQL
- DROP MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- message types [Service Broker], removing
- deleting message types
- dropping message types
- DROP MESSAGE TYPE statement
- removing message types
ms.assetid: 805e8ad5-8a93-49f0-88e5-e6fca8814dd5
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c3c16a12cb8b5880f0afd82e6b3a0831402fb61
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="drop-message-type-transact-sql"></a>DROP MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除現有的訊息類型。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP MESSAGE TYPE message_type_name  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *message_type_name*  
 要刪除的訊息類型名稱。 您不可指定伺服器、資料庫和結構描述名稱。  
  
## <a name="permissions"></a>Permissions  
 卸除訊息類型的權限預設為訊息類型的擁有者、db_ddladmin 或 db_owner 固定資料庫角色的成員，以及系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
## <a name="remarks"></a>備註  
 如果有任何合約參考訊息類型，您便無法刪除這個訊息類型。  
  
## <a name="examples"></a>範例  
 下列範例會從資料庫中刪除 `//Adventure-Works.com/Expenses/SubmitExpense` 訊息類型。  
  
```  
DROP MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense] ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [變更訊息類型 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [建立訊息類型 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
