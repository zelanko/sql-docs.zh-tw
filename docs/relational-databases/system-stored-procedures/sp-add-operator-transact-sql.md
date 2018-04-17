---
title: sp_add_operator (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c91f79397a84f6277f4bb891144a5fceb40d02ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spaddoperator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立操作員 (通知收件者) 來搭配使用警示和作業。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]   
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]   
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]   
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@name=** ] **'***name***'**  
 操作員 (通知收件者) 的名稱。 此名稱必須是唯一的而且不能包含百分比 (**%**) 字元。 *名稱*是**sysname**，沒有預設值。  
  
 [  **@enabled=** ]*啟用*  
 指出操作員目前的狀態。 *啟用*是**tinyint**，預設值是**1** （啟用）。 如果**0**，操作員未啟用，並不會收到通知。  
  
 [ **@email_address=** ] **'***email_address***'**  
 操作員的電子郵件地址。 這個字串會直接傳遞至電子郵件系統。 *email_address*是**nvarchar （100)**，預設值是 NULL。  
  
 您可以指定實體電子郵件地址或別名*email_address*。 例如：  
  
 '**jdoe**'**jdoe@xyz.com**'  
  
> [!NOTE]  
>  您必須針對 Database Mail 使用電子郵件地址。  
  
 [ **@pager_address=** ] **'***pager_address***'**  
 操作員的呼叫器號碼。 這個字串會直接傳遞至電子郵件系統。 *pager_address*是**narchar(100)**，預設值是 NULL。  
  
 [ **@weekday_pager_start_time=** ] *weekday_pager_start_time*  
 從星期一到星期五的工作日，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在經過這段時間之後，便將呼叫器通知傳給指定的操作員。 *weekday_pager_start_time*是**int**，預設值是**090000**，表示上午 9:00 必須用 HHMMSS 格式來輸入。  
  
 [ **@weekday_pager_end_time=** ] *weekday_pager_end_time*  
 之後的時間**SQLServerAgent**服務便不再將呼叫器通知給指定操作員的工作日，從星期一到星期五。 *weekday_pager_end_time*是**int**，預設值是 180000，表示下午 6:00 必須用 HHMMSS 格式來輸入。  
  
 [ **@saturday_pager_start_time =**] *saturday_pager_start_time*  
 之後的時間**SQLServerAgent**服務將呼叫器通知傳送給指定的操作員在星期六。 *saturday_pager_start_time*是**int**，預設值是 090000，表示上午 9:00 必須用 HHMMSS 格式來輸入。  
  
 [ **@saturday_pager_end_time=** ] *saturday_pager_end_time*  
 之後的時間**SQLServerAgent**服務便不再將呼叫器通知給指定的操作員在星期六。 *saturday_pager_end_time*是**int**，預設值是**180000**，表示下午 6:00 必須用 HHMMSS 格式來輸入。  
  
 [ **@sunday_pager_start_time=** ] *sunday_pager_start_time*  
 之後的時間**SQLServerAgent**服務將呼叫器通知傳送給指定的操作員在星期日。 *sunday_pager_start_time*是**int**，預設值是**090000**，表示上午 9:00 必須用 HHMMSS 格式來輸入。  
  
 [ **@sunday_pager_end_time =**] *sunday_pager_end_time*  
 之後的時間**SQLServerAgent**服務便不再將呼叫器通知給指定的操作員在星期日。 *sunday_pager_end_time*是**int**，預設值是**180000**，表示下午 6:00 必須用 HHMMSS 格式來輸入。  
  
 [  **@pager_days=** ] *pager_days*  
 這是一個數字，指出操作員能夠接收呼叫的天數 (遵照指定的開始/結束時間)。 *pager_days*是**tinyint**，預設值是**0**表示操作員便永遠不會收到頁面。 有效值為**0**透過**127**。 *pager_days*的計算方式是加入必要天數的個別值。 例如，從星期一到星期五是**2**+**4**+**8**+**16** + **32** = **62**。 下表列出一星期中各天的值。  
  
|Value|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**4**|星期二|  
|**8**|星期三|  
|**16**|星期四|  
|**32**|星期五|  
|**64**|星期六|  
  
 [ **@netsend_address=** ] **'***netsend_address***'**  
 要傳送網路訊息的目標操作員網路位址。 *netsend_address*是**nvarchar （100)**，預設值是 NULL。  
  
 [ **@category_name=** ] **'***category***'**  
 這位操作員的類別目錄名稱。 *類別*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_add_operator**必須從執行**msdb**資料庫。  
  
 電子郵件系統也支援傳呼，如果您要使用傳呼，電子郵件系統必須有「電子郵件至呼叫器」的功能。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_operator**。  
  
## <a name="examples"></a>範例  
 下列範例設定 `danwi` 的操作員資訊。 操作員是啟用的狀態。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會在星期一到星期五的上午 8 點至下午 5 點，利用呼叫器來傳送通知 。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
