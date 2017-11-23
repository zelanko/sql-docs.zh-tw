---
title: "sp_helpsubscriberinfo (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriberinfo
- sp_helpsubscriberinfo_TSQL
helpviewer_keywords: sp_helpsubscriberinfo
ms.assetid: fbabe1ec-57cf-425c-bae7-af7f5d3198fd
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ec5df274042b35d30a251c90802c06cd4347ab1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示訂閱者的相關資訊。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@subscriber =** ] **'***訂閱者***'**  
 這是訂閱者的名稱。 *訂閱者*是**sysname**，預設值是 **%** ，它會傳回所有資訊。  
  
 [  **@publisher =** ] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，而且預設為目前伺服器的名稱。  
  
> [!NOTE]  
>  *發行者*不應指定，除非它是 「 Oracle 發行者 」。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**訂閱者**|**sysname**|訂閱者的名稱。|  
|**型別**|**tinyint**|訂閱者的類型：<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫**1** = ODBC 資料來源|  
|**登入**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的登入識別碼。|  
|**密碼**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼。|  
|**commit_batch_size**|**int**|不支援。|  
|**status_batch_size**|**int**|不支援。|  
|**flush_frequency**|**int**|不支援。|  
|**frequency_type**|**int**|散發代理程式的執行頻率：<br /><br /> **1** = 一次<br /><br /> **2** = 視需要<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月相對<br /><br /> **64** = 自動啟動<br /><br /> **128** = 重複執行|  
|**frequency_interval**|**int**|若要設定的頻率所套用的值*frequency_type*。|  
|**frequency_relative_interval**|**int**|散發代理程式的日期時使用*frequency_type*設**32** （每月相對）：<br /><br /> **1** = 第一個<br /><br /> **2** = 第二個<br /><br /> **4** = 第三個<br /><br /> **8** = 第四個<br /><br /> **16** = 最後一個|  
|**frequency_recurrence_factor**|**int**|所用的循環因數*frequency_type*。|  
|**frequency_subday**|**int**|在定義的期間內，重新排程的頻率：<br /><br /> **1** = 一次<br /><br /> **2** = 第二個<br /><br /> **4** = 分鐘<br /><br /> **8** = 小時|  
|**frequency_subday_interval**|**int**|間隔*frequency_subday*。|  
|**active_start_time_of_day**|**int**|第一次排程散發代理程式的當日時間，格式為 HHMMSS。|  
|**active_end_time_of_day**|**int**|排程停止散發代理程式的當日時間，格式為 HHMMSS。|  
|**active_start_date**|**int**|第一次排程散發代理程式的日期，格式為 YYYYMMDD。|  
|**active_end_date**|**int**|排程停止散發代理程式的日期，格式為 YYYYMMDD。|  
|**retryattempt**|**int**|不支援。|  
|**retrydelay**|**int**|不支援。|  
|**描述**|**nvarchar(255)**|訂閱者的文字描述。|  
|**security_mode**|**int**|實作的安全性模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證|  
|**frequency_type2**|**int**|合併代理程式的執行頻率：<br /><br /> **1** = 一次<br /><br /> **2** = 視需要<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月相對<br /><br /> **64** = 自動啟動<br /><br /> **128** = 重複執行|  
|**frequency_interval2**|**int**|若要設定的頻率所套用的值*frequency_type*。|  
|**frequency_relative_interval2**|**int**|合併代理程式的日期時使用*frequency_type*設為 32 （每月相對）：<br /><br /> **1** = 第一個<br /><br /> **2** = 第二個<br /><br /> **4** = 第三個<br /><br /> **8** = 第四個<br /><br /> **16** = 最後一個|  
|**frequency_recurrence_factor2**|**int**|所用的循環因數*frequency_type**。*|  
|**frequency_subday2**|**int**|在定義的期間內，重新排程的頻率：<br /><br /> **1** = 一次<br /><br /> **2** = 第二個<br /><br /> **4** = 分鐘<br /><br /> **8** = 小時|  
|**frequency_subday_interval2**|**int**|間隔*frequency_subday*。|  
|**active_start_time_of_day2**|**int**|第一次排程合併代理程式的當日時間，格式為 HHMMSS。|  
|**active_end_time_of_day2**|**int**|排程停止合併代理程式的當日時間，格式為 HHMMSS。|  
|**active_start_date2**|**int**|第一次排程合併代理程式的日期，格式為 YYYYMMDD。|  
|**active_end_date2**|**int**|排程停止合併代理程式的日期，格式為 YYYYMMDD。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpsubscriberinfo**用於快照式複寫、 異動複寫和合併式複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色、 **db_owner**固定的資料庫角色或發行集的發行集存取清單可以執行**sp_helpsubscriberinfo**.  
  
## <a name="see-also"></a>請參閱＜  
 [sp_adddistpublisher &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addpullsubscription &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
