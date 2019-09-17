---
title: sp_add_operator （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 14746f5d18db9fbdac3dc6f80d885a8e07e8216a
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/09/2019
ms.locfileid: "70810406"
---
# <a name="sp_add_operator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

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
`[ @name = ] 'name'`操作員（通知收件者）的名稱。 這個名稱必須是唯一的，而且不能包含 **%** 百分比（）字元。 *名稱*是**sysname**，沒有預設值。  
  
`[ @enabled = ] enabled`指出操作員的目前狀態。 [*已啟用*] 是**Tinyint**，預設值是**1** （已啟用）。 如果為**0**，則不會啟用操作員，也不會收到通知。  
  
`[ @email_address = ] 'email_address'`操作員的電子郵件地址。 這個字串會直接傳遞至電子郵件系統。 *email_address*是**Nvarchar （100）** ，預設值是 Null。  
  
 您可以為*email_address*指定實體電子郵件地址或別名。 例如:  
  
 '**jdoe**' 或 ' **jdoe@xyz.com** '  
  
> [!NOTE]  
>  您必須針對 Database Mail 使用電子郵件地址。  
  
`[ @pager_address = ] 'pager_address'`操作員的呼叫者位址。 這個字串會直接傳遞至電子郵件系統。 *pager_address*是**Nvarchar （100）** ，預設值是 Null。  
  
`[ @weekday_pager_start_time = ] weekday_pager_start_time`這[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]段時間之後，Agent 會從星期一到星期五的工作日，將呼叫者通知傳送給指定的操作員。 *weekday_pager_start_time*是**int**，預設值是**090000**，表示 9:00 A.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @weekday_pager_end_time = ] weekday_pager_end_time`這段時間之後， **SQLServerAgent**服務就不會再從星期一到星期五的工作日，將傳呼通知傳送給指定的操作員。 *weekday_pager_end_time*是**int**，預設值是180000，表示 6:00 P.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @saturday_pager_start_time = ] saturday_pager_start_time`這段時間之後， **SQLServerAgent**服務會在星期六將頁面通知傳送給指定的操作員。 *saturday_pager_start_time*是**int**，預設值是090000，表示 9:00 A.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @saturday_pager_end_time = ] saturday_pager_end_time`在這段時間之後， **SQLServerAgent**服務就不會再將呼機通知傳送給星期六的指定操作員。 *saturday_pager_end_time*是**int**，預設值是**180000**，表示 6:00 P.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @sunday_pager_start_time = ] sunday_pager_start_time`這段時間之後， **SQLServerAgent**服務會在星期日將呼叫者通知傳送給指定的操作員。 *sunday_pager_start_time*是**int**，預設值是**090000**，表示 9:00 A.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @sunday_pager_end_time = ] sunday_pager_end_time`這段時間之後， **SQLServerAgent**服務就不會再將呼機通知傳送給星期日上指定的操作員。 *sunday_pager_end_time*是**int**，預設值是**180000**，表示 6:00 P.M。 必須用 HHMMSS 格式來輸入。  
  
`[ @pager_days = ] pager_days`這是一個數位，表示操作員可供頁面使用的天數（受限於指定的開始/結束時間）。 *pager_days*是**Tinyint**，預設值是**0** ，表示操作員永遠無法用於接收頁面。 有效的值為**0**到**127**。 *pager_days*的計算方式是新增所需天數的個別值。 例如，從星期一到星期五是**2** + **4** + **8** + **16** +3262 = 。 下表列出一星期中各天的值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**4**|星期二|  
|**8**|星期三|  
|**16**|星期四|  
|**32**|星期五|  
|**64**|星期六|  
  
`[ @netsend_address = ] 'netsend_address'`要傳送網路訊息的目標操作員網路位址。 *netsend_address*是**Nvarchar （100）** ，預設值是 Null。  
  
`[ @category_name = ] 'category'`這個運算子的類別目錄名稱。 *category*是**sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 **sp_add_operator**必須從**msdb**資料庫中執行。  
  
 電子郵件系統也支援傳呼，如果您要使用傳呼，電子郵件系統必須有「電子郵件至呼叫器」的功能。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_add_operator**。  
  
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
 [sp_delete_operator &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
