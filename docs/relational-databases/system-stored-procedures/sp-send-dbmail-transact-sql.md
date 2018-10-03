---
title: sp_send_dbmail (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11b5d9c48c073d3a8208b9c8be1e73c5aa68e88e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075774"
---
# <a name="spsenddbmail-transact-sql"></a>sp_send_dbmail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將電子郵件訊息傳送給指定的收件者。 訊息可能包含查詢結果集、檔案附件，或兩者皆有。 當郵件順利放在 Database Mail 佇列中， **sp_send_dbmail**會傳回**mailitem_id**的訊息。 這個預存程序處於**msdb**資料庫。  
  
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
 [  **@profile_name=** ] **'***profile_name***'**  
 這是傳送訊息的來源設定檔名稱。 *Profile_name*別的**sysname**，預設值是 NULL。 *Profile_name*必須是現有 Database Mail 設定檔的名稱。 若未*profile_name*指定，則**sp_send_dbmail**使用目前使用者的預設私人設定檔。 如果使用者沒有預設私人設定檔， **sp_send_dbmail**使用的預設公用設定檔**msdb**資料庫。 如果使用者沒有預設私人設定檔，而且沒有資料庫中，沒有預設公用設定檔**@profile_name**必須指定。  
  
 [  **@recipients=** ] **'***收件者***'**  
 這是訊息所要送往的電子郵件地址清單，用分號分隔各個電子郵件地址。 收件者清單的類型是**varchar （max)**。 雖然這個參數是選擇性的至少其中一個**@recipients**， **@copy_recipients**，或**@blind_copy_recipients**必須指定，或**sp_send_dbmail**會傳回錯誤。  
  
 [  **@copy_recipients=** ] **'***copy_recipients***'**  
 這是訊息副本所要送往的電子郵件地址清單，用分號分隔各個電子郵件地址。 副本收件者清單的類型是**varchar （max)**。 雖然這個參數是選擇性的至少其中一個**@recipients**， **@copy_recipients**，或**@blind_copy_recipients**必須指定，或**sp_send_dbmail**會傳回錯誤。  
  
 [ **@blind_copy_recipients=** ] **'***blind_copy_recipients***'**  
 這是訊息密件副本所要送往的電子郵件地址清單，用分號分隔各個電子郵件地址。 密件副本收件者清單的類型是**varchar （max)**。 雖然這個參數是選擇性的至少其中一個**@recipients**， **@copy_recipients**，或**@blind_copy_recipients**必須指定，或**sp_send_dbmail**會傳回錯誤。  
  
 [ **@from_address=** ] **'***from_address***'**  
 這是電子郵件的 'from address' 值。 這是選擇性參數，用來覆寫郵件設定檔中的設定。 此參數的類型是**varchar （max)**。 SMTP 安全性設定會決定是否要接受這些覆寫。 如果沒有指定參數，預設值為 NULL。  
  
 [ **@reply_to=** ] **'***reply_to***'**  
 這是電子郵件的 'reply to address' 值。 它只接受一個電子郵件地址做為有效的值。 這是選擇性參數，用來覆寫郵件設定檔中的設定。 此參數的類型是**varchar （max)**。 SMTP 安全性設定會決定是否要接受這些覆寫。 如果沒有指定參數，預設值為 NULL。  
  
 [ **@subject=** ] **'***subject***'**  
 這是電子郵件訊息的主旨。 主旨的類型是**nvarchar(255)**。 如果未指定主旨，預設值便是「SQL Server 訊息」。  
  
 [ **@body=** ] **'***body***'**  
 這是電子郵件訊息的主體。 訊息主體的類型是**nvarchar （max)**，預設值是 NULL。  
  
 [ **@body_format=** ] **'***body_format***'**  
 這是訊息主體的格式。 參數的類型是**varchar （20)**，預設值是 NULL。 當指定這個選項時，會設定外寄訊息的標頭來表示訊息主體有指定的格式。 參數可包含下列各值之一：  
  
-   TEXT  
  
-   HTML  
  
 預設值是 TEXT。  
  
 [  **@importance=** ] **'***重要性***'**  
 這是訊息的重要性。 參數的類型是**varchar(6)**。 參數可包含下列各值之一：  
  
-   低  
  
-   一般  
  
-   高  
  
 預設值是 Normal。  
  
 [  **@sensitivity=** ] **'***敏感度***'**  
 這是訊息的敏感性。 參數的類型是**varchar(12)**。 參數可包含下列各值之一：  
  
-   一般  
  
-   Personal  
  
-   Private  
  
