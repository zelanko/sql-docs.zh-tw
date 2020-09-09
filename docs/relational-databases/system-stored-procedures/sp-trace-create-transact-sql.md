---
description: sp_trace_create (Transact-SQL)
title: sp_trace_create (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 47e16f40b7cdd9ea9c65d3262487a7a68c8cb6ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547317"
---
# <a name="sp_trace_create-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @traceid = ] trace_id` 這是指派給 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新追蹤的號碼。 系統會忽略任何使用者所提供的輸入。 *trace_id* 是 **int**，預設值是 Null。 使用者會使用 *trace_id* 值來識別、修改和控制這個預存程式所定義的追蹤。  
  
`[ @options = ] option_value` 指定追蹤所設定的選項。 *option_value* 是 **int**，沒有預設值。 使用者可以指定所取用選項的總值，來選擇這些選項的組合。 例如，若要開啟 TRACE_FILE_ROLLOVER 和 SHUTDOWN_ON_ERROR 的選項，請針對*option_value*指定**6** 。  
  
 下表列出選項、描述及其值。  
  
|選項名稱|選項值|描述|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|指定當達到 *max_file_size* 時，將會關閉目前的追蹤檔案，並建立新的檔案。 所有新記錄都會寫入新檔案中。 新檔案與先前的檔案同名，但會附加一個整數來表示順序。 例如，如果原始追蹤檔的名稱是 filename.trc，下一個追蹤檔的名稱就是 filename_1.trc，再下一個追蹤檔的名稱就是 filename_2.trc，依此類推。<br /><br /> 在建立換用追蹤檔時，檔案名稱所附加的整數值也會循序增加。<br /><br /> 如果指定此選項，但未指定*max_file_size*的值，SQL Server 會使用預設值*MAX_FILE_SIZE* (5 MB) 。|  
|SHUTDOWN_ON_ERROR|**4**|指定追蹤因故無法寫入檔案時，SQL Server 便關機。 當執行安全性稽核追蹤時，這個選項非常有用。|  
|TRACE_PRODUCE_BLACKBOX|**8**|指定伺服器將所產生最後 5 MB 的追蹤資訊記錄儲存起來。 TRACE_PRODUCE_BLACKBOX 與所有其他選項不相容。|  
  
`[ @tracefile = ] 'trace_file'` 指定將寫入追蹤的位置和檔案名。 *trace_file* 是 **Nvarchar (245) ** 沒有預設值。 *trace_file*可以是本機目錄 (例如 n ' C:\MSSQL\Trace\trace.trc ' ) 或 UNC 至共用或路徑 (N ' \\ \\ *Servername* \\ *共用* \\ *目錄*\trace.trc ' ) 。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 **>flightrecordercurrent.trc** 副檔名附加至所有追蹤檔案名。 如果指定了 TRACE_FILE_ROLLOVER 選項和 *max_file_size* ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當原始的追蹤檔案成長到其大小上限時，就會建立新的追蹤檔案。 新檔案與原始檔案的名稱相同，但會附加 _*n* 以表示其順序，從 **1**開始。 例如，如果第一個追蹤檔的名稱是 **>flightrecordercurrent.trc**，則第二個追蹤檔的名稱為 **filename_1. >flightrecordercurrent.trc**。  
  
 如果使用了 TRACE_FILE_ROLLOVER 選項，建議您不要在原始追蹤檔名稱中使用底線字元。 若您使用底線字元，便會發生下列行為：  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果) 這些檔案換用選項的其中一個設定，則不會自動載入或提示您載入換用檔案 (。  
  
-   Fn_trace_gettable 函式在使用 *number_files* 自) 變數指定時，不會載入換用檔案 (，其中原始檔案的名稱結尾為底線和數值。 (若為檔案換用時自動附加的底線及數值，則不在此列)。  
  
> [!NOTE]  
>  為了因應以上兩種行為，您可以重新命名檔案，移除原始檔案名稱中的底線。 例如，如果原始檔案名為 **my_trace >flightrecordercurrent.trc**，而換用檔案的 my_trace_1 名稱為 **>flightrecordercurrent.trc**，您可以將檔案重新命名為 **mytrace. >flightrecordercurrent.trc** 和 **mytrace_1. >flightrecordercurrent.trc** ，然後再開啟中的檔案 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 。  
  
 使用 TRACE_PRODUCE_BLACKBOX 選項時，無法指定*trace_file* 。  
  
`[ @maxfilesize = ] max_file_size` 指定追蹤檔案可以成長的大小上限（以 mb 為單位）)  (MB。 *max_file_size* 是 **Bigint**，預設值是 **5**。  
  
 如果指定此參數但未指定 TRACE_FILE_ROLLOVER 選項，當使用的磁碟空間超過 *max_file_size*指定的數量時，追蹤就會停止記錄至檔案。  
  
`[ @stoptime = ] 'stop_time'` 指定追蹤將停止的日期和時間。 *stop_time* 是 **datetime**，預設值是 Null。 如果是 NULL，追蹤就會執行到手動停止或伺服器關機為止。  
  
 如果同時指定 *stop_time* 和 *max_file_size* ，而且未指定 TRACE_FILE_ROLLOVER，則在達到指定的停止時間或最大檔案大小時，就會進行追蹤。 如果指定 *stop_time*、 *max_file_size*和 TRACE_FILE_ROLLOVER，則追蹤會在指定的停止時間停止，並假設追蹤未填滿磁片磁碟機。  
  
`[ @filecount = ] 'max_rollover_files'` 指定要使用相同的基底檔案名來維護的最大數目或追蹤檔案。 *max_rollover_files* 是 **int**，大於1。 只有在指定了 TRACE_FILE_ROLLOVER 選項時，這個參數才有效。 當指定 *max_rollover_files* 時，會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開啟新的追蹤檔案之前，先刪除最舊的追蹤檔，嘗試維持不超過 *max_rollover_files* 的追蹤檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在基礎檔案名稱上附加數字來追蹤這些追蹤檔的存在時間。  
  
 例如，當 *trace_file* 參數指定為 "c:\mytrace" 時，名稱為 "c：\ mytrace_123. >flightrecordercurrent.trc" 的檔案會早于名稱為 "c：\ mytrace_124. >flightrecordercurrent.trc" 的檔案。 如果 *max_rollover_files* 設定為2，則 SQL Server 在建立追蹤檔 "c：\ mytrace_125. >flightrecordercurrent.trc" 之前刪除 "c：\ mytrace_123. >flightrecordercurrent.trc" 檔案。  
  
 請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會嘗試刪除各個檔案一次，且無法刪除有其他程序在使用的檔案。 因此，如果您在進行追蹤時，有另一個應用程式在使用追蹤檔，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將這些追蹤檔保留在檔案系統中。  
  
## <a name="return-code-values"></a>傳回碼值  
 下表描述在預存程序完成之後，使用者可能得到的代碼值。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|0|沒有錯誤。|  
|1|未知的錯誤。|  
|10|無效的選項。 當指定的選項不相容時，便傳回這個代碼。|  
|12|未建立檔案。|  
|13|記憶體不足。 當沒有足夠的記憶體可以執行指定的動作時，便傳回這個代碼。|  
|14|無效停止時間。 當指定的停止時間已發生過時，便傳回這個代碼。|  
|15|無效的參數。 當使用者提供不相容的參數時，便傳回這個代碼。|  
  
## <a name="remarks"></a>備註  
 **sp_trace_create**是一種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程式，它會執行先前**xp_trace_ \* **的擴充預存程式所執行的許多動作，這些動作會在舊版 SQL Server 中提供。 使用 **sp_trace_create** 取代：  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create** 只會建立追蹤定義。 您無法利用這個預存程序來啟動或變更追蹤。  
  
 所有 SQL 追蹤預存程式 (**sp_trace_xx**) 的參數都是嚴格輸入的。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
 針對 **sp_trace_create**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須具有追蹤檔案資料夾的寫入權限。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶不是追蹤檔所在電腦的管理員，您就必須將寫入權限明確授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。  
  
> [!NOTE]  
>  您可以使用**fn_trace_gettable**系統函數，自動將使用**sp_trace_create**建立的追蹤檔案載入資料表中。 如需有關如何使用這個系統函數的詳細資訊，請參閱 [sys. fn_trace_gettable &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
 **TRACE_PRODUCE_BLACKBOX** 具有下列特性：  
  
-   這是換用追蹤。 預設 *file_count* 為2，但使用者可以使用 *filecount* 選項來覆寫此預設值。  
  
-   預設 *file_size* 與其他追蹤相同是 5 MB，而且可以變更。  
  
-   不可指定任何檔名。 檔案將儲存為： **N '%SQLDIR%\MSSQL\DATA\blackbox.trc '**  
  
-   追蹤中只會包含下列事件及其資料行：  
  
    -   **RPC starting**  
  
    -   **Batch starting**  
  
    -   **例外狀況**  
  
    -   **注意**  
  
-   無法從這項追蹤加入或移除事件或資料行。  
  
-   無法針對這項追蹤指定篩選器。  
  
## <a name="permissions"></a>權限  
 使用者必須有 ALTER TRACE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  
