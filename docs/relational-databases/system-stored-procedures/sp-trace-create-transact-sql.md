---
title: sp_trace_create (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3344ad65a2445a8d39451f6a048f057b7158d135
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533400"
---
# <a name="sptracecreate-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立追蹤定義。 新追蹤會處於已停止狀態。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用擴充事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @traceid = ] trace_id` 已指派的數字[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]給新追蹤。 系統會忽略任何使用者所提供的輸入。 *trace_id*已**int**，預設值是 NULL。 使用者會利用*trace_id*值來識別、 修改和控制這個預存程序所定義的追蹤。  
  
`[ @options = ] option_value` 指定追蹤所設定的選項。 *option_value*已**int**，沒有預設值。 使用者可以指定所取用選項的總值，來選擇這些選項的組合。 例如，若要開啟這兩個 TRACE_FILE_ROLLOVER 和 SHUTDOWN_ON_ERROR 選項，指定**6** for *option_value*。  
  
 下表列出選項、描述及其值。  
  
|選項名稱|選項值|描述|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|指定當*max_file_size*為止，目前的追蹤檔案已關閉，且在建立新的檔案。 所有新記錄都會寫入新檔案中。 新檔案與先前的檔案同名，但會附加一個整數來表示順序。 例如，如果原始追蹤檔的名稱是 filename.trc，下一個追蹤檔的名稱就是 filename_1.trc，再下一個追蹤檔的名稱就是 filename_2.trc，依此類推。<br /><br /> 在建立換用追蹤檔時，檔案名稱所附加的整數值也會循序增加。<br /><br /> SQL Server 使用的預設值*max_file_size* (5 MB) 如果未指定的值指定此選項*max_file_size*。|  
|SHUTDOWN_ON_ERROR|**4**|指定追蹤因故無法寫入檔案時，SQL Server 便關機。 當執行安全性稽核追蹤時，這個選項非常有用。|  
|TRACE_PRODUCE_BLACKBOX|**8**|指定伺服器將所產生最後 5 MB 的追蹤資訊記錄儲存起來。 TRACE_PRODUCE_BLACKBOX 與所有其他選項不相容。|  
  
`[ @tracefile = ] 'trace_file'` 指定將寫入追蹤的檔案名稱與位置。 *trace_file*已**nvarchar(245)** 沒有預設值。 *trace_file*可以是本機目錄 （如 N 'C:\MSSQL\Trace\trace.trc') 或共用或路徑的 UNC (N'\\\\*Servername*\\*Sharename*\\ *Directory*\trace.trc')。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會附加 **.trc**延伸至所有的追蹤檔名稱。 如果了 TRACE_FILE_ROLLOVER 選項和*max_file_size*都有指定，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原始追蹤檔成長到其大小上限時，會建立新的追蹤檔案。 新的檔案具有相同名稱做為原始的檔案，但 __*n*附加至指出其順序，開頭**1**。 例如，如果第一個追蹤檔案名為**filename.trc**，第二個追蹤檔案會命名為**filename_1.trc**。  
  
 如果使用了 TRACE_FILE_ROLLOVER 選項，建議您不要在原始追蹤檔名稱中使用底線字元。 若您使用底線字元，便會發生下列行為：  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 不會自動載入或提示您載入換用檔案 （如果已經設定任何這些檔案換用選項）。  
  
-   Fn_trace_gettable 函數不會載入換用檔案 (當指定利用*number_files&lt*引數) 的原始的檔案名稱以底線加一個數字值的結束位置。 (若為檔案換用時自動附加的底線及數值，則不在此列)。  
  
> [!NOTE]  
>  為了因應以上兩種行為，您可以重新命名檔案，移除原始檔案名稱中的底線。 例如，如果原始的檔案命名為**my_trace.trc**，和名為換用檔案**my_trace_1.trc**，您可以重新命名的檔案**mytrace.trc**和**mytrace_1.trc**開啟中的檔案之前[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。  
  
 *trace_file*無法使用 TRACE_PRODUCE_BLACKBOX 選項時指定。  
  
`[ @maxfilesize = ] max_file_size` 指定可以成長的大小上限 （單位為 MB) 的追蹤檔案。 *您將 max_file_size*已**bigint**，預設值是**5**。  
  
 如果不使用了 TRACE_FILE_ROLLOVER 選項指定這個參數，則追蹤會停止記錄到檔案時使用的磁碟空間超過指定的數量*max_file_size*。  
  
