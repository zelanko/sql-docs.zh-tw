---
title: sp_changesubstatus （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 5c10e05098a611e51583b2b1132f811d36b0f20a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771332"
---
# <a name="sp_changesubstatus-transact-sql"></a>sp_changesubstatus (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，預設值是**%**。 如果未指定發行集，則會影響所有*發行*集。  
  
`[ @article = ] 'article'`這是發行項的名稱。 對發行集而言，它必須是唯一的。 ** 發行項**** **%** 是 sysname，預設值是。 如果未指定發行項 *，則會*影響所有發行項。  
  
`[ @subscriber = ] 'subscriber'`這是要變更狀態的訂閱者名稱。 *訂閱者*是**sysname**，預設值是**%**。 如果未指定「*訂閱者*」，則會針對指定之發行項的所有訂閱者變更狀態。  
  
`[ @status = ] 'status'`這是**syssubscriptions**資料表中的訂用帳戶狀態。 *狀態*為**sysname**，沒有預設值，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**主動**|已同步處理訂閱者，正在接收資料。|  
|**非使用**|訂閱者項目存在，但不含訂閱。|  
|**已訂閱**|訂閱者在要求資料，但尚未同步處理。|  
  
`[ @previous_status = ] 'previous_status'`這是訂用帳戶的先前狀態。 *previous_status*是**sysname**，預設值是 Null。 這個參數可讓您變更目前具有該狀態的任何訂用帳戶，藉此允許一組特定訂用帳戶的群組函式（例如，將所有作用中的訂閱設定回**訂閱**）。  
  
`[ @destination_db = ] 'destination_db'`這是目的地資料庫的名稱。 *destination_db*是**sysname**，預設值是**%**。  
  
`[ @frequency_type = ] frequency_type`這是散發工作的排程頻率。 *frequency_type*是**int**，預設值是 Null。  
  
`[ @frequency_interval = ] frequency_interval`這是要套用至*frequency_type*所設定之頻率的值。 *frequency_interval*是**int**，預設值是 Null。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`這是散發工作的日期。 當*frequency_type*設定為32（每月相對）時，會使用這個參數。 *frequency_relative_interval*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|第一頁|  
|**2**|秒|  
|**4**|第三個|  
|**8**|第四個|  
|**1600**|最後一頁|  
|NULL (預設值)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`這是*frequency_type*所使用的迴圈因數。 *frequency_recurrence_factor*是**int**，預設值是 Null。  
  
`[ @frequency_subday = ] frequency_subday`這是在定義的期間內，重新排程的頻率（以分鐘為單位）。 *frequency_subday*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**1**|單次|  
|**2**|秒|  
|**4**|分鐘|  
|**8**|小時|  
|NULL (預設值)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`這是*frequency_subday*的間隔。 *frequency_subday_interval*是**int**，預設值是 Null。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`這是第一次排程散發工作的當日時間，格式為 HHMMSS。 *active_start_time_of_day*是**int**，預設值是 Null。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`這是排程停止散發工作的當日時間，格式為 HHMMSS。 *active_end_time_of_day*是**int**，預設值是 Null。  
  
`[ @active_start_date = ] active_start_date`這是第一次排程散發工作的日期，格式為 YYYYMMDD。 *active_start_date*是**int**，預設值是 Null。  
  
`[ @active_end_date = ] active_end_date`這是排程停止散發工作的日期，格式為 YYYYMMDD。 *active_end_date*是**int**，預設值是 Null。  
  
`[ @optional_command_line = ] 'optional_command_line'`是選擇性的命令提示字元。 *optional_command_line*是**Nvarchar （4000）**，預設值是 Null。  
  
`[ @distribution_jobid = ] distribution_jobid`這是將訂閱狀態從非作用中變更為作用中時，在訂閱者端的散發代理程式的作業識別碼。 在其他情況下，不會加以定義。 如果對這個預存程序的單一呼叫涉及多個散發代理程式，就不會定義結果。 *distribution_jobid*是**binary （16）**，預設值是 Null。  
  
`[ @from_auto_sync = ] from_auto_sync` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] remote_agent_activation`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_activation*設定為**0**以外的值會產生錯誤。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  遠端代理程式啟用已被取代，不再受到支援。 支援這個參數的目的，只是為了與舊版的指令碼相容。 將*remote_agent_server_name*設定為任何非 Null 值都會產生錯誤。  
  
`[ @dts_package_name = ] 'dts_package_name'`指定資料轉換服務（DTS）封裝的名稱。 *dts_package_name*是**sysname**，預設值是 Null。 例如，針對名為**DTSPub_Package**的封裝，您會`@dts_package_name = N'DTSPub_Package'`指定。  
  
`[ @dts_package_password = ] 'dts_package_password'`指定封裝上的密碼。 *dts_package_password*是**sysname** ，預設值是 Null，它會指定 password 屬性保持不變。  
  
> [!NOTE]  
>  DTS 封裝必須有密碼。  
  
`[ @dts_package_location = ] dts_package_location`指定封裝位置。 *dts_package_location*是**int**，預設值是**0**。 如果是**0**，則封裝位置是在散發者端。 如果是**1**，則封裝位置是在訂閱者端。 封裝的位置**可以是「** 散發者」或「**訂閱者**」。  
  
`[ @skipobjectactivation = ] skipobjectactivation` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @distribution_job_name = ] 'distribution_job_name'`這是散發作業的名稱。 *distribution_job_name*是**sysname**，預設值是 Null。  
  
`[ @publisher = ] 'publisher'`指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  ** 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者上變更發行項屬性時，不應使用「發行者」。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changesubstatus**用於快照式複寫和異動複寫中。  
  
 **sp_changesubstatus**會在**syssubscriptions**資料表中變更訂閱者的狀態，其狀態為已變更。 如有需要，它會更新**sysarticles**資料表中的發行項狀態，以指出作用中或非作用中。 如有需要，它會在複寫資料表的**sysobjects**資料表中，將複寫旗標設定為 on 或 off。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員、 **db_owner**固定資料庫角色或訂閱的建立者，才能夠執行**sp_changesubstatus**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
