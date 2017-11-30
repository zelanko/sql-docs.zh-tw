---
title: "sysmail_unsentitems (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs: TSQL
helpviewer_keywords: sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85b7db39b03913b735ebde53571675fd9235a7e8
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailunsentitems-transact-sql"></a>sysmail_unsentitems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含一個資料列的每個 Database Mail 訊息**未傳送**或**重試**狀態。 未傳送或正在重試狀態的訊息仍存在郵件佇列中，隨時可能傳送。 訊息可以有**未傳送**狀態，原因如下：  
  
-   訊息是新的，雖然訊息已置於郵件佇列中，但 Database Mail 正在處理其他訊息而尚未到達這則訊息。  
  
-   Database Mail 外部程式未執行，且未傳送郵件。  
  
 訊息可以有**重試**狀態，原因如下：  
  
-   Database Mail 已嘗試傳送郵件，但無法連絡 SMTP 郵件伺服器。 Database Mail 會使用指派給傳送訊息之設定檔的其他 Database Mail 帳戶，繼續嘗試傳送訊息。 如果沒有帳戶可以傳送郵件，Database Mail 會等待設定的時間長度**帳戶重試延遲**參數然後再嘗試重新傳送訊息。 Database Mail 使用**帳戶重試嘗試**參數，來判斷多少次嘗試傳送訊息。 訊息保留**重試**只要 Database Mail 嘗試傳送訊息的狀態。  
  
 若要查看等候傳送的訊息數和其於郵件佇列中停留的時間，請使用這份檢視。 通常數目**未傳送**訊息將會很低。 在正常作業期間進行基準測試，可判斷作業之訊息佇列中的合理訊息數。  
  
 若要查看 Database Mail 處理的所有訊息，請使用[sysmail_allitems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). 若要查看只失敗狀態訊息，請使用[sysmail_faileditems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). 若要查看已傳送的訊息，請使用[sysmail_sentitems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|郵件佇列中郵件項目的識別碼。|  
|**profile_id**|**int**|用來提交訊息之設定檔的識別碼。|  
|**收件者**|**varchar(max)**|訊息收件者的電子郵件地址。|  
|**copy_recipients**|**varchar(max)**|訊息副本收件者的電子郵件地址。|  
|**blind_copy_recipients**|**varchar(max)**|名稱未顯示於訊息標頭之訊息副本收件者的電子郵件地址。|  
|**主體**|**nvarchar(510)**|訊息的主旨。|  
|**主體**|**varchar(max)**|訊息的主體。|  
|**body_format**|**varchar （20)**|訊息的主體格式。 可能的值為**文字**和**HTML**。|  
|**重要性**|**varchar(6)**|**重要性**訊息參數。|  
|**敏感度**|**varchar(12)**|**敏感度**訊息參數。|  
|**file_attachments**|**varchar(max)**|附加至電子郵件訊息中的檔案名稱清單，用分號分隔各檔案名稱。|  
|**attachment_encoding**|**varchar （20)**|郵件附加檔案的類型。|  
|**查詢**|**varchar(max)**|郵件程式執行的查詢。|  
|**execute_query_database**|**sysname**|郵件程式執行查詢所在的資料庫內容。|  
|**attach_query_result_as_file**|**bit**|當值是 0 時，查詢結果會包含在電子郵件訊息的主體中，在主體的內容之後。 當值是 1 時，會以附加檔案的方式傳回結果。|  
|**query_result_header**|**bit**|當值是 1 時，查詢結果會包含資料行標頭。 當值是 0 時，查詢結果不會包含資料行標頭。|  
|**query_result_width**|**int**|**Query_result_width**訊息參數。|  
|**query_result_separator**|**char （1)**|在查詢輸出中用來分隔資料行的字元。|  
|**exclude_query_output**|**bit**|**Exclude_query_output**訊息參數。 如需詳細資訊，請參閱[sp_send_dbmail &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|**Append_query_error**訊息參數。 0 表示如果查詢中有錯誤，則 Database Mail 不應傳送電子郵件訊息。|  
|**send_request_date**|**datetime**|訊息置於郵件佇列的日期和時間。|  
|**send_request_user**|**sysname**|提交訊息的使用者。 這不是 database mail 程序的使用者內容**從**訊息的欄位。|  
|**sent_account_id**|**int**|用來傳送訊息之 Database Mail 帳戶的識別碼。 針對這個檢視一律為 NULL。|  
|**sent_status**|**varchar(8)**|將**未傳送**如果 Database Mail 未嘗試傳送郵件。 將**重試**如果 Database Mail 無法傳送訊息，但是再試一次。|  
|**sent_date**|**datetime**|Database Mail 上次嘗試傳送郵件的日期和時間。 如果 Database Mail 未嘗試傳送訊息，則是 NULL。|  
|**last_mod_date**|**datetime**|資料列上次修改的日期和時間。|  
|**last_mod_user**|**sysname**|上次修改資料列的使用者。|  
  
## <a name="remarks"></a>備註  
 對 Database Mail 進行疑難排解時，這個檢視可藉顯示等候傳送的訊息數和訊息已等候的時間量，來幫助您識別問題的本質。 如果未傳送任何訊息，Database Mail 外部程式可能不在執行中，或者可能有使 Database Mail 無法連絡 SMTP 伺服器的網路問題。 許多未傳送的訊息都有相同**profile_id**，可能與 SMTP 伺服器問題。 請考慮將其他帳戶加入設定檔中。 如果正在傳送訊息，但訊息耗費太多時間在佇列中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能需要更多資源來處理需要的訊息量。  
  
## <a name="permissions"></a>Permissions  
 授與給**sysadmin**固定的伺服器角色和**DatabaseMailUserRole**資料庫角色。 成員執行時**sysadmin**固定伺服器角色，此檢視會顯示所有**未傳送**或**重試**訊息。 所有其他使用者只看**未傳送**或**重試**得到他們所提交的訊息。  
  
  
