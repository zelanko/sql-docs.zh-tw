---
description: sp_link_publication (Transact-SQL)
title: sp_link_publication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b80c28d86ae4d7022ad8784adfa7ab9023e3ebd0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543217"
---
# <a name="sp_link_publication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  設定在連接到發行者時，立即更新訂閱的同步處理觸發程序所用的組態和安全性資訊。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
> [!IMPORTANT]
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
> 
> [!IMPORTANT]
>  在某些情況下，如果訂閱者執行的是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 或更新版本，而發行者正在執行較舊的版本，此預存程式可能會失敗。 如果在此情況下預存程序失敗，請將「發行者」升級為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 或更新版本。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是要連結的發行者名稱。 *publisher* 是 **sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 這是要連結的發行者資料庫名稱。 *publisher_db* 是 **sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 這是要連結的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @security_mode = ] security_mode` 這是訂閱者用來連接到遠端發行者以進行立即更新的安全性模式。 *security_mode* 是 **int**，而且可以是下列值之一。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|值|描述|  
|-----------|-----------------|  
|**0**|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 這個預存程式中指定的登入做為 *登* 入和 *密碼*的驗證。<br /><br /> 注意：在舊版中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，此選項是用來指定 (RPC) 的動態遠端程序呼叫。|  
|**1**|使用在訂閱者端進行變更之使用者的安全性內容 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證或 Windows 驗證)。<br /><br /> 注意：這個帳戶也必須存在於發行者端，且具有足夠的許可權。 當使用 Windows 驗證時，必須支援安全性帳戶的委派。|  
|**2**|使用以 **sp_link_publication**建立的現有使用者定義連結伺服器登入。|  
  
`[ @login = ] 'login'` 這是登入。 *login* 是預設值為 NULL 的 **sysname**。 當 *security_mode* 為 **0**時，必須指定這個參數。  
  
`[ @password = ] 'password'` 這是密碼。 *password* 是 **sysname**，預設值是 Null。 當 *security_mode* 為 **0**時，必須指定這個參數。  
  
`[ @distributor = ] 'distributor'` 這是散發者的名稱。 散發者是**sysname**，預設*值是 Null* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_link_publication** 是由異動複寫中的立即更新訂閱使用。  
  
 **sp_link_publication** 可用於推播和提取訂閱。 您可以在建立訂閱之前或之後呼叫它。 [MSsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)系統資料表中插入或更新專案。  
  
 針對發送訂閱， [sp_subscription_cleanup &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)可以清除專案。 針對提取訂閱， [sp_droppullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) 或 [sp_subscription_cleanup &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)可以清除專案。 您也可以使用 Null 密碼來呼叫 **sp_link_publication** ，以清除 [MSsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) 系統資料表中的專案，以瞭解安全性問題。  
  
 立即更新訂閱者連接到發行者時所用的預設模式，不允許連接使用 Windows 驗證。 若要利用 Windows 驗證模式來連接，則必須設定發行者的連結伺服器，當更新訂閱者時，立即更新訂閱者應該使用這個連接。 這需要使用**sp_link_publication** *security_mode*  =  **2**來執行 sp_link_publication。 當使用 Windows 驗證時，必須支援安全性帳戶的委派。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_link_publication**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_droppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
