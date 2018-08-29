---
title: sp_helplogreader_agent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helplogreader_agent
- sp_helplogreader_agent_TSQL
helpviewer_keywords:
- sp_helplogreader_agent
ms.assetid: ff837209-e2b3-481a-a48f-8530bfe53d97
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef9fd50728a4bc9ebf661b2dbb22ad8ca4e9f4ad
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031819"
---
# <a name="sphelplogreaderagent-transact-sql"></a>sp_helplogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回發行集資料庫的記錄讀取器代理程式作業的屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplogreader_agent [ [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher**=] **'***發行者***'**  
 這是發行者的名稱。 *發行者*已**sysname**，預設值是 NULL。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理程式的識別碼。|  
|**name**|**nvarchar(100)**|代理程式的名稱。|  
|**publisher_security_mode**|**smallint**|這是連接到發行者時，代理程式所用的安全性模式，它可以是下列項目之一：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證。|  
|**publisher_login**|**sysname**|當連接到發行者時所用的登入。|  
|**publisher_password**|**nvarchar(524)**|基於安全性理由，值為**\* \* \* \* \* \* \* \* \* \*** 一律為傳回此項目。|  
|**job_id**|**uniqueidentifier**|代理程式作業的唯一識別碼。|  
|**job_login**|**nvarchar(512)**|是 Windows 帳戶 「 記錄讀取器代理程式執行，這傳回的格式如下*網域*\\*username*。|  
|**job_password**|**sysname**|基於安全性理由，值為**\* \* \* \* \* \* \* \* \* \*** 一律為傳回此項目。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helplogreader_agent**用於異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色，在發行者端的成員**db_owner**發行集資料庫的固定的資料庫角色可以執行**sp_helplogreader_agent**.  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addlogreader_agent &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)   
 [sp_changelogreader_agent &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)  
  
  
