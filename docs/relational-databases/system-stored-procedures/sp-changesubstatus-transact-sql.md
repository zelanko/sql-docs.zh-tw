---
title: sp_changesubstatus (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0040f986e5ff3b6de025761b32d2f40e2e127d39
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529612"
---
# <a name="spchangesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更現有訂閱者的狀態。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，預設值是**%**。 如果*發行集*未指定，會影響所有發行集。  
  
`[ @article = ] 'article'` 是發行項的名稱。 對發行集而言，它必須是唯一的。 *發行項*已**sysname**，預設值是**%**。 如果*文章*未指定，所有發行項會受到影響。  
  
`[ @subscriber = ] 'subscriber'` 是要變更狀態的訂閱者的名稱。 *訂閱者*已**sysname**，預設值是**%**。 如果*訂閱者*未指定，狀態時，都會變更為 所有訂閱者上，指定的發行項。  
  
`[ @status = ] 'status'` 這是在訂用帳戶狀態**syssubscriptions**資料表。 *狀態*已**sysname**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**active**|已同步處理訂閱者，正在接收資料。|  
|**inactive**|訂閱者項目存在，但不含訂閱。|  
|**subscribed**|訂閱者在要求資料，但尚未同步處理。|  
  
`[ @previous_status = ] 'previous_status'` 這是先前狀態的訂用帳戶。 *previous_status*已**sysname**，預設值是 NULL。 此參數可讓您變更目前是這個狀態，因此允許一組特定的訂用帳戶中的 群組函式的任何訂用帳戶 (例如，將設定所有作用中訂用帳戶將會回到**訂閱**)。  
  
`[ @destination_db = ] 'destination_db'` 是目的地資料庫的名稱。 *destination_db*已**sysname**，預設值是**%**。  
  
`[ @frequency_type = ] frequency_type` 是用來排程散發工作的頻率。 *frequency_type*已**int**，預設值是 NULL。  
  
`[ @frequency_interval = ] frequency_interval` 要套用至所設定之頻率的值*frequency_type*。 *frequency_interval*已**int**，預設值是 NULL。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 這是散發工作的日期。 使用這個參數時*frequency_type*設定為 32 （每月相對）。 *frequency_relative_interval*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|第一個|  
|**2**|第二個|  
|**4**|第三個|  
|**8**|第四個|  
|**16**|最後一個|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 所使用的循環因數*frequency_type*。 *frequency_recurrence_factor*已**int**，預設值是 NULL。  
  
`[ @frequency_subday = ] frequency_subday` 是頻率，以分鐘為單位，將重新排定成定義的期間。 *frequency_subday*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二個|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 間隔*frequency_subday*。 *frequency_subday_interval*已**int**，預設值是 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 當散發工作這是第一次的排程時間，格式為 HHMMSS。 *active_start_time_of_day*已**int**，預設值是 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 已停止散發工作的當日時間排程，格式為 HHMMSS。 *active_end_time_of_day*已**int**，預設值是 NULL。  
  
`[ @active_start_date = ] active_start_date` 是散發工作時第一個排程的日期，格式為 YYYYMMDD。 *active_start_date*已**int**，預設值是 NULL。  
  
`[ @active_end_date = ] active_end_date` 已停止散發工作的日期排程，格式為 YYYYMMDD。 *active_end_date*已**int**，預設值是 NULL。  
  
`[ @optional_command_line = ] 'optional_command_line'` 是選擇性的命令提示字元。 *optional_command_line*已**nvarchar(4000)**，預設值是 NULL。  
  
`[ @distribution_jobid = ] distribution_jobid` 從非作用中的訂用帳戶狀態變更為 作用中時，請為散發代理程式在散發者的訂用帳戶的作業識別碼。 在其他情況下，不會加以定義。 如果對這個預存程序的單一呼叫涉及多個散發代理程式，就不會定義結果。 *distribution_jobid*已**二進位 （16)**，預設值是 NULL。  
  
`[ @from_auto_sync = ] from_auto_sync` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] remote_agent_activation`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_activation&lt*以外的值來**0**會產生錯誤。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 設定*remote_agent_server_name*為任何非 NULL 值會產生錯誤。  
  
`[ @dts_package_name = ] 'dts_package_name'` 指定 Data Transformation Services (DTS) 封裝的名稱。 *dts_package_name*已**sysname**，預設值是 NULL。 例如，對於名為的套件**DTSPub_Package**您可以指定`@dts_package_name = N'DTSPub_Package'`。  
  
`[ @dts_package_password = ] 'dts_package_password'` 指定封裝的密碼。 *dts_package_password*已**sysname**預設值是 NULL，它指定密碼屬性維持不變。  
  
> [!NOTE]  
>  DTS 封裝必須有密碼。  
  
`[ @dts_package_location = ] dts_package_location` 指定封裝位置。 *dts_package_location*已**int**，預設值是**0**。 如果**0**，封裝位置是在散發者。 如果**1**，封裝位置是在 「 訂閱者 」。 封裝位置可以是**散發者端**或是**訂閱者**。  
  
`[ @skipobjectactivation = ] skipobjectactivation` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @distribution_job_name = ] 'distribution_job_name'` 是散發工作的名稱。 *distribution_job_name*已**sysname**，預設值是 NULL。  
  
`[ @publisher = ] 'publisher'` 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*應該不在上變更發行項屬性時才使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubstatus**用於快照式複寫和異動複寫。  
  
 **sp_changesubstatus**中的訂閱者的狀態變更**syssubscriptions**資料表具有已變更的狀態。 如有需要，它會更新中的發行項狀態**sysarticles**資料表，以指出作用中或非使用中。 如有需要，它會設定複寫旗標開啟或關閉**sysobjects**在複寫資料表的資料表。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定的資料庫角色或訂用帳戶的建立者能夠執行**sp_changesubstatus**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
