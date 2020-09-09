---
description: sp_send_dbmail (Transact-SQL)
title: sp_send_dbmail (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sendmail_sp_TSQL
- sendmail_sp
- SP_SEND_DBMAIL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_send_dbmail
ms.assetid: f1d7a795-a3fd-4043-ac4b-c781e76dab47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d2e7f1d11052b422ef8eb387349fbc8089a49eb2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547426"
---
# <a name="sp_send_dbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  將電子郵件訊息傳送給指定的收件者。 訊息可能包含查詢結果集、檔案附件，或兩者皆有。 當郵件成功放置於 Database Mail 佇列時， **sp_send_dbmail** 會傳回訊息的 **mailitem_id** 。 這個預存程式在 **msdb** 資料庫中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_send_dbmail [ [ @profile_name = ] 'profile_name' ]  
    [ , [ @recipients = ] 'recipients [ ; ...n ]' ]  
    [ , [ @copy_recipients = ] 'copy_recipient [ ; ...n ]' ]  
    [ , [ @blind_copy_recipients = ] 'blind_copy_recipient [ ; ...n ]' ]  
    [ , [ @from_address = ] 'from_address' ]  
    [ , [ @reply_to = ] 'reply_to' ]   
    [ , [ @subject = ] 'subject' ]   
    [ , [ @body = ] 'body' ]   
    [ , [ @body_format = ] 'body_format' ]  
    [ , [ @importance = ] 'importance' ]  
    [ , [ @sensitivity = ] 'sensitivity' ]  
    [ , [ @file_attachments = ] 'attachment [ ; ...n ]' ]  
    [ , [ @query = ] 'query' ]  
    [ , [ @execute_query_database = ] 'execute_query_database' ]  
    [ , [ @attach_query_result_as_file = ] attach_query_result_as_file ]  
    [ , [ @query_attachment_filename = ] query_attachment_filename ]  
    [ , [ @query_result_header = ] query_result_header ]  
    [ , [ @query_result_width = ] query_result_width ]  
    [ , [ @query_result_separator = ] 'query_result_separator' ]  
    [ , [ @exclude_query_output = ] exclude_query_output ]  
    [ , [ @append_query_error = ] append_query_error ]  
    [ , [ @query_no_truncate = ] query_no_truncate ]   
    [ , [ @query_result_no_padding = ] @query_result_no_padding ]   
    [ , [ @mailitem_id = ] mailitem_id ] [ OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_name = ] 'profile_name'` 這是要用來傳送訊息的設定檔名稱。 *Profile_name*的型別為**sysname**，預設值是 Null。 *Profile_name*必須是現有 Database Mail 設定檔的名稱。 如果未指定任何 *profile_name* ， **sp_send_dbmail** 會使用目前使用者的預設私用設定檔。 如果使用者沒有預設的私人設定檔， **sp_send_dbmail** 會使用 **msdb** 資料庫的預設公用設定檔。 如果使用者沒有預設的私人設定檔，而且沒有資料庫的預設公用設定檔，則必須指定** \@ profile_name** 。  
  
`[ @recipients = ] 'recipients'` 這是要傳送訊息的電子郵件地址清單（以分號分隔）。 收件者清單的類型是 **Varchar (max) **。 雖然此參數是選擇性的，但至少必須指定其中一個收件** \@ 者、** ** \@ copy_recipients**或** \@ blind_copy_recipients** ，否則**sp_send_dbmail**會傳回錯誤。  
  
`[ @copy_recipients = ] 'copy_recipients'` 這是用來複製訊息的電子郵件地址清單（以分號分隔）。 複製收件者清單的類型是 **Varchar (max) **。 雖然此參數是選擇性的，但至少必須指定其中一個收件** \@ 者、** ** \@ copy_recipients**或** \@ blind_copy_recipients** ，否則**sp_send_dbmail**會傳回錯誤。  
  
`[ @blind_copy_recipients = ] 'blind_copy_recipients'` 這是以分號分隔的電子郵件地址清單，用來將訊息複製到其中。 密件副本收件者清單的類型是 **Varchar (max) **。 雖然此參數是選擇性的，但至少必須指定其中一個收件** \@ 者、** ** \@ copy_recipients**或** \@ blind_copy_recipients** ，否則**sp_send_dbmail**會傳回錯誤。  
  
`[ @from_address = ] 'from_address'` 這是電子郵件訊息的 [寄件者位址] 的值。 這是選擇性參數，用來覆寫郵件設定檔中的設定。 此參數的類型為 **Varchar (MAX) **。 SMTP 安全性設定會決定是否要接受這些覆寫。 如果沒有指定參數，預設值為 NULL。  
  
`[ @reply_to = ] 'reply_to'` 這是電子郵件訊息之 [回復位址] 的值。 它只接受一個電子郵件地址做為有效的值。 這是選擇性參數，用來覆寫郵件設定檔中的設定。 此參數的類型為 **Varchar (MAX) **。 SMTP 安全性設定會決定是否要接受這些覆寫。 如果沒有指定參數，預設值為 NULL。  
  
`[ @subject = ] 'subject'` 是電子郵件訊息的主旨。 主體的類型為 **Nvarchar (255) **。 如果未指定主旨，預設值便是「SQL Server 訊息」。  
  
`[ @body = ] 'body'` 這是電子郵件訊息的主體。 訊息主體的類型為 **Nvarchar (max) **，預設值是 Null。  
  
`[ @body_format = ] 'body_format'` 這是訊息主體的格式。 參數的類型是 **Varchar (20) **，預設值是 Null。 當指定這個選項時，會設定外寄訊息的標頭來表示訊息主體有指定的格式。 參數可包含下列各值之一：  
  
-   TEXT  
  
-   HTML  
  
 預設值是 TEXT。  
  
`[ @importance = ] 'importance'` 這是訊息的重要性。 參數的類型為 **Varchar (6) **。 參數可包含下列各值之一：  
  
-   低  
  
-   正常  
  
-   高  
  
 預設值是 Normal。  
  
`[ @sensitivity = ] 'sensitivity'` 這是訊息的敏感性。 參數的類型為 **Varchar (12) **。 參數可包含下列各值之一：  
  
-   正常  
  
-   個人  
  
-   Private  
  
-   機密  
  
 預設值是 Normal。  
  
`[ @file_attachments = ] 'file_attachments'` 這是要附加至電子郵件訊息的檔案名清單（以分號分隔）。 清單中的檔案必須指定為絕對路徑。 附件清單的類型為 **Nvarchar (max) **。 根據預設，Database Mail 會將檔案附件限制為每個檔案 1 MB。  
 
 > [!IMPORTANT]
 > 因為此參數無法存取本機檔案系統，所以無法在 Azure SQL 受控執行個體中使用。
  
`[ @query = ] 'query'` 這是要執行的查詢。 查詢的結果可以附加成一個檔案，也可以包含在電子郵件訊息的主體中。 查詢的類型為 **Nvarchar (max) **，而且可以包含任何有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句。 請注意，查詢會在不同的會話中執行，因此查詢中無法使用呼叫 **sp_send_dbmail** 之腳本中的本機變數。  
  
`[ @execute_query_database = ] 'execute_query_database'` 這是預存程式執行查詢所在的資料庫內容。 參數的類型是 **sysname**，預設值是目前的資料庫。 只有在指定** \@ query**時，此參數才適用。  
  
`[ @attach_query_result_as_file = ] attach_query_result_as_file` 指定是否以附加檔案的方式傳回查詢的結果集。 *attach_query_result_as_file* 的類型是 **bit**，預設值是0。  
  
 當值為0時，查詢結果會包含在電子郵件訊息的本文中（在** \@ body**參數的內容之後）。 當值是 1 時，會以附加檔案的方式傳回結果。 只有在指定** \@ query**時，此參數才適用。  
  
`[ @query_attachment_filename = ] query_attachment_filename` 指定要用於查詢附件之結果集的檔案名。 *query_attachment_filename* 的類型為 **Nvarchar (255) **，預設值是 Null。 當 *attach_query_result* 為0時，會忽略此參數。 當 *attach_query_result* 為1，且此參數為 Null 時，Database Mail 會建立任意的檔案名。  
  
`[ @query_result_header = ] query_result_header` 指定查詢結果是否包含資料行標頭。 Query_result_header 值的類型為 **bit**。 當值是 1 時，查詢結果會包含資料行標頭。 當值是 0 時，查詢結果不會包含資料行標頭。 此參數預設為 **1**。 只有在指定** \@ query**時，此參數才適用。  
 
   >[!NOTE]
   > 將 \@ query_result_header 設定為0，並將 query_no_truncate 設定為1時，可能會發生下列錯誤 \@ ：
   > <br> 訊息22050，層級16，狀態1，行12：無法初始化 sqlcmd 程式庫，錯誤號碼：2147024809。
  
`[ @query_result_width = ] query_result_width` 這是用來格式化查詢結果的行寬（以字元為單位）。 *Query_result_width*的類型是**int**，預設值是256。 提供的值必須介於 10 和 32767 之間。 只有在指定** \@ query**時，此參數才適用。  
  
`[ @query_result_separator = ] 'query_result_separator'` 這是在查詢輸出中用來分隔資料行的字元。 分隔符號的類型為 **char (1) **。 預設值是 ' ' (空白)。  
  
`[ @exclude_query_output = ] exclude_query_output` 指定是否要在電子郵件訊息中傳回查詢執行的輸出。 **exclude_query_output** 是 bit，預設值是0。 當這個參數是0時， **sp_send_dbmail** 預存程式的執行會在主控台上列印查詢執行結果所傳回的訊息。 當這個參數是1時，執行 **sp_send_dbmail** 預存程式並不會在主控台上列印任何查詢執行訊息。  
  
`[ @append_query_error = ] append_query_error`指定在** \@ 查詢**引數中指定的查詢傳回錯誤時，是否傳送電子郵件。 **append_query_error** 是 **bit**，預設值是0。 當這個參數是 1 時，Database Mail 會傳送電子郵件，且會在電子郵件的主體中包含查詢錯誤訊息。 當這個參數是0時，Database Mail 不會傳送電子郵件訊息，且 **sp_send_dbmail** 以傳回碼1結尾，表示失敗。  
  
`[ @query_no_truncate = ] query_no_truncate` 指定是否要使用選項來執行查詢，以避免截斷大型可變長度資料類型 (**Varchar (max) **、 **Nvarchar (max) **、 **Varbinary (max) **、 **xml**、 **text**、 **Ntext**、 **image**和使用者定義資料類型) 。 若有設定，查詢結果不包含資料行標頭。 *Query_no_truncate*值的類型為**bit**。 當此值是 0 或未指定時，查詢中的資料行會截斷為 256 個字元。 當此值是 1 時，不會截斷查詢中的資料行。 這個參數的預設值是 0。  
  
> [!NOTE]  
>  搭配大量資料使用時， \@ **query_no_truncate**選項會耗用額外的資源，而且可能會降低伺服器效能。  
  
`[ @query_result_no_padding ] @query_result_no_padding` 此類型為 bit。 預設值是 0。 當您將設定為1時，查詢結果不會填補，可能會減少檔案大小。如果您將 \@ query_result_no_padding 設定為1，並設定 \@ query_result_width 參數， \@ query_result_no_padding 參數會覆寫 \@ query_result_width 參數。  
  
 在此情況下，不會發生任何錯誤。  
 
  >[!NOTE]
  > 將 \@ query_result_no_padding 設定為1，並為 query_no_truncate 提供參數時，可能會發生下列錯誤 \@ ：
  > <br> 訊息22050，層級16，狀態1，行0：無法執行查詢，因為 \@ query_result_no_append 和 \@ query_no_truncate 選項互斥。 
  
 如果您將 \@ query_result_no_padding 設定為1，並設定 \@ query_no_truncate 參數，則會引發錯誤。  
  
`[ @mailitem_id = ] mailitem_id [ OUTPUT ]` 選擇性輸出參數會傳回訊息的 *mailitem_id* 。 *Mailitem_id*的類型為**int**。  
  
## <a name="return-code-values"></a>傳回碼值  
 傳回碼為 0 表示成功。 其他任何值都表示失敗。 失敗的語句錯誤碼會儲存在 \@ \@ 錯誤變數中。  
  
## <a name="result-sets"></a>結果集  
 成功時，傳回「郵件已列入佇列」訊息。  
  
## <a name="remarks"></a>備註  
 在使用之前，必須使用 Database Mail Configuration Wizard 或 **sp_configure**來啟用 Database Mail。  
  
 **sysmail_stop_sp** 停止外部程式所使用的 Service Broker 物件，以停止 Database Mail。 當使用**sysmail_stop_sp**停止 Database Mail 時， **sp_send_dbmail**仍接受 mail。 若要開始 Database Mail，請使用 **sysmail_start_sp**。  
  
 未指定** \@ 設定檔**時， **sp_send_dbmail**會使用預設設定檔。 如果傳送電子郵件訊息的使用者有預設私人設定檔，Database Mail 會使用這個設定檔。 如果使用者沒有預設的私人設定檔， **sp_send_dbmail** 會使用預設公用設定檔。 如果使用者沒有預設的私人設定檔，而且沒有預設公用設定檔， **sp_send_dbmail** 會傳回錯誤。  
  
 **sp_send_dbmail** 不支援沒有內容的電子郵件訊息。 若要傳送電子郵件訊息，您必須至少指定其中一個** \@ body**、 ** \@ query**、 ** \@ file_attachments**或** \@ subject**。 否則， **sp_send_dbmail** 會傳回錯誤。  
  
 Database Mail 利用目前使用者的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 安全性內容來控制檔案的存取。 因此，使用驗證進行驗證的使用者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法使用** \@ file_attachments**附加檔案。 Windows 不允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在遠端電腦之間提供認證。 因此，從執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦以外的電腦執行命令時，Database Mail 可能無法從網路共用附加檔案。  
  
 如果同時指定了** \@ 查詢**和** \@ file_attachments** ，而且找不到該檔案，則仍會執行查詢，但不會傳送電子郵件。  
  
 當指定查詢時，結果集會格式化為內嵌文字。 結果中的二進位資料會以十六進位格式傳送。  
  
 收件** \@ 者**、 ** \@ copy_recipients**和** \@ blind_copy_recipients**的參數都是以分號分隔的電子郵件地址清單。 至少必須提供這些參數的其中一個，否則 **sp_send_dbmail** 會傳回錯誤。  
  
 在沒有交易內容的情況下執行 **sp_send_dbmail** 時，Database Mail 會啟動並認可隱含交易。 從現有交易中執行 **sp_send_dbmail** 時，Database Mail 會依賴使用者來認可或回復任何變更。 它並不會啟動內部交易。  
  
## <a name="permissions"></a>權限  
 **Sp_send_dbmail**的 Execute 許可權預設為**Msdb**資料庫中**DatabaseMailUser**資料庫角色的所有成員。 但是，當傳送訊息的使用者沒有使用該要求設定檔的許可權時， **sp_send_dbmail** 會傳回錯誤，而且不會傳送訊息。  
  
## <a name="examples"></a>範例  
  
### <a name="a-sending-an-e-mail-message"></a>A. 傳送電子郵件訊息  
 此範例會使用電子郵件地址，將電子郵件訊息傳送給您的朋友 `myfriend@Adventure-Works.com` 。 訊息的主旨是 `Automated Success Message`。 訊息的主體包含 `'The stored procedure finished successfully'` 這個句子。  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>B. 利用查詢結果傳送電子郵件訊息  
 此範例會使用電子郵件地址，將電子郵件訊息傳送給您的朋友 `yourfriend@Adventure-Works.com` 。 訊息的主旨是 `Work Order Count`，且會執行查詢來顯示在 2004 年 4 月 30 日之後 `DueDate` 小於兩天的工作訂單數目。 Database Mail 會將結果附加為一個文字檔。  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @query = 'SELECT COUNT(*) FROM AdventureWorks2012.Production.WorkOrder  
                  WHERE DueDate > ''2004-04-30''  
                  AND  DATEDIFF(dd, ''2004-04-30'', DueDate) < 2' ,  
    @subject = 'Work Order Count',  
    @attach_query_result_as_file = 1 ;  
```  
  
### <a name="c-sending-an-html-e-mail-message"></a>C. 傳送 HTML 電子郵件訊息  
 此範例會使用電子郵件地址，將電子郵件訊息傳送給您的朋友 `yourfriend@Adventure-Works.com` 。 訊息的主旨是 `Work Order List`，且包含一份 HTML 文件，其中顯示在 2004 年 4 月 30 日之後 `DueDate` 小於兩天的工作訂單。 Database Mail 會使用 HTML 格式來傳送訊息。  
  
```  
DECLARE @tableHTML  NVARCHAR(MAX) ;  
  
SET @tableHTML =  
    N'<H1>Work Order Report</H1>' +  
    N'<table border="1">' +  
    N'<tr><th>Work Order ID</th><th>Product ID</th>' +  
    N'<th>Name</th><th>Order Qty</th><th>Due Date</th>' +  
    N'<th>Expected Revenue</th></tr>' +  
    CAST ( ( SELECT td = wo.WorkOrderID,       '',  
                    td = p.ProductID, '',  
                    td = p.Name, '',  
                    td = wo.OrderQty, '',  
                    td = wo.DueDate, '',  
                    td = (p.ListPrice - p.StandardCost) * wo.OrderQty  
              FROM AdventureWorks.Production.WorkOrder as wo  
              JOIN AdventureWorks.Production.Product AS p  
              ON wo.ProductID = p.ProductID  
              WHERE DueDate > '2004-04-30'  
                AND DATEDIFF(dd, '2004-04-30', DueDate) < 2   
              ORDER BY DueDate ASC,  
                       (p.ListPrice - p.StandardCost) * wo.OrderQty DESC  
              FOR XML PATH('tr'), TYPE   
    ) AS NVARCHAR(MAX) ) +  
    N'</table>' ;  
  
EXEC msdb.dbo.sp_send_dbmail @recipients='yourfriend@Adventure-Works.com',  
    @subject = 'Work Order List',  
    @body = @tableHTML,  
    @body_format = 'HTML' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [&#40;Transact-sql&#41;的 Database Mail 預存程式 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
