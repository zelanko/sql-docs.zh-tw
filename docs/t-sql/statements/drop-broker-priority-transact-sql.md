---
title: "DROP BROKER PRIORITY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_BROKER_PRIORITY_TSQL
- DROP BROKER PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- DROP BROKER PRIORITY statement
ms.assetid: 09ee6c5b-af94-4a4b-a0e2-f9eac50e43aa
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 254914f3b92289faf19a37b4651e7c95804ac791
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-broker-priority-transact-sql"></a>DROP BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫中移除交談優先權。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP BROKER PRIORITY ConversationPriorityName  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *ConversationPriorityName*  
 指定要移除的交談優先權名稱。  
  
## <a name="remarks"></a>備註  
 當您卸除交談優先權時，任何現有的交談都會繼續運作，而使用的優先權等級是從交談優先權指派。  
  
## <a name="permissions"></a>Permissions  
 建立交談優先權的權限預設為 db_ddladmin 或 db_owner 固定資料庫角色的成員，以及 sysadmin 固定伺服器角色的成員。 需要資料庫的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會卸除名稱為 `InitiatorAToTargetPriority` 的交談優先權。  
  
```  
DROP BROKER PRIORITY InitiatorAToTargetPriority;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER BROKER PRIORITY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [建立 BROKER 優先權 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  