-   Confidential  
  
 預設值是 Normal。  
  
 [  **@file_attachments=** ] **'***file_attachments***'**  
 這是附加至電子郵件訊息中的檔案名稱清單，用分號分隔各檔案名稱。 清單中的檔案必須指定為絕對路徑。 附件清單的類型是**nvarchar （max)**。 根據預設，Database Mail 會將檔案附件限制為每個檔案 1 MB。  
  
 [  **@query=** ] **'***查詢***'**  
 這是要執行的查詢。 查詢的結果可以附加成一個檔案，也可以包含在電子郵件訊息的主體中。 查詢的類型是**nvarchar （max)**，而且可以包含任何有效[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。 請注意，查詢執行在不同的工作階段，因此指令碼呼叫中區域變數**sp_send_dbmail**不適用於查詢。  
  
 [ **@execute_query_database=** ] **'***execute_query_database***'**  
 這是預存程序執行查詢所在的資料庫內容。 參數的類型是**sysname**，預設值是目前的資料庫。 此參數才適用如果**@query**指定。  
  
 [ **@attach_query_result_as_file=** ] *attach_query_result_as_file*  
 指定是否以附加檔案的方式傳回查詢的結果集。 *attach_query_result_as_file*屬於型別**元**，預設值是 0。  
  
 值為 0 時，查詢結果包含電子郵件訊息的主體中的內容之後**@body**參數。 當值是 1 時，會以附加檔案的方式傳回結果。 此參數才適用如果**@query**指定。  
  
 [ **@query_attachment_filename=** ] *query_attachment_filename*  
 指定查詢附加檔案結果集使用的檔案名稱。 *query_attachment_filename*屬於型別**nvarchar(255)**，預設值是 NULL。 會忽略這個參數時*attach_query_result*為 0。 當*attach_query_result*為 1，且此參數是 NULL，Database Mail 會建立任意檔案名稱。  
  
 [ **@query_result_header=** ] *query_result_header*  
 指定查詢結果是否包含資料行標頭。 Query_result_header 屬於類型**元**。 當值是 1 時，查詢結果會包含資料行標頭。 當值是 0 時，查詢結果不會包含資料行標頭。 此參數的預設值**1**。 此參數才適用如果**@query**指定。  
 
   >[!NOTE]
   > 設定時，可能會發生下列錯誤@query_result_header為 0 且設定@query_no_truncate為 1:
   > <br> Msg 22050，層級 16，State 1，行 12： 無法初始化 sqlcmd 程式庫，錯誤號碼-2147024809。
  
 [ **@query_result_width** = ] *query_result_width*  
 這是以字元為單位的行寬，用來格式化查詢的結果。 *Query_result_width*別的**int**，預設值是 256。 提供的值必須介於 10 和 32767 之間。 此參數才適用如果**@query**指定。  
  
 [ **@query_result_separator=** ] **'***query_result_separator***'**  
 這是在查詢輸出中用來分隔資料行的字元。 分隔符號的類型是**char(1)**。 預設值是 ' ' (空白)。  
  
 [ **@exclude_query_output=** ] *exclude_query_output*  
 指定是否要在電子郵件中傳回查詢執行的輸出。 **exclude_query_output** bit，預設值是 0。 當此參數是 0 時，執行**sp_send_dbmail**預存程序會列印在主控台上執行查詢的結果傳回的訊息。 當此參數是 1，執行**sp_send_dbmail**預存程序不會列印任何查詢執行訊息在主控台上。  
  
 [ **@append_query_error=** ] *append_query_error*  
 指定是否要在指定的查詢所傳回的錯誤時，傳送電子郵件**@query**引數。 **append_query_error**已**元**，預設值是 0。 當這個參數是 1 時，Database Mail 會傳送電子郵件，且會在電子郵件的主體中包含查詢錯誤訊息。 此參數為 0 時，Database Mail 不會傳送電子郵件訊息，並**sp_send_dbmail**結束，傳回碼 1，表示失敗。  
  
 [ **@query_no_truncate=** ] *query_no_truncate*  
 指定是否要執行之查詢的選項來避免截斷大型變數長度資料類型 (**varchar （max)**， **nvarchar （max)**， **varbinary （max)****xml**，**文字**， **ntext**，**映像**，以及使用者定義資料類型)。 若有設定，查詢結果不包含資料行標頭。 *Query_no_truncate*的值為類型**元**。 當此值是 0 或未指定時，查詢中的資料行會截斷為 256 個字元。 當此值是 1 時，不會截斷查詢中的資料行。 這個參數的預設值是 0。  
  
> [!NOTE]  
>  當搭配大量資料，@**query_no_truncate**選項會耗用其他資源並減慢伺服器效能。  
  
 [ **@query_result_no_padding** ] *@query_result_no_padding*  
 此類型為 bit。 預設值是 0。 當您設定為 1 時，查詢結果未開啟填補時，可能會減少檔案大小。如果您設定@query_result_no_padding為 1，而且設定@query_result_width參數@query_result_no_padding參數會覆寫@query_result_width參數。  
  
 在此情況下，不會發生任何錯誤。  
 
  >[!NOTE]
  > 設定時，可能會發生下列錯誤@query_result_no_padding1 」 和 「 提供的參數 @query_no_truncate:
  > <br> Msg 22050，第 0 層級 16，State 1，行： 無法執行查詢，因為@query_result_no_append和@query_no_truncate選項互斥。 
  
 如果您設定@query_result_no_padding為 1，而且設定@query_no_truncate參數，發生錯誤，就會引發。  
  
 [  **@mailitem_id=** ] *mailitem_id* [輸出]  
 選擇性輸出參數傳回*mailitem_id*的訊息。 *Mailitem_id*別的**int**。  
  
