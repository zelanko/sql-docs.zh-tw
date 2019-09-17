---
title: 使用 SQL Server 針對一般 Database Mail 進行疑難排解 | Microsoft Docs
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
ms.openlocfilehash: 4ea44a55a7c58e64f327a97943481dfd63289324
ms.sourcegitcommit: 2da98f924ef34516f6ebf382aeb93dab9fee26c1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/03/2019
ms.locfileid: "70228428"
---
# <a name="general-database-mail-troubleshooting-steps"></a>Database Mail 疑難排解的一般步驟 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

若要針對 Database Mail 進行疑難排解，必須檢查下列 Database Mail 系統的一般區域。 這些程序是以邏輯順序來呈現，但您可以採用任何順序來進行評估。

## <a name="permissions"></a>權限

您必須是系統管理員固定伺服器角色的成員，才能針對 Database Mail 的各個方面進行疑難排解。 如果使用者不是系統管理員固定伺服器角色的成員，則只能取得他們嘗試傳送的電子郵件資訊，而無法取得由其他使用者傳送的電子郵件資訊。

## <a name="is-database-mail-enabled"></a>是否已啟用 Database Mail

1. 在 SQL Server Management Studio 中，使用查詢編輯器視窗連接至 SQL Server 的執行個體，然後執行下列程式碼：

    ```sql
    sp_configure 'show advanced', 1; 
    GO
    RECONFIGURE;
    GO
    sp_configure;
    GO
    ```

   在結果窗格中，確認 [Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) 的 run_value 設為 1。
   如果 run_value 不是 1，即未啟用 Database Mail。 為了降低惡意使用者可攻擊的功能數目，系統不會自動啟用 Database Mail。 如需詳細資訊，請參閱[了解介面區設定](../security/surface-area-configuration.md)。

1. 如果您認為啟用 Database Mail 是適當作法，請執行下列程式碼：

    ```sql
    sp_configure 'Database Mail XPs', 1; 
    GO
    RECONFIGURE;
    GO
    ```

1. 若要將 sp_configure 程序還原為預設狀態 (不顯示進階選項)，請執行下列程式碼：

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    ```sql 
    sp_configure 'show advanced', 0; 
    GO
    RECONFIGURE;
    GO
    ```

## <a name="are-users-properly-configured-to-send-mail"></a>是否已正確設定使用者以傳送郵件

1. 若要傳送 Database Mail，您必須是 msdb 資料庫的 DatabaseMailUserRole 資料庫角色成員。 系統管理員固定伺服器角色和 msdbdb_owner 角色的成員會自動歸屬為 DatabaseMailUserRole 角色成員。 若要列出 DatabaseMailUserRole 的所有其他成員，請執行下列陳述式：

    ```sql
    EXEC msdb.sys.sp_helprolemember 'DatabaseMailUserRole';
    ```

1. 若要將使用者新增至 DatabaseMailUserRole 角色，請使用下列陳述式：

    ```sql
    USE msdb;
    GO
    
    sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<database user>';
    ```

1. 若要傳送 Database Mail，使用者必須至少具備一個 Database Mail 設定檔的存取權。 若要列出使用者 (主體) 和他們可存取的設定檔，請執行下列陳述式。

    ```sql
    EXEC msdb.dbo.sysmail_help_principalprofile_sp;
    ```

1. 使用 [Database Mail 設定精靈] 建立設定檔，並將設定檔的存取權授與使用者。
 
## <a name="is-database-mail-started"></a>是否已啟動 Database Mail

1. 當有電子郵件訊息要處理時，就會啟動 [Database Mail 外部程式](database-mail-external-program.md)。 若在指定的逾時期限內沒有訊息需要傳送，程式就會結束。 若要確認 Database Mail 是否已啟動，請執行下列陳述式：

    ```sql
    EXEC msdb.dbo.sysmail_help_status_sp;
    ```
