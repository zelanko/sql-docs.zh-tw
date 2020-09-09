---
description: sp_changelogreader_agent (Transact-SQL)
title: sp_changelogreader_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changelogreader_agent
- sp_changelogreader_agent_TSQL
helpviewer_keywords:
- sp_changelogreader_agent
ms.assetid: 929b2fa7-1267-41d0-8b69-e9ab26a62c0f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b7be6bc9fb6d52508677d75448b429726be005b8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89528493"
---
# <a name="sp_changelogreader_agent-transact-sql"></a>sp_changelogreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  變更記錄讀取器代理程式的安全性屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!IMPORTANT]  
>  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changelogreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @job_login = ] 'job_login'` 這是用來執行代理程式之帳戶的登入。 *job_login* 是 **Nvarchar (257) **，預設值是 Null。 在 Azure SQL 受控執行個體上，請使用 SQL Server 帳戶。 *無法變更為非* [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*發行者。*  
  
`[ @job_password = ] 'job_password'` 這是用來執行代理程式之帳戶的密碼。 *job_password* 是 **sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 這是連接到發行者時，代理程式所使用的安全性模式。 *publisher_security_mode* 是 **Smallint**，預設值是 Null。 **0** 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證， **1** 指定 Windows 驗證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` 這是連接到發行者時所用的登入。 *publisher_login* 是 **sysname**，預設值是 Null。 當*publisher_security_mode*為**0**時，必須指定*publisher_login* 。 如果 *publisher_login* 為 Null，而 *publisher_security_mode* 為 **1**，則在連接到發行者時，會使用 *job_login* 中指定的 Windows 帳戶。  
  
`[ @publisher_password = ] 'publisher_password'` 這是連接到發行者時所使用的密碼。 *publisher_password* 是 **sysname**，預設值是 Null。  
  
> [!IMPORTANT]  
>  請勿使用空白密碼。 請使用增強式密碼。 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。 只支援非 SQL Server 發行者使用這個參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_changelogreader_agent** 用於異動複寫中。  
  
 **sp_changelogreader_agent** 用來變更記錄讀取器代理程式執行時所使用的 Windows 帳戶。 您可以變更現有 Windows 登入的密碼，或者提供新的 Windows 登入和密碼。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_changelogreader_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_helplogreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)   
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
