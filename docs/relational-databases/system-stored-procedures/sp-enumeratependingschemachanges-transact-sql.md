---
title: sp_enumeratependingschemachanges （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: stevestein
ms.author: sstein
ms.openlocfilehash: da5579c52d1ffe1400e3b4c8c01210ca5856597b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124584"
---
# <a name="sp_enumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回所有暫止結構描述變更的清單。 這個預存程式可以與[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)搭配使用，讓系統管理員略過選取的暫止架構變更，使其不會被覆寫。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @starting_schemaversion = ] starting_schemaversion`這是要包含在結果集中的最小數位架構變更。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|套用至整個發行集的架構變更之發行項的名稱，或是適用于整篇發行集之架構變更的**全發佈**。|  
|**schemaversion**|**int**|暫止結構描述變更的編號。|  
|**schematype**|**sysname**|代表結構描述變更類型的文字值。|  
|**schematext**|**nvarchar(max)**|描述結構描述變更的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。|  
|**schemastatus**|**Nvarchar （10）**|指出發行項的結構描述變更是否暫止，它可以是下列值之一：<br /><br /> **active** = 架構變更暫止<br /><br /> **非**使用中 = 架構變更非使用中<br /><br /> **skip** = 不復寫架構變更|  
|**schemaguid**|**uniqueidentifier**|識別結構描述變更。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_enumeratependingschemachanges**用於合併式複寫中。  
  
 搭配[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)使用的**sp_enumeratependingschemachanges**適用于合併式複寫的可支援性，而且只有在其他更正動作（如重新初始化）無法更正狀況時，才應使用。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_enumeratependingschemachanges**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
