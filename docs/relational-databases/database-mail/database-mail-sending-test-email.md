---
title: 使用 Database Mail 傳送測試電子郵件 | Microsoft Docs
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
ms.openlocfilehash: a689daf33baece845ddf81c09b99fc61c96509a2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726501"
---
# <a name="send-a-test-email-with-database-mail"></a>使用 Database Mail 傳送測試電子郵件  
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

使用 [傳送測試電子郵件] 對話方塊測試使用特定設定檔傳送郵件的功能。

## <a name="permissions"></a>權限

您必須是系統管理員固定伺服器角色的成員，才能使用 [傳送測試電子郵件] 對話方塊。 非系統管理員固定伺服器角色成員的使用者，可以使用 [sp_send_dbmail](../system-stored-procedures/sp-send-dbmail-transact-sql.md) 程序來測試 Database Mail。

## <a name="procedure"></a>程序

1. 在 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 中使用 [物件總管]，連接到已設定 Database Mail 的 SQL Server 資料庫引擎執行個體，展開 [管理]，以滑鼠右鍵按一下 [Database Mail]，然後選取 [傳送測試電子郵件]。 如果 Database Mail 設定檔不存在，會出現一個對話方塊提示使用者建立設定檔，並開啟 [Database Mail 設定精靈]。
1. 從 [<instance name>] 對話方塊的 [傳送測試電子郵件] 中，在 [Database Mail 設定檔] 方塊中選取您要測試的設定檔。
1. 在 [收件者]  方塊中，鍵入測試電子郵件的收件者電子郵件名稱。
1. 在 [主旨]  方塊中，鍵入測試電子郵件的主旨列。 變更預設的主旨，以便識別您的電子郵件來進行疑難排解。
1. 在 [本文]  方塊中，鍵入測試電子郵件的本文。 變更預設的主旨，以便識別您的電子郵件來進行疑難排解。
1. 選取 [傳送測試電子郵件]  將測試電子郵件傳送到 Database Mail 佇列。
1. 傳送測試電子郵件會開啟 [Database Mail 測試電子郵件] 對話方塊。 記下 [已傳送的電子郵件] 方塊中顯示的數字。 這是測試訊息的 mailitem_id。 選取 [確定]。
1. 在工具列上選取 [新增查詢] 開啟 [查詢編輯器] 視窗。 執行下列 T-SQL 陳述式來判斷測試電子郵件訊息的狀態：

    ```sql
    SELECT * FROM msdb.dbo.sysmail_allitems 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```

    sent_status 資料行會指出是否已傳送測試電子郵件訊息。

1. 如果發生錯誤，請執行以下陳述式檢視錯誤訊息：

    ```sql
    SELECT * FROM msdb.dbo.sysmail_event_log 
    WHERE mailitem_id = <the mailitem_id from the previous step> ;
    ```


##  <a name="see-also"></a><a name="RelatedContent"></a> 另請參閱 
  
-   [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)
-   [Database Mail 訊息物件](../../relational-databases/database-mail/database-mail-messaging-objects.md)
-   [Database Mail 外部程式](../../relational-databases/database-mail/database-mail-external-program.md)
-   [Database Mail 記錄與稽核](../../relational-databases/database-mail/database-mail-log-and-audits.md)
-   [設定 SQL Server Agent Mail 使用 Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)
  
  
