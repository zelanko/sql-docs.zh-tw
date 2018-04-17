---
title: sysmail_faileditems (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_faileditems
- sysmail_faileditems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_faileditems database mail view
ms.assetid: a31562c5-358e-4cfc-a72d-b3faccc53851
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c156558b782eef8dc2ef76f06a012d3d6cd4967c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailfaileditems-transact-sql"></a>sysmail_faileditems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個 Database Mail 訊息**失敗**狀態。 使用這份檢視可判斷哪些訊息未成功傳送。  
  
 若要查看 Database Mail 處理的所有訊息，請使用[sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)。 若要查看未傳送的訊息，請使用[sysmail_unsentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)。 若要查看已傳送的訊息，請使用[sysmail_sentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)。 若要檢視電子郵件附件，請使用[sysmail_mailattachments &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|郵件佇列中郵件項目的識別碼。|  
|**profile_id**|**int**|用來提交訊息之設定檔的識別碼。|  
|**收件者**|**varchar(max)**|訊息收件者的電子郵件地址。|  
|**copy_recipients**|**varchar(max)**|訊息副本收件者的電子郵件地址。|  
|**blind_copy_recipients**|**varchar(max)**|名稱未顯示於訊息標頭之訊息副本收件者的電子郵件地址。|  
|**subject**|**nvarchar(510)**|訊息的主旨。|  
|**主體**|**varchar(max)**|訊息的主體。|  
|**body_format**|**varchar(20)**|訊息的主體格式。 可能的值是 TEXT 和 HTML。|  
|**重要性**|**varchar(6)**|**重要性**訊息參數。|  
|**敏感度**|**varchar(12)**|**敏感度**訊息參數。|  
|**file_attachments**|**varchar(max)**|附加至電子郵件訊息中的檔案名稱清單，用分號分隔各檔案名稱。|  
|**Attachment_encoding**|**varchar(20)**|郵件附加檔案的類型。|  
|**查詢**|**varchar(max)**|郵件程式執行的查詢。|  
|**execute_query_database**|**sysname**|郵件程式執行查詢所在的資料庫內容。|  
|**attach_query_result_as_file**|**bit**|當值是 0 時，查詢結果會包含在電子郵件訊息的主體中，在主體的內容之後。 當值是 1 時，會以附加檔案的方式傳回結果。|  
|**query_result_header**|**bit**|當值是 1 時，查詢結果會包含資料行標頭。 當值是 0 時，查詢結果不會包含資料行標頭。|  
|**query_result_width**|**int**|**Query_result_width**訊息參數。|  
|**query_result_separator**|**char(1)**|在查詢輸出中用來分隔資料行的字元。|  
|**exclude_query_output**|**bit**|**Exclude_query_output**訊息參數。 如需詳細資訊，請參閱[sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。|  
|**append_query_error**|**bit**|**Append_query_error**訊息參數。 0 表示如果查詢中有錯誤，則 Database Mail 不應傳送電子郵件訊息。|  
|**send_request_date**|**datetime**|訊息置於郵件佇列的日期和時間。|  
|**send_request_user**|**sysname**|提交訊息的使用者。 這是 Database Mail 程序的使用者內容，不是訊息的「寄件者:」欄位。|  
|**sent_account_id**|**int**|用來傳送訊息之 Database Mail 帳戶的識別碼。 針對這個檢視一律為 NULL。|  
|**sent_status**|**varchar(8)**|郵件的狀態。 一律**失敗**此檢視。|  
|**sent_date**|**datetime**|訊息從郵件佇列中移除的日期和時間。|  
|**last_mod_date**|**datetime**|資料列上次修改的日期和時間。|  
|**last_mod_user**|**sysname**|上次修改資料列的使用者。|  
  
## <a name="remarks"></a>備註  
 使用**sysmail_faileditems**檢視可查看 Database Mail 未傳送的訊息時。 對 Database Mail 進行疑難排解時，這個檢視可藉顯示未傳送訊息的屬性，來幫助您識別問題的本質。 若要檢視失敗的原因，請參閱失敗的訊息中的項目[sysmail_event_log &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)檢視。  
  
## <a name="permissions"></a>Permissions  
 授與給**sysadmin**固定的伺服器角色和**databasemailuserrole**資料庫角色。 成員執行時**sysadmin**固定伺服器角色，此檢視會顯示所有失敗的訊息。 所有其他使用者只看得到他們所提交的失敗訊息。  
  
  
