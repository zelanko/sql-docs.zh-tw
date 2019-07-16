---
title: sp_redirect_publisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
author: stevestein
ms.author: sstein
ms.openlocfilehash: cde6f00d16bcff4ee56513f515cf2ecac93a1b5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002517"
---
# <a name="spredirectpublisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為現有的發行者/資料庫配對指定重新導向的發行者。 如果發行者資料庫屬於 Alwayson 可用性群組，重新導向的發行者就會是可用性群組相關聯的可用性群組接聽程式名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @original_publisher = ] 'original_publisher'` 執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當初發行資料庫。 *original_publisher*已**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 發行的資料庫名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @redirected_publisher = ] 'redirected_publisher'` 可用性群組將成為新的發行者相關聯可用性群組接聽程式名稱。 *redirected_publisher*已**sysname**，沒有預設值。 當可用性群組接聽程式設定為非預設的通訊埠時，請連同接聽程式名稱一起指定通訊埠編號，例如 `'Listenername,51433'`  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_redirect_publisher**用來允許將複寫發行者重新導向至目前的主要複本的 Alwayson 可用性群組所關聯的可用性群組接聽程式的發行者/資料庫配對。 執行**sp_redirect_publisher** AG 接聽程式設定為包含已發行的資料庫的可用性群組之後。  
  
 如果移除原始發行者的發行集資料庫從可用性群組主要複本上，執行**sp_redirect_publisher**而不指定值 *@redirected_publisher* 若要移除發行者/資料庫配對的重新導向的參數。 如需有關重新導向和發行者，請參閱 <<c0> [ 維護 AlwaysOn 發行集資料庫&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)。</c0>  
  
## <a name="permissions"></a>Permissions  
 呼叫端必須是隸屬**sysadmin**固定伺服器角色**db_owner**散發資料庫或定義的發行集的發行集存取清單成員的固定的資料庫角色發行者資料庫相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
