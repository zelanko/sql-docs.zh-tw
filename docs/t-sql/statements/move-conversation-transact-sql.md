---
title: MOVE CONVERSATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e6b636d170432c1c5eb3b784b0f29e06f412c5ec
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781789"
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
 這是一個變數或常數，其中包含要移動之交談的交談控制代碼。 *conversation_handle* 必須是類型 **uniqueidentifier**。  
  
 TO *conversation_group_id*  
 這是一個變數或常數，其中包含要移動交談之交談群組的識別碼。 *conversation_group_id* 必須是類型 **uniqueidentifier**。  
  
## <a name="remarks"></a>Remarks  
 MOVE CONVERSATION 陳述式會將 *conversation_handle* 指定的交談移到 *conversation_group_id* 識別的交談群組。 對話只能在與同一佇列相關聯的交談群組之間重新導向。  
  
> [!IMPORTANT]  
>  如果 MOVE CONVERSATION 陳述式不是批次或預存程序中的第一個陳述式，就必須利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式結束字元 (也就是分號 **;**) 來結束前一個陳述式。  
  
 MOVE CONVERSATION 陳述式會鎖定與 *conversation_handle* 相關聯的交談群組，以及 *conversation_group_id* 所指定的交談群組，直到包含該陳述式的交易認可或回復為止。  
  
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
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [GET CONVERSATION GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-groups-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
