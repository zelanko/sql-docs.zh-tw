---
title: Database Mail：郵件已排入佇列中，但未傳遞| Microsoft Docs
ms.custom: ''
ms.date: 04/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 92ff867d98b83f1934972a576df8295c3f9ca79d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "70228417"
---
# <a name="database-mail-mail-queued-not-delivered"></a>Database Mail：郵件已排入佇列中，未傳遞 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

本主題說明如何對電子郵件訊息已成功排入佇列但訊息並未傳遞的問題，進行疑難排解。

## <a name="diagnose-the-problem"></a>診斷問題 

Database Mail 外部程式會將電子郵件活動記錄在 **msdb** 資料庫中。

首先，若要確認是否已啟用 Database Mail，請使用 **sp_configure** 系統預存程序的 [Database Mail XP 選項](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)，如下例所示：

```sql 
EXEC sp_configure 'show advanced', 1;  
RECONFIGURE; 
EXEC sp_configure; 
GO
```

接著，請在 **msdb** 資料庫中執行下列陳述式，以便檢查郵件佇列的狀態：

```sql
sysmail_help_queue_sp @queue_type = 'Mail' ;
```

如需資料行的詳細說明，請參閱 [sysmail_help_queue_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-queue-sp-transact-sql.md#result-set)。

檢查 **sysmail_event_log** 檢視中是否有活動。 檢視應該包含一個項目，說明已經啟動了 Database Mail 外部程式。 如果 **sysmail_event_log** 檢視中沒有項目，請參閱徵兆[訊息已排入佇列，但 **sysmail_event_log** 中沒有項目](database-mail-common-errors.md#database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log)。 如果 **sysmail_event_log** 檢視中有錯誤，請針對特定錯誤進行疑難排解。

如果 **sysmail_event_log** 檢視中有項目，請檢查 **sysmail_allitems** 檢視以取得訊息的狀態。

## <a name="message-status-unsent"></a>訊息狀態未傳送 

狀態為**未傳送**表示 [Database Mail 外部程式](database-mail-external-program.md)尚未處理電子郵件訊息。 Database Mail 外部程式可能已經在處理訊息時落後；外部程式處理訊息的速率取決於網路狀況、重試逾時、訊息量，以及 SMTP 伺服器的容量。 如果問題持續存在，請考慮使用多個設定檔，將訊息散發於多個 SMTP 伺服器。

檢查最近修改日期，以取得成功傳遞的訊息。 如果上次的成功傳遞已經過好一陣子，請檢查 sysmail_event_log 檢視，驗證 Service Broker 是否成功啟動外部程式。 如果上次嘗試並未啟動外部程式，請確認 Database Mail 外部程式是否位於正確目錄，且 SQL Server 服務帳戶是否具有執行可執行檔的權限。

   > [!NOTE]
   > 若要刪除舊的未傳送訊息，請先等到無法傳遞的訊息成為佇列中最舊訊息後，再使用 [sysmail_delete_mailitems_sp](../system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) 刪除它們。

## <a name="message-status-retrying"></a>訊息狀態正在重試

狀態為「正在重試」表示 Database Mail 已嘗試，但無法將訊息傳遞至 SMTP 伺服器。 這通常是由網路干擾、SMTP 伺服器失敗或 Database Mail 帳戶設定不正確所造成。 不論訊息最後傳遞成敗與否，都會張貼一份訊息至事件記錄檔中。

## <a name="message-status-sent"></a>訊息狀態已傳送

狀態為**已傳送**表示 Database Mail 外部程式已順利地將電子郵件訊息傳遞至 SMTP 伺服器。 如果訊息並未到達目的地，SMTP 伺服器會接受來自 Database Mail 的訊息，但是沒有將訊息傳遞給最終收件者。 檢查 SMTP 伺服器的記錄檔，或連絡 SMTP 伺服器的系統管理員。 您也可以使用其他用戶端 (如 Outlook Express) 來測試 SMTP 郵件伺服器。

## <a name="message-status-failed"></a>訊息狀態失敗

狀態為失敗，表示 Database Mail 外部程式無法將訊息傳遞至 SMTP 伺服器。 在此情況下，**sysmail_event_log** 檢視會包含來自外部程式的詳細資訊。 如需聯結 **sysmail_faileditems** 和 **sysmail_event_log** 以擷取詳細錯誤訊息的範例查詢，請參閱[檢查使用 Database Mail 傳送之電子郵件訊息的狀態](check-the-status-of-e-mail-messages-sent-with-database-mail.md)。 最常見的失敗原因是目的地位址不正確，或網路發生問題而使外部程式無法到達一或多個容錯移轉帳戶。 SMTP 伺服器的問題也會導致該伺服器拒絕郵件。 請使用 [Database Mail 設定精靈]，將 [記錄層級]  變更為 [詳細資訊]  ，然後傳送測試郵件來調查失敗點。



##  <a name="RelatedContent"></a> 另請參閱
  
-  [Database Mail 概觀](database-mail.md)

  
  
