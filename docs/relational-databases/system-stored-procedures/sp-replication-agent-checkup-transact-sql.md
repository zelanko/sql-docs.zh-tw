---
title: sp_replication_agent_checkup （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 25daf9098c1c4da74d8c5adfdac062016f68ce96
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725712"
---
# <a name="sp_replication_agent_checkup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  檢查複寫代理程式的每個散發資料庫，這些複寫代理程式正在執行中，但未在指定活動訊號間隔內記錄記錄。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>引數  
`[ @heartbeat_interval = ] 'heartbeat_interval'`這是代理程式在未記錄進度訊息的情況下所能執行的最大分鐘數。 *heartbeat_interval*是**int**，預設值是10分鐘。  
  
## <a name="return-code-values"></a>傳回碼值  
 **sp_replication_agent_checkup**會對每個代理程式引發錯誤14151，它會偵測為可疑。 另外，它也會記錄代理程式的失敗記錄訊息。  
  
## <a name="remarks"></a>備註  
 **sp_replication_agent_checkup**用於快照式複寫、異動複寫和合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_replication_agent_checkup**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