## <a name="return-code-values"></a>傳回碼值  
 傳回碼為 0 表示成功。 其他任何值都表示失敗。 失敗的陳述式的錯誤程式碼會儲存在 @@ERROR變數。  
  
## <a name="result-sets"></a>結果集  
 成功時，傳回「郵件已列入佇列」訊息。  
  
## <a name="remarks"></a>備註  
 使用之前，Database Mail 才能使用 Database Mail 組態精靈 中，或是**sp_configure**。  
  
 **sysmail_stop_sp**外部程式使用的 Service Broker 物件來停止 Database Mail。 **sp_send_dbmail** Database Mail 已停止使用時，仍接受郵件**sysmail_stop_sp**。 若要啟動 Database Mail，請使用**sysmail_start_sp**。  
  
 當**@profile**未指定，則**sp_send_dbmail**會使用預設設定檔。 如果傳送電子郵件訊息的使用者有預設私人設定檔，Database Mail 會使用這個設定檔。 如果使用者沒有預設私人設定檔**sp_send_dbmail**會使用預設公用設定檔。 如果沒有使用者沒有預設私人設定檔，而且沒有預設公用設定檔**sp_send_dbmail**會傳回錯誤。  
  
 **sp_send_dbmail**不支援沒有內容的電子郵件訊息。 若要傳送電子郵件訊息，您必須指定至少一個**@body**， **@query**， **@file_attachments**，或 **@subject**. 否則，請**sp_send_dbmail**會傳回錯誤。  
  
 Database Mail 利用目前使用者的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 安全性內容來控制檔案的存取。 因此，對於使用經過驗證的使用者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證將使用的檔案無法附加**@file_attachments**。 Windows 不允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在遠端電腦之間提供認證。 因此，從執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦以外的電腦執行命令時，Database Mail 可能無法從網路共用附加檔案。  
  
 如果兩個**@query**並**@file_attachments**指定且找不到檔案，仍會執行查詢，但不是會傳送電子郵件。  
  
 當指定查詢時，結果集會格式化為內嵌文字。 結果中的二進位資料會以十六進位格式傳送。  
  
 參數**@recipients**， **@copy_recipients**，以及**@blind_copy_recipients**是以分號分隔的電子郵件地址的清單。 必須提供至少其中一個參數，或**sp_send_dbmail**會傳回錯誤。  
  
 執行時**sp_send_dbmail**沒有交易內容中，Database Mail 會啟動並認可隱含交易。 執行時**sp_send_dbmail**從現有的交易，在 Database Mail 依賴使用者來認可或回復任何變更。 它並不會啟動內部交易。  
  
## <a name="permissions"></a>Permissions  
 執行權限**sp_send_dbmail**的所有成員的預設**DatabaseMailUser**中的資料庫角色**msdb**資料庫。 不過，當傳送訊息的使用者沒有權限要求，使用設定檔**sp_send_dbmail**傳回錯誤，而且不會傳送訊息。  
  
## <a name="examples"></a>範例  
  
### <a name="a-sending-an-e-mail-message"></a>A. 傳送電子郵件訊息  
 這個範例會將電子郵件訊息傳送給您電子郵件地址的好友`myfriend@Adventure-Works.com`。 訊息的主旨是 `Automated Success Message`。 訊息的主體包含 `'The stored procedure finished successfully'` 這個句子。  
  
```  
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'Adventure Works Administrator',  
    @recipients = 'yourfriend@Adventure-Works.com',  
    @body = 'The stored procedure finished successfully.',  
    @subject = 'Automated Success Message' ;  
```  
  
### <a name="b-sending-an-e-mail-message-with-the-results-of-a-query"></a>B. 利用查詢結果傳送電子郵件訊息  
 這個範例會將電子郵件訊息傳送給您電子郵件地址的好友`yourfriend@Adventure-Works.com`。 訊息的主旨是 `Work Order Count`，且會執行查詢來顯示在 2004 年 4 月 30 日之後 `DueDate` 小於兩天的工作訂單數目。 Database Mail 會將結果附加為一個文字檔。  
  
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
 這個範例會將電子郵件訊息傳送給您電子郵件地址的好友`yourfriend@Adventure-Works.com`。 訊息的主旨是 `Work Order List`，且包含一份 HTML 文件，其中顯示在 2004 年 4 月 30 日之後 `DueDate` 小於兩天的工作訂單。 Database Mail 會使用 HTML 格式來傳送訊息。  
  
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
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
  
