---
title: sp_changeqreader_agent (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21da0ca61d2d9075fe7c962156443fd85f3ebefd
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135121"
---
# <a name="spchangeqreaderagent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更佇列讀取器代理程式的安全性屬性。 這個預存程序執行於散發資料庫的散發者端，或發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>引數  
 [ **@job_login**=] **'**_job_login_**'**  
 這是用來執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的登入。 *job_login*已**nvarchar(257)**，預設值是 NULL。  
  
 [ **@job_password**=] **'**_job_password_**'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*已**sysname**，預設值是 NULL。  
  
 [  **@frompublisher=** ] *frompublisher*  
 指出程序是否正在發行者端執行。 *frompublisher* bit，預設值是**0**。 值為**1**表示，從發行集資料庫的發行者上執行此程序。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changeqreader_agent**用於異動複寫中。  
  
 **sp_changeqreader_agent**用來變更執行佇列讀取器代理程式 」 的 Windows 帳戶。 您可以變更現有 Windows 登入的密碼，或者提供新的 Windows 登入和密碼。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_changeqreader_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
