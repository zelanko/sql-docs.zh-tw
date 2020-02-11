---
title: sp_MSchange_distribution_agent_properties （T-sql）
description: 描述用來變更 SQL Server 複寫拓撲之散發代理程式屬性的 sp_MSchange_distribution_agent_properties 預存程式。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a2e2e3c0074c3fcc53298c2556c786c9b7057db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75322256"
---
# <a name="sp_mschange_distribution_agent_properties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本散發者上執行之散發代理程式作業的屬性。 當發行者執行於 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的執行個體時，系統會利用這個預存程序來變更屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，沒有預設值。  
  
`[ @property = ] 'property'`這是要變更的發行集屬性。 *屬性*是**sysname**，沒有預設值。  
  
`[ @value = ] 'value'`這是新的屬性值。 *value*是**Nvarchar （524）**，預設值是 Null。  
  
 下表描述可變更的散發代理程式作業屬性及這些屬性值的限制。  
  
|屬性|值|描述|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||用來執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的登入。|  
|**distrib_job_password**||用來執行代理程式作業之 Windows 帳戶的密碼。|  
|**subscriber_catalog**||建立 OLE DB 提供者連接時所用的目錄。 *此屬性只對非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *訂閱者有效。*|  
|**subscriber_datasource**||OLE DB 提供者所了解的資料來源名稱。 *此屬性只對非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *訂閱者有效。*|  
|**subscriber_location**||OLE DB 提供者所了解的資料庫位置。 *此屬性只對非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *訂閱者有效。*|  
|**subscriber_login**||用來連接到訂閱者以同步處理訂閱的登入。|  
|**subscriber_password**||訂閱者密碼。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的 OLE DB 提供者登錄所用的唯一程式設計識別碼 (PROGID)。 *此屬性只對非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *訂閱者有效。*|  
|**subscriber_providerstring**||OLE DB 提供者特定的連接字串，用來識別資料來源。 *這個屬性僅適用於非 SQL Server 訂閱者。*|  
|**subscriber_security_mode**|**1**|Windows 驗證。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Authentication.|  
|**subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預訂|  
||**1**|ODBC 資料來源伺服器|  
||**第**|OLE DB 提供者|  
|**subscriptionstreams**||表示每個散發代理程式將數批變更並行套用在訂閱者時所能使用的連接數目。 *不支援非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *訂閱者、Oracle 發行者或對等訂閱。*|  
  
> [!NOTE]  
>  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_MSchange_distribution_agent_properties**用於快照式複寫和異動複寫中。  
  
 當「發行者」在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本的實例上執行時，您應該使用[sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)來變更同步處理「散發者」端執行之「發送訂閱」合併代理程式作業的屬性。  
  
## <a name="permissions"></a>權限  
 只有在散發者端的**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_MSchange_distribution_agent_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addpushsubscription_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
