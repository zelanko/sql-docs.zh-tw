---
title: sp_link_publication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 17e1b051fed32e78cd18cc634b7688245ecb0972
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="splinkpublication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定在連接到發行者時，立即更新訂閱的同步處理觸發程序所用的組態和安全性資訊。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
> [!IMPORTANT]  
>  某些狀況下，此預存程序可能會失敗如果 「 訂閱者執行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 或更新版本和 「 發行者 」 執行較早版本。 如果在此情況下預存程序失敗，請將「發行者」升級為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 或更新版本。  
  
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
 [ **@publisher**=] **'***發行者***'**  
 這是要連結的發行者名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [ **@publisher_db**=] **'***publisher_db***'**  
 這是要連結的發行者資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [ **@publication**=] **'***發行集***'**  
 這是要連結的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ **@security_mode**=] *security_mode*  
 這是訂閱者連接到遠端發行者來進行立即更新時所用的安全性模式。 *security_mode*是**int**，而且可以是下列值之一。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程序中指定的登入驗證*登入*和*密碼*。<br /><br /> 注意： 在舊版的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個選項用來指定動態遠端程序呼叫 (RPC)。|  
|**1**|使用在訂閱者端進行變更之使用者的安全性內容 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證或 Windows 驗證)。<br /><br /> 注意： 此帳戶也必須存在於 「 發行者 」 具有足夠權限。 當使用 Windows 驗證時，必須支援安全性帳戶的委派。|  
|**2**|使用現有使用者定義連結的伺服器登入使用建立**sp_link_publication**。|  
  
 [ **@login**=] **'***登入***'**  
 這是登入。 *login* 是預設值為 NULL 的 **sysname**。 這個參數必須是指定何時*security_mode*是**0**。  
  
 [ **@password**=] **'***密碼***'**  
 這是密碼。 *密碼*是**sysname**，預設值是 NULL。 這個參數必須是指定何時*security_mode*是**0**。  
  
 [  **@distributor=** ] **'***散發者***'**  
 這是散發者的名稱。 *散發者*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_link_publication**是立即更新訂閱使用的異動複寫中。  
  
 **sp_link_publication**可以用於發送和提取訂閱。 您可以在建立訂閱之前或之後呼叫它。 項目會插入或更新[MSsubscription_properties &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)系統資料表。  
  
 對於發送訂閱，清除項目可以是由[sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)。 對於提取訂閱，清除項目可以是由[sp_droppullsubscription &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)或[sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)。 您也可以呼叫**sp_link_publication**具有 NULL 密碼，可以清除中的項目[MSsubscription_properties &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)系統資料表的安全性考量。  
  
 立即更新訂閱者連接到發行者時所用的預設模式，不允許連接使用 Windows 驗證。 若要利用 Windows 驗證模式來連接，則必須設定發行者的連結伺服器，當更新訂閱者時，立即更新訂閱者應該使用這個連接。 這需要**sp_link_publication**以執行*security_mode* = **2**。 當使用 Windows 驗證時，必須支援安全性帳戶的委派。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_link_publication**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_droppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
