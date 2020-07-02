---
title: sp_MSchange_logreader_agent_properties （T-sql）
description: 描述用來變更 SQL Server 複寫拓撲之記錄讀取器代理程式屬性的 sp_MSchange_logreader_agent_properties 預存程式。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 852346183f56901e1cee32e3bb8d21d0ea24beb8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786151"
---
# <a name="sp_mschange_logreader_agent_properties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  變更在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 或更新版本散發者上執行之記錄讀取器代理程式作業的屬性 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 當發行者執行於 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的執行個體時，系統會利用這個預存程序來變更屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_MSchange_logreader_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @publisher_security_mode = ] publisher_security_mode`這是連接到發行者時，代理程式所使用的安全性模式。 *publisher_security_mode*是**Smallint**，沒有預設值。  
  
 **0**指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。  
  
 **1**指定 Windows 驗證。  
  
`[ @publisher_login = ] 'publisher_login'`這是連接到發行者時所使用的登入。 *publisher_login*是**sysname**，沒有預設值。 當*publisher_security_mode*為**0**時，必須指定*publisher_login* 。 如果*publisher_login*是 Null，而且*publisher_security_mode*是**1**，則連接到發行者時，將會使用*job_login*中指定的 Windows 帳戶。  
  
`[ @publisher_password = ] 'publisher_password'`這是連接到發行者時所使用的密碼。 *publisher_password*是**sysname**，沒有預設值。  
  
`[ @job_login = ] 'job_login'`這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**Nvarchar （257）**，沒有預設值。 *這不能變更為非* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*發行者。*  
  
`[ @job_password = ] 'job_password'`這是執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
`[ @publisher_type = ] 'publisher_type'`當發行者不是在實例中執行時，指定發行者類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *publisher_type*是**sysname**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE GATEWAY**|指定 Oracle Gateway 發行者。|  
  
 如需有關「Oracle 發行者」與「Oracle 閘道發行者」之間差異的詳細資訊，請參閱[Oracle 發行總覽](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="remarks"></a>備註  
 **sp_MSchange_logreader_agent_properties**用於異動複寫中。  
  
 執行**sp_MSchange_logreader_agent_properties**時，您必須指定所有參數。 執行[sp_helplogreader_agent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) ，以傳回記錄讀取器代理程式作業的目前屬性。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
 當發行者在或更新版本的實例上執行時 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，您應該使用[sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)來變更記錄讀取器代理程式的屬性。  
  
## <a name="permissions"></a>權限  
 只有在散發者端的**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_MSchange_logreader_agent_properties**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
