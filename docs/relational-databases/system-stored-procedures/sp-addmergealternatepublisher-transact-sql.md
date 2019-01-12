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
ms.openlocfilehash: 21d0ea34f3521333976ce00a3f5b823c3fcb816a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129298"
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
 [  **@publisher=**] **'**_發行者_**'**  
 這是發行者的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 這是發行集資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [  **@publication=**] **'**_發行集_**'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@alternate_publisher=**] **'**_alternate_synchronization_partner_**'**  
 這是替代發行者的名稱。 *alternate_synchronization_partner*已**sysname**，沒有預設值。  
  
 [  **@alternate_publisher_db=**] **'**_alternate_publisher_db_**'**  
 這是替代發行者上的發行集資料庫名稱。 *alternate_publisher_db*已**sysname**，沒有預設值。  
  
 [  **@alternate_publication=**] **'**_alternate_synchronization_partner_**'**  
 這是替代同步處理夥伴上的發行集名稱。 *alternate_synchronization_partner*已**sysname**，沒有預設值。  
  
 [  **@alternate_distributor=**] **'**_alternate_distributor_**'**  
 這是替代同步處理夥伴的散發者名稱。 *alternate_distributor*已**sysname**，沒有預設值。  
  
 [  **@friendly_name=**] **'**_friendly_name_**'**  
 這是一個顯示名稱，用來識別組成替代同步處理夥伴之發行者、發行集和散發者的關聯。 *friendly_name*已**nvarchar(255)**，預設值是 NULL。  
  
 [  **@reserved=**] **'**_保留_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addmergealternatepublisher**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addmergealternatepublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dropmergealternatepublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
