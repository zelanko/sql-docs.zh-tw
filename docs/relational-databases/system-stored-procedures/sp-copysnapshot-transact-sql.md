---
title: sp_copysnapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysnapshot
- sp_copysnapshot_TSQL
helpviewer_keywords:
- sp_copysnapshot
ms.assetid: a012a32f-6f26-45bf-8046-b51cd7fec455
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7e857539c26f7806712c3c8e0fd4222064eac8c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108697"
---
# <a name="spcopysnapshot-transact-sql"></a>sp_copysnapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將指定的發行集的快照集資料夾複製到資料夾中列出 **@destination_folder** 。 這個預存程序執行於發行集資料庫的發行者端。 這個預存程序可用來將快照集複製到抽取式媒體 (如 CD-ROM)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_copysnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是快照集內容是要複製的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @destination_folder = ] 'destination_folder'` 是要複製發行集快照集內容名稱。 *destination_folder*已**nvarchar(255)** ，沒有預設值。 *Destination_folder*可以是替代位置例如另一部伺服器、 網路磁碟機或抽取式媒體 （如 Cd-rom 或抽取式磁碟）。  
  
`[ @subscriber = ] 'subscriber'` 是訂閱者的名稱。 *訂閱者*是 sysname，預設值是 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'` 是訂閱資料庫的名稱。 *subscriber_db*是 sysname，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_copysnapshot**用於所有類型的複寫。 執行訂閱者[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和更新版本無法使用替代快照集位置。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_copysnapshot**。  
  
## <a name="see-also"></a>另請參閱  
 [替代快照集資料夾位置](../../relational-databases/replication/snapshot-options.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
