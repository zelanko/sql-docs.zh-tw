---
title: sp_helppublication_snapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c82b95cd68ec451129d0611b55d1366ab823ad47
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703526"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回給定發行集之快照集代理程式的相關資訊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication =** ] **'***publication***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@publisher =** ] **'***發行者***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應加入至發行項時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|快照集代理程式的識別碼。|  
|**name**|**nvarchar(100)**|快照集代理程式的名稱。|  
|**publisher_security_mode**|**smallint**|這是連接到發行者時，代理程式所用的安全性模式，它可以是下列項目之一：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1** = Windows 驗證。|  
|**publisher_login**|**sysname**|當連接到發行者時所用的登入。|  
|**publisher_password**|**nvarchar(524)**|基於安全性理由，值為**\* \* \* \* \* \* \* \* \* \*** 一律為傳回此項目。|  
|**job_id**|**uniqueidentifier**|代理程式作業的唯一識別碼。|  
|**job_login**|**nvarchar(512)**|是 Windows 帳戶的快照集代理程式執行，這傳回的格式如下*網域*\\*username*。|  
|**job_password**|**sysname**|基於安全性理由，值為**\* \* \* \* \* \* \* \* \* \*** 一律為傳回此項目。|  
|**schedule_name**|**sysname**|這個代理程式作業所用的排程名稱。|  
|**frequency_type**|**int**|這是排程執行代理程式的頻率，它可以是下列值之一。<br /><br /> **1** = 一次<br /><br /> **2** = 視<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月相對<br /><br /> **64** = 自動啟動<br /><br /> **128** = 重複執行|  
|**frequency_interval**|**int**|代理程式執行的天數，它可以是下列值之一。<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 日<br /><br /> **9** = 工作日<br /><br /> **10** = 週末|  
|**frequency_subday_type**|**int**|會定義代理程式執行頻率時的型別*frequency_type*是**4** （每天），而且可以是下列值之一。<br /><br /> **1** = 在指定的時間<br /><br /> **2** = 秒數<br /><br /> **4** = 分鐘<br /><br /> **8** = 小時|  
|**frequency_subday_interval**|**int**|間隔的數目*frequency_subday_type*代理程式的各排程執行之間發生。|  
|**frequency_relative_interval**|**int**|代理程式執行的當月週時*frequency_type*是**32** （每月相對），而且可以是下列值之一。<br /><br /> **1** = 第一個<br /><br /> **2** = 第二個<br /><br /> **4** = 第三個<br /><br /> **8** = 第四個<br /><br /> **16** = 最後一個|  
|**frequency_recurrence_factor**|**int**|排程執行代理程式的間隔週數或月數。|  
|**active_start_date**|**int**|這是第一次排程執行代理程式的日期，格式為 YYYYMMDD。|  
|**active_end_date**|**int**|這是最後一次排程執行代理程式的日期，格式為 YYYYMMDD。|  
|**active_start_time**|**int**|這是第一次排程執行代理程式的時間，格式為 HHMMSS。|  
|**active_end_time**|**int**|這是最後一次排程執行代理程式的時間，格式為 HHMMSS。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_help_publication_snapshot**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色，在發行者端的成員**db_owner**發行集資料庫的固定的資料庫角色可以執行**sp_help_publication_snapshot**.  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
