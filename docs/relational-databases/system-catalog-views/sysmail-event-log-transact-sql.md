---
title: sysmail_event_log (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ac38c2e54fde2beb02e009e00b9f587e9265a43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759950"
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個由 Database Mail 系統傳回的 Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訊息，各包含一個資料列。 （在此內容中的訊息是指例如提供錯誤訊息，而不是電子郵件訊息的訊息）。設定**記錄層級**使用的參數**設定系統參數**對話方塊中的 Database Mail 組態精靈，或[sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)預存程序，以判斷傳回的訊息。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|記錄中項目的識別碼。|  
|**event_type**|**varchar(11)**|插入記錄中通知的類型。 可能的值有錯誤、警告、參考訊息、成功訊息和其他內部訊息。|  
|**log_date**|**datetime**|產生記錄項目的日期和時間。|  
|**description**|**nvarchar(max)**|記錄的訊息文字。|  
|**process_id**|**int**|Database Mail 外部程式的處理序識別碼。 這通常在每一次 Database Mail 外部程式啟動時都會變更。|  
|**mailitem_id**|**int**|郵件佇列中郵件項目的識別碼。 如果訊息與特定電子郵件項目無關，則為 NULL。|  
|**account_id**|**int**|**Account_id**與事件相關的帳戶。 如果訊息與特定帳戶無關，則為 NULL。|  
|**last_mod_date**|**datetime**|資料列上次修改的日期和時間。|  
|**last_mod_user**|**sysname**|上次修改資料列的使用者。 針對電子郵件，這是傳送郵件的使用者。 針對 Database Mail 外部程式產生的訊息，這是程式的使用者內容。|  
  
## <a name="remarks"></a>備註  
 當 Database Mail 進行疑難排解，搜尋**sysmail_event_log**電子郵件失敗的相關事件的檢視。 部分訊息 (如 Database Mail 外部程式失敗) 與特定電子郵件沒有關聯。 若要搜尋與特定電子郵件相關的錯誤，請查閱**mailitem_id**中失敗的電子郵件**sysmail_unsentitems**檢視，然後搜尋**sysmail_event_log**相關的訊息**mailitem_id**。 當從傳回的錯誤**sp_send_dbmail**、 電子郵件不會提交到 Database Mail 系統和錯誤不會顯示在此檢視。  
  
 當個別帳戶傳遞嘗試失敗時，Database Mail 會在重試嘗試期間保留錯誤訊息，直到郵件項目傳遞成功或失敗為止。 如果成功，所有累積的錯誤會記錄為個別的警告，包括**account_id**。 即使電子郵件已傳送，這仍可能會使警告出現。 如果最終傳遞失敗，所有先前的警告會記錄為一個錯誤訊息，而不需要**account_id**，因為所有的帳戶失敗。  
  
## <a name="permissions"></a>Permissions  
 您必須是隸屬**sysadmin**固定的伺服器角色或**DatabaseMailUserRole**可存取此檢視的資料庫角色。 成員**DatabaseMailUserRole**誰不屬於**sysadmin**角色，只能看到他們所提交的電子郵件的事件。  
  
## <a name="see-also"></a>另請參閱  
 [sysmail_faileditems &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [Database Mail 外部程式](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
