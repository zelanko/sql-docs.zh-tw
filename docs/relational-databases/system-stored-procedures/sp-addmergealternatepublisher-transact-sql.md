---
title: sp_addmergealternatepublisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: efbf4195294ce8bc279a2ed995ce09a5f384a82c
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58491972"
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新增訂閱者使用替代同步處理夥伴的能力。 發行集屬性必須指定訂閱者能夠與其他發行者同步處理。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmergealternatepublisher [ @publisher= ] 'publisher'  
          , [ @publisher_db= ] 'publisher_db'  
          , [ @publication= ] 'publication'  
          , [ @alternate_publisher= ] 'alternate_synchronization_partner'  
          , [ @alternate_publisher_db= ] 'alternate_publisher_db'  
          , [ @alternate_publication= ] 'alternate_synchronization_partner'  
     , [ @alternate_distributor= ] 'alternate_distributor'   
    [ , [ @friendly_name= ] 'friendly_name' ]   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 是 「 發行者 」 的名稱。 *發行者*已**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行集資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @alternate_publisher = ] 'alternate_synchronization_partner'` 是替代發行者的名稱。 *alternate_synchronization_partner*已**sysname**，沒有預設值。  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'` 是替代發行者的發行集資料庫的名稱。 *alternate_publisher_db*已**sysname**，沒有預設值。  
  
`[ @alternate_publication = ] 'alternate_synchronization_partner'` 是替代同步夥伴的發行集的名稱。 *alternate_synchronization_partner*已**sysname**，沒有預設值。  
  
`[ @alternate_distributor = ] 'alternate_distributor'` 為替代同步夥伴的散發者名稱。 *alternate_distributor*已**sysname**，沒有預設值。  
  
`[ @friendly_name = ] 'friendly_name'` 是可供識別之發行者、 發行集和組成替代同步夥伴的散發者關聯的顯示名稱。 *friendly_name*已**nvarchar(255)**，預設值是 NULL。  
  
`[ @reserved = ] 'reserved'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergealternatepublisher**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergealternatepublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dropmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
