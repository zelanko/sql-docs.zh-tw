---
title: sp_attachsubscription & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_attachsubscription
- sp_attachsubscription_TSQL
helpviewer_keywords:
- sp_attachsubscription
ms.assetid: b9bbda36-a46a-4327-a01e-9cd632e4791b
author: stevestein
ms.author: sstein
ms.openlocfilehash: d9f144d9d896fb75af5f59850c249b9044d1b781
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046155"
---
# <a name="spattachsubscription-transact-sql"></a>sp_attachsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將現有的訂閱資料庫附加至任何訂閱者。 這個預存程序執行於 master 資料庫的新訂閱者端。  
  
> [!IMPORTANT]  
>  這項功能已被取代，未來的版本將會移除它。 這項功能不應該使用在新的開發工作中。 對於使用參數化篩選來進行資料分割的合併式發行集，我們建議您使用資料分割快照集的新功能，這些功能可以簡化大量訂閱的初始化。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。 對於未進行資料分割的發行集，您可以用備份來初始化訂閱。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_attachsubscription [ @dbname = ] 'dbname'  
        , [ @filename = ] 'filename'  
    [ , [ @subscriber_security_mode = ] 'subscriber_security_mode' ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @db_master_key_password = ] 'db_master_key_password' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] 'dbname'` 是依名稱指定目的地訂閱資料庫的字串。 *dbname*已**sysname**，沒有預設值。  
  
`[ @filename = ] 'filename'` 是主要 mdf 的實體位置與名稱 (**主要**資料檔案)。 *檔名*已**nvarchar(260)** ，沒有預設值。  
  
`[ @subscriber_security_mode = ] 'subscriber_security_mode'` 是要同步處理時，連接到訂閱者時使用的訂閱者的安全性模式。 *subscriber_security_mode*已**int**，預設值是 NULL。  
  
> [!NOTE]  
>  必須使用 Windows 驗證。 如果*subscriber_security_mode*不是**1** （Windows 驗證），則會傳回錯誤。  
  
`[ @subscriber_login = ] 'subscriber_login'` 是同步處理時，連接到訂閱者時要使用的訂閱者登入名稱。 *subscriber_login*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果*subscriber_security_mode*不是**1**並*subscriber_login*已指定，則會傳回錯誤。  
  
`[ @subscriber_password = ] 'subscriber_password'` 這是訂閱者密碼。 *subscriber_password*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果*subscriber_security_mode*不是**1**並*subscriber_password*已指定，則會傳回錯誤。  
  
`[ @distributor_security_mode = ] distributor_security_mode` 是，連接到散發者時同步處理時所要使用的安全性模式。 *distributor_security_mode*已**int**，預設值是**0**。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 **1**指定 Windows 驗證。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'` 是，連接到散發者時同步處理時所要使用的散發者登入。 *distributor_login* ，便須*distributor_security_mode*設定為**0**。 *distributor_login*已**sysname**，預設值是 NULL。  
  
`[ @distributor_password = ] 'distributor_password'` 這是散發者密碼。 *distributor_password* ，便須*distributor_security_mode*設定為**0**。 *distributor_password*已**sysname**，預設值是 NULL。 值*distributor_password*必須小於 120 個 Unicode 字元。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 是同步處理時，連接到發行者時所要使用的安全性模式。 *publisher_security_mode*已**int**，預設值是**1**。 如果**0**，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 如果**1**，指定 Windows 驗證。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` 是同步處理時，連接到發行者時所要使用的登入。 *publisher_login*已**sysname**，預設值是 NULL。  
  
`[ @publisher_password = ] 'publisher_password'` 這是連接到 「 發行者 」 時用的密碼。 *publisher_password*已**sysname**，預設值是 NULL。 值*publisher_password*必須小於 120 個 Unicode 字元。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @job_login = ] 'job_login'` 是執行代理程式的 Windows 帳戶的登入。 *job_login*已**nvarchar(257)** ，沒有預設值。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'` 這是代理程式所執行的 Windows 帳戶的密碼。 *job_password*已**sysname**，沒有預設值。 值*job_password*必須小於 120 個 Unicode 字元。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @db_master_key_password = ] 'db_master_key_password'` 這是密碼的使用者定義資料庫主要金鑰。 *db_master_key_password*已**nvarchar(524)** ，預設值是 NULL。 如果*db_master_key_password*未指定，將卸除並重新建立現有的資料庫主要金鑰。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_attachsubscription**用於快照式複寫、 異動複寫和合併式複寫。  
  
 如果發行集保留期限已過期，訂閱就無法附加至發行集。 如果指定含有經過保留期限的訂閱，當附加訂閱或第一次同步處理訂閱時，會發生錯誤。 發行集的發行集保留期限**0** （永不過期） 會被忽略。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_attachsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
