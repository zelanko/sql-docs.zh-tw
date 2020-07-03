---
title: sp_trace_create （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a8327dc8beafb5d4e219cdaf25c44c75af3e85e5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892606"
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
`[ @traceid = ] trace_id`這是指派給 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新追蹤的數位。 系統會忽略任何使用者所提供的輸入。 *trace_id*是**int**，預設值是 Null。 使用者會使用*trace_id*值來識別、修改和控制此預存程式所定義的追蹤。  
  
`[ @options = ] option_value`指定追蹤所設定的選項。 *option_value*是**int**，沒有預設值。 使用者可以指定所取用選項的總值，來選擇這些選項的組合。 例如，若要開啟 TRACE_FILE_ROLLOVER 和 SHUTDOWN_ON_ERROR 的選項，請指定**6**用於*option_value*。  
  
 下表列出選項、描述及其值。  
  
|選項名稱|選項值|說明|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|指定當到達*max_file_size*時，會關閉目前的追蹤檔案，並建立新的檔案。 所有新記錄都會寫入新檔案中。 新檔案與先前的檔案同名，但會附加一個整數來表示順序。 例如，如果原始追蹤檔的名稱是 filename.trc，下一個追蹤檔的名稱就是 filename_1.trc，再下一個追蹤檔的名稱就是 filename_2.trc，依此類推。<br /><br /> 在建立換用追蹤檔時，檔案名稱所附加的整數值也會循序增加。<br /><br /> 如果指定了這個選項，但未指定*max_file_size*的值，SQL Server 會使用*max_file_size*的預設值（5 MB）。|  
|SHUTDOWN_ON_ERROR|**4**|指定追蹤因故無法寫入檔案時，SQL Server 便關機。 當執行安全性稽核追蹤時，這個選項非常有用。|  
|TRACE_PRODUCE_BLACKBOX|**8**|指定伺服器將所產生最後 5 MB 的追蹤資訊記錄儲存起來。 TRACE_PRODUCE_BLACKBOX 與所有其他選項不相容。|  
  
`[ @tracefile = ] 'trace_file'`指定將寫入追蹤的位置和檔案名。 *trace_file*是**Nvarchar （245）** ，沒有預設值。 *trace_file*可以是本機目錄（如 n ' C:\MSSQL\Trace\trace.trc '）或 UNC 到共用或路徑（N ' \\ \\ *Servername* \\ *共用* \\ *目錄*\trace.trc '）。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會將副檔名 **.trc**附加至所有追蹤檔案名。 如果指定了 TRACE_FILE_ROLLOVER 選項和*max_file_size* ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 則當原始追蹤檔案成長到其大小上限時，會建立新的追蹤檔案。 新檔案與原始檔案具有相同的名稱，但會附加 _*n*以指出其順序，從**1**開始。 例如，如果第一個追蹤檔案的名稱為 **.trc**，則第二個追蹤檔案的名稱會是**filename_1. .trc**。  
  
 如果使用了 TRACE_FILE_ROLLOVER 選項，建議您不要在原始追蹤檔名稱中使用底線字元。 若您使用底線字元，便會發生下列行為：  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]不會自動載入或提示您載入換用檔案（如果已設定其中任何一個檔案變換選項）。  
  
-   Fn_trace_gettable 函數不會載入換用檔案（當使用*number_files*引數指定時），其中原始檔案名稱的結尾是底線和數值。 (若為檔案換用時自動附加的底線及數值，則不在此列)。  
  
