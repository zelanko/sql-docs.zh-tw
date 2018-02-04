---
title: "sysmail_event_log (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9dca8c14d7ea9fefbe566d7f0770b395df48bf25
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個由 Database Mail 系統傳回的 Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訊息，各包含一個資料列。 (這個內容中的訊息指的是錯誤訊息之類的訊息，不是電子郵件訊息。) 設定**記錄層級**參數使用**設定系統參數**Database Mail 組態精靈 對話方塊或[sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)預存程序，以判斷傳回的訊息。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|記錄中項目的識別碼。|  
|**event_type**|**varchar(11)**|插入記錄中通知的類型。 可能的值有錯誤、警告、參考訊息、成功訊息和其他內部訊息。|  
|**log_date**|**datetime**|產生記錄項目的日期和時間。|  
|**描述**|**nvarchar(max)**|記錄的訊息文字。|  
|**process_id**|**int**|Database Mail 外部程式的處理序識別碼。 這通常在每一次 Database Mail 外部程式啟動時都會變更。|  
|**mailitem_id**|**int**|郵件佇列中郵件項目的識別碼。 如果訊息與特定電子郵件項目無關，則為 NULL。|  
|**account_id**|**int**|**Account_id**與事件相關的帳戶。 如果訊息與特定帳戶無關，則為 NULL。|  
|**last_mod_date**|**datetime**|資料列上次修改的日期和時間。|  
|**last_mod_user**|**sysname**|上次修改資料列的使用者。 針對電子郵件，這是傳送郵件的使用者。 針對 Database Mail 外部程式產生的訊息，這是程式的使用者內容。|  
  
## <a name="remarks"></a>備註  
 當 Database Mail 進行疑難排解，搜尋**sysmail_event_log**電子郵件失敗的相關事件檢視。 部分訊息 (如 Database Mail 外部程式失敗) 與特定電子郵件沒有關聯。 若要搜尋特定電子郵件相關的錯誤，查閱**mailitem_id**中失敗的電子郵件的**sysmail_faileditems**檢視，然後搜尋**sysmail_event_log**訊息相關的**mailitem_id**。 從傳回的錯誤時**sp_send_dbmail**、 電子郵件不會提交到 Database Mail 系統和錯誤不會顯示在此檢視。  
  
 當個別帳戶傳遞嘗試失敗時，Database Mail 會在重試嘗試期間保留錯誤訊息，直到郵件項目傳遞成功或失敗為止。 如果最終成功，所有累積的錯誤會記錄為個別的警告包括**account_id**。 即使電子郵件已傳送，這仍可能會使警告出現。 如果最終傳遞失敗，所有先前的警告會記錄一個錯誤訊息，但為**account_id**，因為所有的帳戶失敗。  
  
## <a name="permissions"></a>Permissions  
 您必須是成員**sysadmin**固定的伺服器角色或**DatabaseMailUserRole**來存取此檢視的資料庫角色。 成員**DatabaseMailUserRole**人員不屬於**sysadmin**角色，只能看到他們所提交的電子郵件的事件。  
  
## <a name="see-also"></a>另請參閱  
 [sysmail_faileditems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Database Mail 外部程式](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
