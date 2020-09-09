---
description: sp_changeqreader_agent (Transact-SQL)
title: sp_changeqreader_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 08e7e0571cab57d50da670495af95709482899a3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543668"
---
# <a name="sp_changeqreader_agent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更佇列讀取器代理程式的安全性屬性。 這個預存程序執行於散發資料庫的散發者端，或發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>引數  
`[ @job_login = ] 'job_login'` 這是用來 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 執行代理程式之 Windows 帳戶的登入。 *job_login* 是 **Nvarchar (257) **，預設值是 Null。  
  
`[ @job_password = ] 'job_password'` 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password* 是 **sysname**，預設值是 Null。  
  
`[ @frompublisher = ] frompublisher` 這是指是否正在發行者端執行程式。 *frompublisher* 是 bit，預設值是 **0**。 **1**值表示正在從發行集資料庫的「發行者」端執行程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_changeqreader_agent** 用於異動複寫中。  
  
 **sp_changeqreader_agent** 用來變更佇列讀取器代理程式執行時所使用的 Windows 帳戶。 您可以變更現有 Windows 登入的密碼，或者提供新的 Windows 登入和密碼。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_changeqreader_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
