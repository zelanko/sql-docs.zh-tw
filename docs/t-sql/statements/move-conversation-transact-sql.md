---
title: "移動交談 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
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
- MOVE_CONVERSATION_TSQL
- MOVE CONVERSATION
- MOVE_TSQL
- MOVE
dev_langs:
- TSQL
helpviewer_keywords:
- moving conversations
- MOVE CONVERSATION statement
- relocating conversations
- conversations [Service Broker], groups
- conversations [Service Broker], moving
ms.assetid: 1da4d2c9-e767-434e-b49b-615711a7f626
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd8c5e548bf45fe4a2fc6bf0638ebb5282981263
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="move-conversation-transact-sql"></a>MOVE CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將交談移到不同的交談群組。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
MOVE CONVERSATION conversation_handle  
   TO conversation_group_id  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *conversation_handle*  
 這是一個變數或常數，其中包含要移動之交談的交談控制代碼。 *conversation_handle*必須是型別**uniqueidentifier**。  
  
 TO *conversation_group_id*  
 這是一個變數或常數，其中包含要移動交談之交談群組的識別碼。 *conversation_group_id*必須是型別**uniqueidentifier**。  
  
## <a name="remarks"></a>備註  
 MOVE CONVERSATION 陳述式會在指定的交談*conversation_handle*所識別的交談群組*conversation_group_id*。 對話只能在與同一佇列相關聯的交談群組之間重新導向。  
  
> [!IMPORTANT]  
>  如果 MOVE CONVERSATION 陳述式不是在批次或預存程序的第一個陳述式，必須以分號結束之前的陳述式 (**;**)、[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式結束字元。  
  
 MOVE CONVERSATION 陳述式鎖定交談群組相關聯*conversation_handle*和所指定的交談群組*conversation_group_id*直到交易包含陳述式認可或回復。  
  
 在使用者自訂函數中，MOVE CONVERSATION 無效。  
  
## <a name="permissions"></a>Permissions  
 若要移動交談，目前使用者必須是該交談和交談群組的擁有者，或是系統管理員 (sysadmin) 固定伺服器角色的成員，或是 db_owner 固定資料庫角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會將交談移到不同的交談群組。  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER,  
        @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_handle =  
    <retrieve conversation handle from database> ;  
SET @conversation_group_id =  
    <retrieve conversation group ID from database> ;  
  
MOVE CONVERSATION @conversation_handle TO @conversation_group_id ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DIALOG CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;TRANSACT-SQL &#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
