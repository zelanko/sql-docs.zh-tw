---
title: sp_adjustpublisheridentityrange （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords:
- sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1f58c1a212c722873f66d940de691c89d13d08f5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716307"
---
# <a name="sp_adjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  調整發行集的識別範圍，再依據發行集的臨界值來重新配置新的範圍。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是重新配置新識別範圍的發行集名稱。 *發行*集是**sysname**，預設值是 Null。  
  
`[ @table_name = ] 'table_name'`這是重新配置新識別範圍的資料表名稱。 *table_name*是**sysname**，預設值是 Null。  
  
`[ @table_owner = ] 'table_owner'`這是在發行者端之資料表的擁有者。 *table_owner*是**sysname**，預設值是 Null。 如果未指定*table_owner* ，就會使用目前使用者的名稱。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_adjustpublisheridentityrange**用於所有類型的複寫中。  
  
 如果是啟用了自動識別範圍的發行集，散發代理程式或合併代理程式便能夠針對基於臨界值的發行集識別範圍的自動調整來進行回應。 不過，如果基於某些原因，散發代理程式或合併代理程式尚未執行一段時間，而且識別範圍資源已大量耗用到臨界值，則使用者可以呼叫**sp_adjustpublisheridentityrange**來為發行者配置新的值範圍。  
  
 執行**sp_adjustpublisheridentityrange**時，必須指定*發行*集或*table_name* 。 如果同時指定這兩者，或兩者都未指定，就會傳回錯誤。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_adjustpublisheridentityrange**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
