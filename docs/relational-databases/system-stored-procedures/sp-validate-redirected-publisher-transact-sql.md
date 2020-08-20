---
description: sp_validate_redirected_publisher (Transact-SQL)
title: sp_validate_redirected_publisher (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 158f49e40b60b528fa0a243a66fb3a5d29c7b6b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473450"
---
# <a name="sp_validate_redirected_publisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  請確認發行之資料庫的目前主機是否能夠支援複寫。 必須從散發資料庫執行。 **Sp_get_redirected_publisher**會呼叫這個程式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>引數  
`[ @original_publisher = ] 'original_publisher'` 最初發行資料庫的實例名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *original_publisher* 是 **sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 要發行之資料庫的名稱。 *publisher_db* 是 **sysname**，沒有預設值。  
  
`[ @redirected_publisher = ] 'redirected_publisher'` 針對發行者/資料庫配對呼叫 **sp_redirect_publisher** 時，所指定的重新導向目標。 *redirected_publisher* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 如果發行者和發行資料庫沒有專案存在， **sp_validate_redirected_publisher**在輸出參數* \@ redirected_publisher*中傳回 null。 如果有項目存在，則成功和失敗案例的輸出參數中都會傳回此項目。  
  
 如果驗證成功， **sp_validate_redirected_publisher** 會傳回成功指示。  
  
 如果驗證失敗，則會引發描述失敗的錯誤。  
  
## <a name="permissions"></a>權限  
 呼叫端必須是 **系統管理員（sysadmin** ）固定伺服器角色的成員、散發資料庫的 **db_owner** 固定資料庫角色，或是與發行者資料庫相關聯之定義發行集的發行集存取清單的成員。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的複寫預存程式 ](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