> [!NOTE]  
>  為了因應以上兩種行為，您可以重新命名檔案，移除原始檔案名稱中的底線。 例如，如果原始檔案名為**my_trace .trc**，而換用檔案的名稱為**my_trace_1 .trc**，則您可以在中開啟檔案之前，將檔案重新命名為**mytrace. .trc**和**mytrace_1. .trc** [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 。  
  
 使用 TRACE_PRODUCE_BLACKBOX 選項時，無法指定*trace_file* 。  
  
`[ @maxfilesize = ] max_file_size`指定追蹤檔案所能成長的大小上限（以 mb 為單位）。 *max_file_size*是**Bigint**，預設值是**5**。  
  
 如果指定這個參數時沒有 TRACE_FILE_ROLLOVER 選項，當使用的磁碟空間超過*max_file_size*所指定的數量時，追蹤就會停止記錄到檔案中。  
  
`[ @stoptime = ] 'stop_time'`指定追蹤將停止的日期和時間。 *stop_time*是**datetime**，預設值是 Null。 如果是 NULL，追蹤就會執行到手動停止或伺服器關機為止。  
  
 如果同時指定*stop_time*和*max_file_size* ，而且未指定 TRACE_FILE_ROLLOVER，則當到達指定的停止時間或檔案大小上限時，追蹤就會在上方。 如果指定*stop_time*、 *max_file_size*和 TRACE_FILE_ROLLOVER，追蹤就會在指定的停止時間停止，假設追蹤不會填滿磁片磁碟機。  
  
`[ @filecount = ] 'max_rollover_files'`指定要使用相同的基底檔案名來維護的最大數目或追蹤檔案。 *max_rollover_files*為**int**，大於1。 只有在指定了 TRACE_FILE_ROLLOVER 選項時，這個參數才有效。 當指定*max_rollover_files*時，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 開啟新的追蹤檔案之前，會先刪除最舊的追蹤檔，以嘗試維護不超過*max_rollover_files*的追蹤檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在基礎檔案名稱上附加數字來追蹤這些追蹤檔的存在時間。  
  
 例如，當*trace_file*參數指定為 "c:\mytrace" 時，名稱為 "c：\ mytrace_123. .trc" 的檔案會比名稱為 "c：\ mytrace_124. .trc" 的檔案舊。 如果*max_rollover_files*設定為2，則 SQL Server 會先刪除檔案 "c：\ mytrace_123. .trc"，再建立追蹤檔案 "c：\ mytrace_125. .trc"。  
  
 請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 只會嘗試刪除各個檔案一次，且無法刪除有其他程序在使用的檔案。 因此，如果您在進行追蹤時，有另一個應用程式在使用追蹤檔，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將這些追蹤檔保留在檔案系統中。  
  
## <a name="return-code-values"></a>傳回碼值  
 下表描述在預存程序完成之後，使用者可能得到的代碼值。  
  
|傳回碼|說明|  
|-----------------|-----------------|  
|0|沒有錯誤。|  
|1|未知的錯誤。|  
|10|無效的選項。 當指定的選項不相容時，便傳回這個代碼。|  
|12|未建立檔案。|  
|13|記憶體用完。 當沒有足夠的記憶體可以執行指定的動作時，便傳回這個代碼。|  
|14|無效停止時間。 當指定的停止時間已發生過時，便傳回這個代碼。|  
|15|無效的參數。 當使用者提供不相容的參數時，便傳回這個代碼。|  
  
## <a name="remarks"></a>備註  
 **sp_trace_create**是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程式，它會執行先前版本 SQL Server 中所提供的** \* xp_trace_** 擴充預存程式所執行的許多動作。 使用**sp_trace_create** ，而不是：  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create**只會建立追蹤定義。 您無法利用這個預存程序來啟動或變更追蹤。  
  
 所有 SQL 追蹤預存程式的參數（**sp_trace_xx**）都是嚴格類型。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
 針對**sp_trace_create**， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶必須具有追蹤檔案資料夾的寫入權限。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶不是追蹤檔所在電腦的管理員，您就必須將寫入權限明確授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。  
  
> [!NOTE]  
>  您可以使用**fn_trace_gettable**系統函數，將以**sp_trace_create**建立的追蹤檔案自動載入資料表。 如需如何使用此系統函數的詳細資訊，請參閱[fn_trace_gettable &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
 **TRACE_PRODUCE_BLACKBOX**具有下列特性：  
  
-   這是換用追蹤。 預設*file_count*為2，但可由使用者使用*filecount*選項來覆寫。  
  
-   預設*file_size*與其他追蹤相同，這是 5 MB，且可以變更。  
  
-   不可指定任何檔名。 檔案將儲存為： **N '%SQLDIR%\MSSQL\DATA\blackbox.trc '**  
  
-   追蹤中只會包含下列事件及其資料行：  
  
    -   **RPC starting**  
  
    -   **Batch starting**  
  
    -   **例外狀況**  
  
    -   **Attention**  
  
-   無法從這項追蹤加入或移除事件或資料行。  
  
-   無法針對這項追蹤指定篩選器。  
  
## <a name="permissions"></a>權限  
 使用者必須有 ALTER TRACE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  
