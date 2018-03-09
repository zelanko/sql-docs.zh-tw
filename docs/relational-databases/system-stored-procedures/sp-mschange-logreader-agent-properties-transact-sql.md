---
title: "sp_MSchange_logreader_agent_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea342cad83b587382ca9e25141facd613263a20e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangelogreaderagentproperties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更會在執行記錄讀取器代理程式作業的屬性[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本散發者。 當發行者執行於 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 的執行個體時，系統會利用這個預存程序來變更屬性。 這個預存程序執行於散發資料庫的散發者端。  
  
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
 [  **@publisher**  =] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [  **@publisher_security_mode** =] *publisher_security_mode*  
 這是當連接到發行者時使用的安全性模式。 *publisher_security_mode*是**smallint**，沒有預設值。  
  
 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。  
  
 **1**指定 Windows 驗證。  
  
 [  **@publisher_login** =] **'***publisher_login***'**  
 這是連接到發行者時所用的登入。 *publisher_login*是**sysname**，沒有預設值。 *publisher_login*時，必須指定*publisher_security_mode*是**0**。 如果*publisher_login*是 NULL 和*publisher_security_mode*是**1**，則在指定的 Windows 帳戶*job_login*將使用當連接到發行者。  
  
 [  **@publisher_password** =] **'***publisher_password***'**  
 這是連接到發行者時所用的密碼。 *publisher_password*是**sysname**，沒有預設值。  
  
 [  **@job_login** =] **'***job_login***'**  
 這是用來執行代理程式之 Windows 帳戶的登入。 *job_login*是**nvarchar （257)**，沒有預設值。 *無法變更非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *發行者。*  
  
 [  **@job_password** =] **'***job_password***'**  
 這是用來執行代理程式之 Windows 帳戶的密碼。 *job_password*是**sysname**，沒有預設值。  
  
 [  **@publisher_type** =] **'***publisher_type***'**  
 指定當發行者不是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中執行時的發行者類型。 *publisher_type*是**sysname**，而且可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。|  
|**ORACLE**|指定標準 Oracle 發行者。|  
|**ORACLE GATEWAY**|指定 Oracle Gateway 發行者。|  
  
 如需有關 Oracle 發行者和 Oracle Gateway 發行者之間的差異的詳細資訊，請參閱[Oracle 發行概觀](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="remarks"></a>備註  
 **sp_MSchange_logreader_agent_properties**用於異動複寫中。  
  
 執行時，您必須指定所有參數**sp_MSchange_logreader_agent_properties**。 執行[sp_helplogreader_agent &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)傳回記錄讀取器代理程式作業的目前屬性。  
  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
 當發行者執行個體上執行時[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本時，您應該使用[sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)變更記錄讀取器代理程式的屬性。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**散發者端的固定的伺服器角色可以執行**sp_MSchange_logreader_agent_properties**。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
