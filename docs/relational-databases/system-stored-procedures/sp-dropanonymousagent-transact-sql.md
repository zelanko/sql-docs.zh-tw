---
title: sp_dropanonymousagent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0878e6f946cd88eb481e0cd61bdf4183883dd01e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829926"
---
# <a name="spdropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從發行者卸除在散發者端之複寫監視的匿名代理程式。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>引數  
 [  **@subid=**] *sub_id*  
 這是匿名訂閱的全域識別碼。 *sub_id*已**uniqueidentifier**，沒有預設值。 此識別碼可以擷取 「 訂閱者 」 使用**sp_helppullsubscription**。 中的值**subid**傳回的結果集的欄位是這個全域識別碼。  
  
 [  **@type=**]*類型*  
 這是訂閱的類型。 *型別*已**int**，沒有預設值。 有效值**1**或是**2**。 指定**1**，如果快照式複寫或異動複寫使用 「 散發代理程式。 指定**2**，如果合併式複寫使用 「 合併代理程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropanonymousagent**用於所有類型的複寫。  
  
 這個預存程序只能用來卸除匿名訂閱代理程式，無法用來卸除已知的訂閱。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**散發資料庫中的固定的資料庫角色可以執行**sp_dropanonymousagent**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
