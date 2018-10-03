---
title: sp_dropdistpublisher & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a5b87dc95534d432bf5676b6a0e1c5d2ff08bfa5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734686"
---
# <a name="spdropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除散發發行者。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=** ] **'***發行者***'**  
 這是要卸除的發行者。 *發行者*已**sysname**，沒有預設值。  
  
 [  **@no_checks=** ] *no_checks*  
 指定是否**sp_dropdistpublisher**檢查發行者已解除安裝散發者的伺服器。 *no_checks*已**位元**，預設值是**0**。  
  
 如果**0**，複寫會確認遠端發行者已解除安裝本機伺服器作為散發者。 如果發行者在本機，複寫會確認本機伺服器中沒有其餘發行集或散發物件。  
  
 如果**1**，即使無法到達遠端發行者，會卸除散發發行者相關聯的所有複寫物件。 完成之後，遠端發行者必須使用解除安裝複寫[sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)具有**@ignore_distributor**  =  **1**。  
  
 [  **@ignore_distributor=** ] *ignore_distributor*  
 指定當移除發行者時，是否要將散發物件留在散發者中。 *ignore_distributor*已**元**而且可以是下列其中一個值：  
  
 **1** = 散發物件屬於*發行者*維持在 「 散發者 」。  
  
 **0** = 散發物件*發行者*會清除在散發者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropdistpublisher**用於所有類型的複寫。  
  
 如果無法卸除 「 發行者 」 端卸除 Oracle 發行者 」 時**sp_dropdistpublisher**傳回發生錯誤，「 發行者 」 端的散發者物件會移除。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_dropdistpublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
