---
title: sp_helplogreader_agent （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4c1afca8eed465c191fccb4d24e79a7bd95af9aa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828902"
---
# <a name="sp_helplogreader_agent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回發行集資料庫的記錄讀取器代理程式作業的屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，預設值是 Null。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理程式的識別碼。|  
|**name**|**Nvarchar （100）**|代理程式的名稱。|  
|**publisher_security_mode**|**smallint**|這是連接到發行者時，代理程式所用的安全性模式，它可以是下列項目之一：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證<br /><br /> **1** = Windows 驗證。|  
|**publisher_login**|**sysname**|當連接到發行者時所用的登入。|  
|**publisher_password**|**Nvarchar （524）**|基於安全性理由， **\*\*\*\*\*\*\*\*\*\*** 一律會傳回的值。|  
|**job_id**|**uniqueidentifier**|代理程式作業的唯一識別碼。|  
|**job_login**|**nvarchar(512)**|這是用來執行記錄讀取器代理程式的 Windows 帳戶，傳回的格式為*domain* \\ *username*。|  
|**job_password**|**sysname**|基於安全性理由， **\*\*\*\*\*\*\*\*\*\*** 一律會傳回的值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helplogreader_agent**用於異動複寫中。  
  
## <a name="permissions"></a>權限  
 只有在發行者端的**系統管理員（sysadmin** ）固定伺服器角色成員，或是發行集資料庫之**db_owner**固定資料庫角色的成員，才能夠執行**sp_helplogreader_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [查看及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
