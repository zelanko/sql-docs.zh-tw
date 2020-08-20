---
description: sp_helpqreader_agent (Transact-SQL)
title: sp_helpqreader_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpqreader_agent_TSQL
- sp_helpqreader_agent
helpviewer_keywords:
- sp_helpqreader_agent
ms.assetid: 8e74e1aa-e95b-4183-8017-bf123439b08d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c638e7895d95518f59627643deb0b0070a19fa70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489280"
---
# <a name="sp_helpqreader_agent-transact-sql"></a>sp_helpqreader_agent (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回佇列讀取器代理程式的屬性。 這個預存程序執行於散發資料庫的散發者端，或是執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpqreader_agent [ [ @frompublisher = ] frompublisher ]  
```  
  
## <a name="arguments"></a>引數  
`[ @frompublisher = ] frompublisher` 指定是否在發行者端或散發者端呼叫預存程式。 *frompublisher* 是 bit，預設值是0。 **1** 表示預存程式是從發行者呼叫，而 **0** 表示預存程式是從散發者端呼叫。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|代理程式的識別碼。|  
|**name**|**Nvarchar (100) **|代理程式的名稱。|  
|**job_id**|**uniqueidentifier**|代理程式作業的唯一識別碼。|  
|**job_login**|**nvarchar(512)**|這是散發代理程式執行時所用的 Windows 帳戶，以*網域*使用者名稱的格式傳回 \\ * *。|  
|**job_password**|**sysname**|基於安全性考慮， **\*\*\*\*\*\*\*\*\*\*** 一律會傳回的值。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpqreader_agent** 用於異動複寫中。  
  
## <a name="permissions"></a>權限  
 當 *frompublisher* 的值為 **1**時，只有發行者端 **系統管理員（sysadmin** ）固定伺服器角色的成員，或是發行集資料庫之 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_helpqreader_agent**。 否則，只有散發者端之 **系統管理員（sysadmin** ）固定伺服器角色的成員，或是散發資料庫上 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_helpqreader_agent**。  
  
## <a name="see-also"></a>另請參閱  
 [啟用交易式發行集的更新訂閱](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
  
