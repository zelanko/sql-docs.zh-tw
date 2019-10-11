---
title: sp_validate_redirected_publisher （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: stevestein
ms.author: sstein
ms.openlocfilehash: b01fba8260e86d135e740964022187b9914e5fc0
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252057"
---
# <a name="sp_validate_redirected_publisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  請確認發行之資料庫的目前主機是否能夠支援複寫。 必須從散發資料庫執行。 這個程式是由**sp_get_redirected_publisher**所呼叫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>引數  
`[ @original_publisher = ] 'original_publisher'`：原先發行資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的實例名稱。 *original_publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 已發行的資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @redirected_publisher = ] 'redirected_publisher'` 當針對發行者/資料庫配對呼叫**sp_redirect_publisher**時，所指定的重新導向目標。 *redirected_publisher*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 如果發行者和發行資料庫沒有專案存在， **sp_validate_redirected_publisher**會在輸出參數 *\@redirected_publisher*中傳回 null。 如果有項目存在，則成功和失敗案例的輸出參數中都會傳回此項目。  
  
 如果驗證成功， **sp_validate_redirected_publisher**會傳回成功指示。  
  
 如果驗證失敗，則會引發描述失敗的錯誤。  
  
## <a name="permissions"></a>Permissions  
 呼叫者必須是**系統管理員（sysadmin** ）固定伺服器角色的成員、散發資料庫的**db_owner**固定資料庫角色，或是與發行者資料庫相關聯之定義發行集的發行集存取清單的成員。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
