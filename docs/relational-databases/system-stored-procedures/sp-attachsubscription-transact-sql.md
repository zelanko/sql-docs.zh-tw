---
title: sp_attachsubscription （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a1017c3332ca4e399984c01c68585d96aad86666
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716184"
---
# <a name="sp_attachsubscription-transact-sql"></a>sp_attachsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/applies-to-version/sql-asdb.md)]

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
`[ @dbname = ] 'dbname'`這是依名稱指定目的地訂閱資料庫的字串。 *dbname*是**sysname**，沒有預設值。  
  
`[ @filename = ] 'filename'`這是主要 MDF （**master** data file）的名稱和實體位置。 *filename*是**Nvarchar （260）**，沒有預設值。  
  
`[ @subscriber_security_mode = ] 'subscriber_security_mode'`這是在同步處理時，連接到訂閱者時，所要使用之訂閱者的安全性模式。 *subscriber_security_mode*是**int**，預設值是 Null。  
  
> [!NOTE]  
>  必須使用 Windows 驗證。 如果*subscriber_security_mode*不是**1** （Windows 驗證），則會傳回錯誤。  
  
`[ @subscriber_login = ] 'subscriber_login'`這是進行同步處理時，連接到訂閱者時所要使用的訂閱者登入名稱。 *subscriber_login*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果*subscriber_security_mode*不是**1** ，且指定*subscriber_login* ，則會傳回錯誤。  
  
`[ @subscriber_password = ] 'subscriber_password'`這是訂閱者密碼。 *subscriber_password*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  這個參數已被取代，維護它的目的，只是為了與舊版的指令碼相容。 如果*subscriber_security_mode*不是**1** ，且指定*subscriber_password* ，則會傳回錯誤。  
  
`[ @distributor_security_mode = ] distributor_security_mode`這是在同步處理時，連接到散發者時所要使用的安全性模式。 *distributor_security_mode*是**int**，預設值是**0**。 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 **1**指定 Windows 驗證。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`這是在同步處理時，用來連接到散發者的散發者登入。 如果*distributor_security_mode*設定為**0**，則需要*distributor_login* 。 *distributor_login*是**sysname**，預設值是 Null。  
  
`[ @distributor_password = ] 'distributor_password'`這是散發者密碼。 如果*distributor_security_mode*設定為**0**，則需要*distributor_password* 。 *distributor_password*是**sysname**，預設值是 Null。 *Distributor_password*的值必須小於120的 Unicode 字元。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_security_mode = ] publisher_security_mode`這是在同步處理時，連接到發行者時所使用的安全性模式。 *publisher_security_mode*是**int**，預設值是**1**。 如果為**0**，則指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 如果是**1**，則指定 Windows 驗證。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`這是在同步處理時，用來連接到發行者的登入。 *publisher_login*是**sysname**，預設值是 Null。  
  
`[ @publisher_password = ] 'publisher_password'`這是連接到發行者時所使用的密碼。 *publisher_password*是**sysname**，預設值是 Null。 *Publisher_password*的值必須小於120的 Unicode 字元。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @job_login = ] 'job_login'`這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**Nvarchar （257）**，沒有預設值。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'`這是執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。 *Job_password*的值必須小於120的 Unicode 字元。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @db_master_key_password = ] 'db_master_key_password'`這是使用者定義資料庫主要金鑰的密碼。 *db_master_key_password*是**Nvarchar （524）**，預設值是 Null。 如果未指定*db_master_key_password* ，將會卸載並重新建立現有的資料庫主要金鑰。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_attachsubscription**用於快照式複寫、異動複寫和合併式複寫中。  
  
 如果發行集保留期限已過期，訂閱就無法附加至發行集。 如果指定含有經過保留期限的訂閱，當附加訂閱或第一次同步處理訂閱時，會發生錯誤。 發行集保留期限為**0** （永不過期）的發行集會被忽略。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_attachsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
