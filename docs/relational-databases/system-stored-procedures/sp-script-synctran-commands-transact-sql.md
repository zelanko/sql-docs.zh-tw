---
title: sp_script_synctran_commands (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3705a28d85c7375aad701d77a517719778954c25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32997755"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含的指令碼會產生**sp_addsynctrigger**可更新訂閱，訂閱者端套用的呼叫。 有一個**sp_addsynctrigger**呼叫每個發行項中發行集。 產生的指令碼也包含**sp_addqueued_artinfo**建立的呼叫**MSsubsciption_articles**需要處理佇列發行集的資料表。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication** = ] **'***publication***'**  
 這是要編寫指令碼的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ **@article** =] **'***文章***'**  
 這是要編寫指令碼的發行項名稱。 *發行項*是**sysname**，預設值是**所有**，以指定的所有發行項會編寫指令碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="results-set"></a>結果集  
 **sp_script_synctran_commands**傳回的結果集包含單一**nvarchar （4000)** 資料行。 這個結果集形成完整的指令碼需要建立這兩者**sp_addsynctrigger**和**sp_addqueued_artinfo**訂閱者端套用的呼叫。  
  
## <a name="remarks"></a>備註  
 **sp_script_synctran_commands**用於快照式和異動複寫。  
  
 **sp_addqueued_artinfo**用於佇列更新訂閱。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_script_synctran_commands**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsynctriggers &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
