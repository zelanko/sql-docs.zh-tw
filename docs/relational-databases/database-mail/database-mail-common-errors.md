---
title: 使用 Database Mail 的常見錯誤 | Microsoft Docs
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
ms.openlocfilehash: ee5e7fd6511a624b05b4d6c7d03c1f2dcd288054
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288022"
---
# <a name="common-errors-with-database-mail"></a>使用 Database Mail 的常見錯誤 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

本文描述使用 Database Mail 及其解決方案時會發生的一些常見錯誤。

## <a name="could-not-find-stored-procedure-sp_send_dbmail"></a>找不到預存程序 'sp_send_dbmail'
[sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) 預存程序已安裝在 msdb 資料庫。 您必須從 msdb 資料庫執行 **sp_send_dbmail**，或為預存程序指定三段式名稱。

範例：
```sql
EXEC msdb.dbo.sp_send_dbmail ...
```

或：

```sql
USE msdb;
GO
EXEC dbo.sp_send_dbmail ...
```

使用 [Database Mail 設定精靈](configure-database-mail.md)啟用及設定 Database Mail。

## <a name="profile-not-valid"></a>設定檔無效
此訊息有兩個可能原因。 指定的設定檔不存在，或執行 [sp_send_dbmail (Transact-SQL)](../system-stored-procedures/sp-send-dbmail-transact-sql.md) 的使用者無權存取設定檔。

若要檢查設定檔的權限，請使用設定檔名稱執行預存程序 [sysmail_help_principalprofile_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md)。 使用預存程序 [sysmail_add_principalprofile_sp (Transact-SQL)](../system-stored-procedures/sysmail-help-principalprofile-sp-transact-sql.md) 或 [Database Mail 設定精靈](configure-database-mail.md)授與 msdb 使用者或群組存取設定檔的權限。

## <a name="permission-denied-on-sp_send_dbmail"></a>sp_send_dbmail 拒絕權限

此主題描述如何針對嘗試傳送 Database Mail 之使用者沒有權限執行 sp_send_dbmail 的錯誤訊息進行疑難排解。

錯誤文字是：

```
EXECUTE permission denied on object 'sp_send_dbmail', 
database 'msdb', schema 'dbo'.
```

若要傳送 Database Mail，使用者必須是 msdb 資料庫中的使用者，且為 msdb 資料庫中 DatabaseMailUserRole 資料庫角色的成員。 若要將 msdb 使用者或群組新增至此角色，請使用 SQL Server Management Studio 或對需要傳送 Database Mail 的使用者或角色執行下列陳述式。

```sql
EXEC msdb.dbo.sp_addrolemember @rolename = 'DatabaseMailUserRole'
    ,@membername = '<user or role name>';
GO
```
如需詳細資訊，請參閱 [sp_addrolemember](../system-stored-procedures/sp-addrolemember-transact-sql.md) 和 [sp_droprolemember](../system-stored-procedures/sp-droprolemember-transact-sql.md)。

## <a name="database-mail-queued-no-entries-in-sysmail_event_log-or-windows-application-event-log"></a>Database Mail 已排入佇列，sysmail_event_log 或 Windows 應用程式事件記錄檔中沒有項目 

Database Mail 依賴 Service Broker 佇列電子郵件訊息。 如已停止 Database Mail，或如果未在 **msdb** 資料庫中啟動 Service Broker 訊息傳遞，則 Database Mail 會將訊息佇列於資料庫中，但無法傳遞訊息。 在此情況下，Service Broker 訊息會保留在 Service Broker 郵件佇列中。 Service Broker 不啟動外部程式，因此 **sysmail_event_log** 中沒有項目，且 **sysmail_allitems** 與相關檢視中的項目狀態不會更新。

執行下列陳述式，檢查 **msdb** 資料庫中是否啟用 Service Broker：

```sql
SELECT is_broker_enabled FROM sys.databases WHERE name = 'msdb';
```

0 值表示 msdb 資料庫未啟動 Service Broker 訊息傳遞。 若要修正此問題，請使用下列 TRANSACT-SQL 命令在資料庫中啟動 Service Broker：

```sql
USE master ;
GO

ALTER DATABASE msdb SET ENABLE_BROKER ;
GO
``` 

Database Mail 仰賴許多內部預存程序。 為降低介面區，安裝新的 SQL Server 時會停用這些預存程序。 若要啟用這些預存程序，請使用 **sp_configure** 系統預存程序的 [Database Mail XP 選項](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)，如下例所示：

```sql
EXEC sp_configure 'show advanced options', 1;  
RECONFIGURE;
EXEC sp_configure 'Database Mail XPs', 1;  
RECONFIGURE  
GO  

Database Mail may be stopped in the **msdb** database. To check status of Database Mail, execute the following statement:

```sql
EXECUTE dbo.sysmail_help_status_sp;
```

若要在郵件主機資料庫中啟動 Database Mail，請在 msdb 資料庫中執行下列命令：

```sql
EXECUTE dbo.sysmail_start_sp;
```

Service Broker 會在啟動時檢查訊息的對話存留時間，因此任何已在 Service Broker 傳輸佇列的訊息，只要其存留時間比設定的對話存留時間還要長，就會立即失敗。 Database Mail 會更新 [sysmail_allitems](../system-catalog-views/sysmail-allitems-transact-sql.md) 與相關檢視中的失敗訊息狀態。 您必須判斷是否再次傳送電子郵件訊息。 如需設定 Database Mail 使用的對話方塊存留時間詳細資訊，請參閱 [sysmail_configure_sp (Transact-SQL)](../system-stored-procedures/sysmail-configure-sp-transact-sql.md)。



##  <a name="RelatedContent"></a> 另請參閱
  
-  [Database Mail 概觀](database-mail.md)
-  [建立 Database Mail 設定檔](create-a-database-mail-profile.md)
  
  