`[ @stoptime = ] 'stop_time'` 指定的日期和時間將會停止追蹤。 *stop_time*已**datetime**，預設值是 NULL。 如果是 NULL，追蹤就會執行到手動停止或伺服器關機為止。  
  
 如果兩個*stop_time*並*max_file_size*都有指定，和 TRACE_FILE_ROLLOVER 不指定，追蹤多時指定的停止時間 」 或 「 最大檔案大小上限。 如果*stop_time*， *max_file_size*，而且指定了 TRACE_FILE_ROLLOVER，追蹤就會停止指定的停駐點時，假設追蹤不會填滿磁碟機。  
  
`[ @filecount = ] 'max_rollover_files'` 指定的最大的數字或追蹤檔，才能維持相同的基底檔案名稱。 *max_rollover_files*已**int**，大於 1。 只有在指定了 TRACE_FILE_ROLLOVER 選項時，這個參數才有效。 當*max_rollover_files*指定，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]嘗試維持不超過*max_rollover_files*追蹤檔的開啟新的追蹤檔之前，請先刪除最舊的追蹤檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在基礎檔案名稱上附加數字來追蹤這些追蹤檔的存在時間。  
  
 例如，當*trace_file*參數指定為"c:\mytrace"時，名稱為"c:\mytrace_123.trc"的檔案為早於具有名稱"c:\mytrace_124.trc"的檔案。 如果*max_rollover_files*是設定為 2，則 SQL Server 刪除"c:\mytrace_123.trc"的檔案再建立追蹤檔"c:\mytrace_125.trc"。  
  
 請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會嘗試刪除各個檔案一次，且無法刪除有其他程序在使用的檔案。 因此，如果您在進行追蹤時，有另一個應用程式在使用追蹤檔，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將這些追蹤檔保留在檔案系統中。  
  
## <a name="return-code-values"></a>傳回碼值  
 下表描述在預存程序完成之後，使用者可能得到的代碼值。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|0|沒有錯誤。|  
|1|未知的錯誤。|  
|10|無效的選項。 當指定的選項不相容時，便傳回這個代碼。|  
|12|未建立檔案。|  
|13|記憶體用完。 當沒有足夠的記憶體可以執行指定的動作時，便傳回這個代碼。|  
|14|無效停止時間。 當指定的停止時間已發生過時，便傳回這個代碼。|  
|15|無效的參數。 當使用者提供不相容的參數時，便傳回這個代碼。|  
  
## <a name="remarks"></a>備註  
 **sp_trace_create**已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程序會執行許多先前執行的動作**xp_trace_\*** 擴充預存程序可在舊版的 SQL Server。 使用**sp_trace_create**而不是：  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create**只會建立追蹤定義。 您無法利用這個預存程序來啟動或變更追蹤。  
  
 參數的所有 SQL 追蹤預存程序 (**sp_trace_xx**) 都有強制類型。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
 針對**sp_trace_create**，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務帳戶必須具有寫入權限的追蹤檔案資料夾。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶不是追蹤檔所在電腦的管理員，您就必須將寫入權限明確授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。  
  
> [!NOTE]  
>  您可以自動載入追蹤檔案以建立**sp_trace_create**使用資料表**fn_trace_gettable**系統函數。 如需如何使用這個系統函數的詳細資訊，請參閱[sys.fn_trace_gettable &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
 **TRACE_PRODUCE_BLACKBOX**具有下列特性：  
  
-   這是換用追蹤。 預設值*file_count*為 2，但您可以覆寫使用者利用*filecount*選項。  
  
-   預設值*file_size*一樣與其他追蹤是 5 MB，且可以變更。  
  
-   不可指定任何檔名。 檔案會儲存為：**N'%SQLDIR%\MSSQL\DATA\blackbox.trc'**  
  
-   追蹤中只會包含下列事件及其資料行：  
  
    -   **RPC 正在開始**  
  
    -   **啟動批次**  
  
    -   **Exception**  
  
    -   **注意**  
  
-   無法從這項追蹤加入或移除事件或資料行。  
  
-   無法針對這項追蹤指定篩選器。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有 ALTER TRACE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  
