---
title: sp_addlogreader_agent （Transact-sql） |Microsoft Docs
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
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4b22bb48cd5bc48a3b1812dfd97fc2b56df8ba11
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757979"
---
# <a name="sp_addlogreader_agent-transact-sql"></a>sp_addlogreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @job_login = ] 'job_login'`[!INCLUDE[msCoName](../../includes/msconame-md.md)]這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**Nvarchar （257）**，預設值是 Null。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。  
  
> [!NOTE]
>  若為非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者，這必須是[sp_adddistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)中指定的相同登入。  
  
`[ @job_password = ] 'job_password'`這是執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
`[ @job_name = ] 'job_name'`這是現有代理程式作業的名稱。 *job_name*是**sysname**，預設值是 Null。 只有在利用現有的作業來啟動代理程式，而不用新建立的作業 (預設值) 時，才指定這個參數。  
  
`[ @publisher_security_mode = ] publisher_security_mode`這是連接到發行者時，代理程式所使用的安全性模式。 *publisher_security_mode*是**Smallint**，預設值是**1**。 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證， **1**指定 Windows 驗證。 非發行者必須指定**0**的值 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @publisher_login = ] 'publisher_login'`這是連接到發行者時所使用的登入。 *publisher_login*是**sysname**，預設值是 Null。 當*publisher_security_mode*為**0**時，必須指定*publisher_login* 。 如果*publisher_login*是 Null，而且*publisher_security_mode*是**1**，則連接到發行者時，將會使用*job_login*中指定的 Windows 帳戶。  
  
`[ @publisher_password = ] 'publisher_password'`這是連接到發行者時所使用的密碼。 *publisher_password*是**sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
`[ @publisher = ] 'publisher'`這是非發行者的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  您不應該將這個參數指定給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_addlogreader_agent**用於異動複寫中。  
  
 如果您在**sp_addlogreader_agent** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用資料庫建立發行集之前，將已啟用複寫的資料庫升級為此版本，您必須執行 Sp_addlogreader_agent 來加入記錄讀取器代理程式。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_addlogreader_agent**。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
