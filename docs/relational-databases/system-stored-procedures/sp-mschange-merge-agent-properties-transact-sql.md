---
description: sp_MSchange_merge_agent_properties (Transact-SQL)
title: sp_MSchange_merge_agent_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_merge_agent_properties_TSQL
- sp_MSchange_merge_agent_properties
helpviewer_keywords:
- sp_MSchange_merge_agent_properties
ms.assetid: f775fa0f-28c7-4863-89ce-7bcfa1ab8b5e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7e81812af12cf7789c48d890ced2aa06a5829ad0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446912"
---
# <a name="sp_mschange_merge_agent_properties-transact-sql"></a>sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 或更新版本散發者端執行合併代理程式作業的屬性 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 當發行者執行於 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的執行個體時，系統會利用這個預存程序來變更屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行集資料庫的名稱。 *publisher_db* 是 **sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'` 這是訂閱者的名稱。 *訂閱者* 是 **sysname**，沒有預設值。  
  
`[ @subscriber_db = ] 'subscriber_db'` 這是訂閱資料庫的名稱。 *subscriber_db* 是 **sysname**，沒有預設值。  
  
`[ @property = ] 'property'` 這是要變更的發行集屬性。 *屬性* 是 **sysname**，沒有預設值。  
  
`[ @value = ] 'value'` 這是新的屬性值。 *值* 是 **Nvarchar (524) **，預設值是 Null。  
  
 下表描述可變更的合併代理程式作業屬性及這些屬性值的限制。  
  
|屬性|值|描述|  
|--------------|-----------|-----------------|  
|**description**||訂閱的簡要描述。|  
|**merge_job_login**||用來執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的登入。|  
|**merge_job_password**||用來執行代理程式作業之 Windows 帳戶的密碼。|  
|**publisher_login**||用來連接到發行者以同步處理訂閱的登入。|  
|**publisher_password**||發行者密碼。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Windows 驗證。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
|**subscriber_login**||用來連接到訂閱者以同步處理訂閱的登入。|  
|**subscriber_password**||訂閱者密碼。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Windows 驗證。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。|  
  
> [!NOTE]  
>  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_MSchange_merge_agent_properties** 用於合併式複寫中。  
  
 當發行者在或更新版本的實例上執行時 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，您應該使用 [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) 來變更合併代理程式作業的屬性，該作業會同步處理在散發者端執行的發送訂閱。  
  
## <a name="permissions"></a>權限  
 只有散發者端的 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_MSchange_merge_agent_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergepushsubscription_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