1. 如果未啟動 Database Mail 啟用作業，請執行下列陳述式來啟動：

    ```sql
    EXEC msdb.dbo.sysmail_start_sp;
    ```

1. 如果 Database Mail 外部程式已啟動，請使用下列陳述式檢查郵件佇列的狀態：

    ```sql
    EXEC msdb.dbo.sysmail_help_queue_sp @queue_type = 'mail';
    ```
  
   郵件佇列應該為 RECEIVES_OCCURRING 狀態。 狀態佇列會隨時間而變動。 如果郵件佇列狀態不是 RECEIVES_OCCURRING，請嘗試重新啟動佇列。 使用下列陳述式停止佇列：
   
```sql
EXEC msdb.dbo.sysmail_stop_sp;
```

然後，使用下列陳述式啟動佇列：

```sql
EXEC msdb.dbo.sysmail_start_sp;
```

  > [!NOTE]
  >  使用 sysmail_help_queue_sp 結果集中的長度資料行，來判斷郵件佇列中的電子郵件數目。

## <a name="do-problems-affect-some-or-all-accounts"></a>問題影響部分或所有的帳戶

1. 如果您判斷只有部分設定檔可以傳送郵件，那麼可能是使用這些問題設定檔的 Database Mail 帳戶有問題。 若要判斷哪些帳戶可以成功傳送郵件，請執行下列陳述式：

    ```sql
    SELECT sent_account_id, sent_date FROM msdb.dbo.sysmail_sentitems;
    ```

1. 如果無法運作的設定檔並未使用任何列出的帳戶，則可能是該設定檔的所有可用帳戶都無法正常運作。 若要測試個別帳戶，請使用 [Database Mail 設定精靈] 建立一個含單一帳戶的設定檔，然後使用新的帳戶從 [傳送測試電子郵件] 對話方塊來傳送電子郵件。 
1. 若要檢視 Database Mail 傳回的錯誤訊息，請執行下列陳述式：

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log;
    ```

   > [!NOTE]
   > 當郵件成功傳遞到 SMTP 郵件伺服器之後，Database Mail 即會將該郵件視為已傳送。 後續所發生的錯誤 (例如收件者的電子郵件地址無效) 仍可能導致郵件無法傳遞，但卻不會包含在 Database Mail 記錄中。

## <a name="retry-mail-delivery"></a>重試郵件傳遞

1. 如果您判斷 Database Mail 是因為無法穩定連接 SMTP 伺服器而失敗，您可以增加 Database Mail 嘗試傳送每則訊息的次數，來提高郵件的成功傳遞率。 請開啟 [Database Mail 設定精靈]，並選取 [檢視] 或變更系統參數選項。 或者，您也可以將多個帳戶與設定檔建立關聯，讓主要帳戶具有容錯移轉的機制，Database Mail 就可以使用容錯移轉帳戶來傳送電子郵件。
1. 在 [設定系統參數] 頁面上，[帳戶重試嘗試] 的預設值是五次，[帳戶重試延遲] 的預設值是 60 秒，這表示如果無法在 5 分鐘內連接 SMTP 伺服器，訊息傳遞就會失敗。 請增加這些參數，以延長訊息傳遞失敗前的時間。

    > [!NOTE]
    > 傳送大量訊息時，較大的預設值能提高穩定性，但當很多訊息一直重複嘗試傳遞時，也會大幅增加使用的資源。 若要處理根本問題，請解決導致 Database Mail 無法正常連絡 SMTP 伺服器的網路或 SMTP 伺服器問題。



##  <a name="RelatedContent"></a> 另請參閱
  
-   [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)  
  
-   [Database Mail 訊息物件](../../relational-databases/database-mail/database-mail-messaging-objects.md)  
  
-   [Database Mail 外部程式](../../relational-databases/database-mail/database-mail-external-program.md)  
  
-   [Database Mail 記錄與稽核](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
-   [設定 SQL Server Agent Mail 使用 Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
  
  
