---
title: sp_dropdistpublisher （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 060b3b793adf53ab988cbba8b82ae683dac1e40a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830182"
---
# <a name="sp_dropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  卸除散發發行者。 這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是要卸載的發行者。 *publisher*是**sysname**，沒有預設值。  
  
`[ @no_checks = ] no_checks`指定**sp_dropdistpublisher**是否檢查發行者是否已將伺服器卸載為散發者。 *no_checks*是**bit**，預設值是**0**。  
  
 如果為**0**，則複寫會確認遠端發行者是否已將本機伺服器卸載為散發者。 如果發行者在本機，複寫會確認本機伺服器中沒有其餘發行集或散發物件。  
  
 如果是**1**，即使無法連線到遠端發行者，也會卸載與散發發行者相關聯的所有複寫物件。 這麼做之後，遠端發行者必須使用** \@ ignore_distributor**1 的[sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)來卸載複寫  =  ** **。  
  
`[ @ignore_distributor = ] ignore_distributor`指定當移除發行者時，散發物件是否留在散發者端。 *ignore_distributor*是**bit** ，而且可以是下列其中一個值：  
  
 **1** = 屬於發行者的散發物件會保留在散發*者*端。  
  
 **0** = 在散發者上清除*發行者*的散發物件。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropdistpublisher**用於所有類型的複寫中。  
  
 卸載「Oracle 發行者」時，如果無法捨棄「發行者」 **sp_dropdistpublisher**會傳回錯誤，並移除「發行者」的「散發者」物件。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_dropdistpublisher**。  
  
## <a name="see-also"></a>另請參閱  
 [停用發行和散發](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
