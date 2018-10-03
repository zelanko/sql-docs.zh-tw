---
title: sysmail_allitems (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_allitems_TSQL
- sysmail_allitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_allitems database mail view
ms.assetid: 21fb8432-7677-4435-902f-64a58bba4cbb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 65c96ade0964146e1d8ff9cfa52f99938d290712
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824846"
---
# <a name="sysmailallitems-transact-sql"></a>sysmail_allitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個 Database Mail 處理的訊息，各包含一個資料列。 當您想要查看所有訊息的狀態時，請使用這份檢視。  
  
 若要查看失敗狀態的訊息，請使用[sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)。 若要查看未傳送的訊息，請使用[sysmail_unsentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)。 若要查看已傳送的訊息，請使用[sysmail_sentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|郵件佇列中郵件項目的識別碼。|  
|**profile_id**|**int**|用來傳送訊息之設定檔的識別碼。|  
|**收件者**|**varchar(max)**|訊息收件者的電子郵件地址。|  
|**copy_recipients**|**varchar(max)**|訊息副本收件者的電子郵件地址。|  
|**blind_copy_recipients**|**varchar(max)**|名稱未顯示於訊息標頭之訊息副本收件者的電子郵件地址。|  
|**subject**|**nvarchar(510)**|訊息的主旨。|  
|**內文**|**varchar(max)**|訊息的主體。|  
|**body_format**|**varchar(20)**|訊息的主體格式。 可能的值是 TEXT 和 HTML。|  
|**重要性**|**varchar(6)**|**重要性**訊息參數。|  
|**敏感度**|**varchar(12)**|**敏感度**訊息參數。|  
|**file_attachments**|**varchar(max)**|附加至電子郵件訊息中的檔案名稱清單，用分號分隔各檔案名稱。|  
|**attachment_encoding**|**varchar(20)**|郵件附加檔案的類型。|  
|**查詢**|**varchar(max)**|郵件程式執行的查詢。|  
|**execute_query_database**|**sysname**|郵件程式執行查詢所在的資料庫內容。|  
|**attach_query_result_as_file**|**bit**|當值是 0 時，查詢結果會包含在電子郵件訊息的主體中，在主體的內容之後。 當值是 1 時，會以附加檔案的方式傳回結果。|  
|**query_result_header**|**bit**|當值是 1 時，查詢結果會包含資料行標頭。 當值是 0 時，查詢結果不會包含資料行標頭。|  
|**query_result_width**|**int**|**Query_result_width**訊息參數。|  
|**query_result_separator**|**char(1)**|在查詢輸出中用來分隔資料行的字元。|  
|**exclude_query_output**|**bit**|**Exclude_query_output**訊息參數。 如需詳細資訊，請參閱 < [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。|  
|**append_query_error**|**bit**|**Append_query_error**訊息參數。 0 表示如果查詢中有錯誤，則 Database Mail 不應傳送電子郵件訊息。|  
|**send_request_date**|**datetime**|訊息置於郵件佇列的日期和時間。|  
|**send_request_user**|**sysname**|提交訊息的使用者。 這是 Database Mail 程序的使用者內容，不是訊息的「寄件者:」欄位。|  
|**sent_account_id**|**int**|用來傳送訊息之 Database Mail 帳戶的識別碼。|  
|**sent_status**|**varchar(8)**|郵件的狀態。 可能的值為：<br /><br /> **傳送**-郵件已傳送。<br /><br /> **未傳送**-Database mail 仍在嘗試傳送訊息。<br /><br /> **重試**-Database Mail 無法傳送訊息，但正在嘗試重新傳送它。<br /><br /> **失敗**-Database mail 無法傳送訊息。|  
|**sent_date**|**datetime**|訊息傳送的日期和時間。|  
|**last_mod_date**|**datetime**|資料列上次修改的日期和時間。|  
|**last_mod_user**|**sysname**|上次修改資料列的使用者。|  
  
## <a name="remarks"></a>備註  
 使用**sysmail_allitems**由 Database Mail 處理的檢視，以查看所有訊息的狀態。 對 Database Mail 進行疑難排解時，這份檢視可藉顯示已傳送訊息和未傳送訊息的屬性比較，來幫助您識別問題的本質。  
  
 這份檢視所公開的系統資料表包含所有訊息，可能會造成**msdb**資料庫成長。 請定期從檢視刪除舊訊息，以減少資料表大小。 如需詳細資訊，請參閱 <<c0> [ 建立的 SQL Server Agent 作業，以封存 Database Mail 訊息和事件記錄檔](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)。  
  
## <a name="permissions"></a>Permissions  
 若要授與**sysadmin**固定的伺服器角色並**DatabaseMailUserRole**資料庫角色。 成員執行時**sysadmin**固定伺服器角色，此檢視會顯示所有訊息。 所有其他使用者只看得到他們所提交的訊息。  
  
  
