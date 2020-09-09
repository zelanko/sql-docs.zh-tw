---
description: sp_addqreader_agent (Transact-SQL)
title: sp_addqreader_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addqreader_agent_TSQL
- sp_addqreader_agent
helpviewer_keywords:
- sp_addqreader_agent
ms.assetid: dc9f591a-e67e-4ba8-bf47-defd5eda0822
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dae183ab0f04ac343e7836b852a881341f188325
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549952"
---
# <a name="sp_addqreader_agent-transact-sql"></a>sp_addqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  加入給定散發者的佇列讀取器代理程式。 這個預存程序執行於散發資料庫的散發者端，或發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addqreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name'  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>引數  
`[ @job_login = ] 'job_login'` 這是用來 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 執行代理程式之 Windows 帳戶的登入。 *job_login* 是 **Nvarchar (257) **，沒有預設值。 通往散發者的代理程式連接一律使用這個 Windows 帳戶。  
  
`[ @job_password = ] 'job_password'` 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password* 是 **sysname**，沒有預設值。  
  
> [!IMPORTANT]  
>  請勿將驗證資訊儲存在指令碼檔案中。 為了要有最佳的安全性，登入名稱和密碼應該在執行階段提供。  
  
`[ @job_name = ] 'job_name'` 這是現有代理程式作業的名稱。 *job_name* 是 **sysname**，預設值是 Null。 只有在利用現有的作業來建立代理程式，而不用新建立的作業 (預設值) 時，才指定這個參數。  
  
`[ @frompublisher = ] frompublisher` 指定程式是否正在發行者端執行。 *frompublisher* 是 bit，預設值是 **0**。 **1**值表示正在從發行集資料庫的「發行者」端執行程式。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_addqreader_agent** 用於異動複寫中。  
  
 在[sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)之後但[sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)之前，至少必須在支援佇列更新的散發者上執行一次**sp_addqreader_agent** 。  
  
 當您執行 [sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)時，佇列讀取器代理程式作業會被移除。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_addqreader_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [針對交易式發行集啟用更新訂閱](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [升級複寫指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_changeqreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)   
 [sp_helpqreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)  
  
  
