---
title: sp_validate_redirected_publisher (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: dc600aeabd1c988c0f9a6768da7fd0f0d280552b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119421"
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  請確認發行之資料庫的目前主機是否能夠支援複寫。 必須從散發資料庫執行。 此程序會呼叫**sp_get_redirected_publisher**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>引數  
`[ @original_publisher = ] 'original_publisher'` 執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當初發行資料庫。 *original_publisher*已**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 發行的資料庫名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @redirected_publisher = ] 'redirected_publisher'` 重新導向的目標時指定**sp_redirect_publisher**針對發行者/資料庫配對呼叫。 *redirected_publisher*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 如果 「 發行者 」 和發行的資料庫，項目不存在**sp_validate_redirected_publisher**會傳回輸出參數中的 null *@redirected_publisher* 。 如果有項目存在，則成功和失敗案例的輸出參數中都會傳回此項目。  
  
 如果驗證成功， **sp_validate_redirected_publisher**傳回成功指示。  
  
 如果驗證失敗，則會引發描述失敗的錯誤。  
  
## <a name="permissions"></a>Permissions  
 呼叫端必須是隸屬**sysadmin**固定伺服器角色**db_owner**散發資料庫或定義的發行集的發行集存取清單成員的固定的資料庫角色發行者資料庫相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
