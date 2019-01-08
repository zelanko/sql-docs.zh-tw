---
title: sp_addlogreader_agent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords:
- sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6fdec3ada9bec27f6ecca2ea6a888d01640f6edb
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210837"
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  加入給定資料庫的記錄讀取器代理程式。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@job_login**=] **'**_job_login_**'**  
 這是用來執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的登入。 *job_login*已**nvarchar(257)**，預設值是 NULL。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。  
  
> [!NOTE]
>  針對非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者，這必須是指定的相同登入[sp_adddistpublisher &#40;-&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。  
  
 [ **@job_password**=] **'**_job_password_**'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
 [ **@job_name**=] **'**_job_name_**'**  
 這是現有散發代理程式作業的名稱。 *job_name*已**sysname**，預設值是 NULL。 只有在利用現有的作業來啟動代理程式，而不用新建立的作業 (預設值) 時，才指定這個參數。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 這是當連接到發行者時使用的安全性模式。 *publisher_security_mode*已**smallint**，預設值是**1**。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，並**1**指定 Windows 驗證。 值為**0**您必須指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 [ **@publisher_login**=] **'**_publisher_login_**'**  
 這是連接到發行者時所用的登入。 *publisher_login*已**sysname**，預設值是 NULL。 *publisher_login*時，必須指定*publisher_security_mode*是**0**。 如果*publisher_login*為 NULL 並*publisher_security_mode*是**1**，在指定的 Windows 帳戶*job_login*將使用當連接到發行者。  
  
 [ **@publisher_password**=] **'**_publisher_password_**'**  
 這是連接到發行者時所用的密碼。 *publisher_password*已**sysname**，預設值是 NULL。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
 [ **@publisher**=] **'**_發行者_**'**  
 名稱非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  您不應該將這個參數指定給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addlogreader_agent**用於異動複寫中。  
  
 您必須執行**sp_addlogreader_agent**以加入記錄讀取器代理程式，如果您已升級的資料庫，啟用以供複寫到此版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用這個資料庫建立發行集之前。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_addlogreader_agent**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40;-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
