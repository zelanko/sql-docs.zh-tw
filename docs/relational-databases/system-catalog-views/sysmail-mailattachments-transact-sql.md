---
title: "sysmail_mailattachments (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_mailattachments_TSQL
- sysmail_mailattachments
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_mailattachments database mail view
ms.assetid: aee87059-a4c1-459a-a95c-641b4e3f0e73
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 028ecfcb41a46c1a218d63fcb298dd2af9719678
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailmailattachments-transact-sql"></a>sysmail_mailattachments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個提交到 Database Mail 的附加檔案，各包含一個資料列。 當您想要 Database Mail 附加檔案的相關資訊時，請使用這份檢視。 若要檢閱 Database Mail 使用所處理的所有電子郵件[sysmail_allitems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md).  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**attachment_id**|**int**|附加檔案的識別碼。|  
|**mailitem_id**|**int**|包含附加檔案之郵件項目的識別碼。|  
|**filename**|**nvarchar(520)**|附加檔案的檔案名稱。 當**attach_query_result**為 1 和**query_attachment_filename**是 NULL 時，Database Mail 會建立任意檔案名稱。|  
|**filesize**|**int**|附加檔案的大小 (以位元組為單位)。|  
|**attachment**|**varbinary(max)**|附加檔案的內容。|  
|**last_mod_date**|**datetime**|資料列上次修改的日期和時間。|  
|**last_mod_user**|**sysname**|上次修改資料列的使用者。|  
  
## <a name="remarks"></a>備註  
 對 Database Mail 進行疑難排解時，請使用這個檢視來查看附加檔案的屬性。  
  
 附件儲存在系統資料表中可能會導致**msdb**資料庫成長。 使用**sysmail_delete_mailitems_sp**刪除郵件項目和其關聯的附加檔案。 如需詳細資訊，請參閱[建立封存 Database Mail 訊息和事件記錄檔的 SQL Server Agent 作業](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)。  
  
## <a name="permissions"></a>Permissions  
 授與給**sysadmin**固定的伺服器角色和**DatabaseMailUserRole**資料庫角色。 成員執行時**sysadmin**固定伺服器角色，此檢視會顯示所有的附件。 所有其他使用者只看得到他們所提交訊息的附加檔案。  
  
## <a name="see-also"></a>另請參閱  
 [sysmail_allitems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [sysmail_sentitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)   
 [sysmail_unsentitems &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)  
  
  
