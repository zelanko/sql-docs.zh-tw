---
title: "sp_helpqreader_agent (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
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
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50492a76e742459e7b883f9887026d0ce63d1eb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpqreaderagent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回佇列讀取器代理程式的屬性。 這個預存程序執行於散發資料庫的散發者端，或是執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@frompublisher=** ] *frompublisher*  
 指定預存程序是在發行者端或散發者端呼叫。 *frompublisher* bit，預設值為 0。 **1**表示預存程序從發行者呼叫和**0**表示預存程序從散發者端呼叫。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理程式的識別碼。|  
|**name**|**nvarchar （100)**|代理程式的名稱。|  
|**job_id**|**uniqueidentifier**|代理程式作業的唯一識別碼。|  
|**job_login**|**nvarchar(512)**|Windows 帳戶的散發代理程式執行，這傳回的格式如下*網域*\\*username*。|  
|**job_password**|**sysname**|基於安全性理由，值為 **\* \* \* \* \* \* \* \* \* \*** 一律是傳回。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpqreader_agent**用於異動複寫中。  
  
## <a name="permissions"></a>Permissions  
 當值*frompublisher*是**1**，只有的成員**sysadmin** 「 發行者 」 或成員的固定的伺服器角色**db_owner**發行集資料庫上的固定的資料庫角色可以執行**sp_helpqreader_agent**。 否則，只有**sysadmin**固定的伺服器角色的成員的散發者**db_owner**散發資料庫上的固定的資料庫角色可以執行**sp_helpqreader_代理程式**。  
  
## <a name="see-also"></a>請參閱＜  
 [啟用交易式發行集的更新訂閱](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
