---
title: DB Mail 和 Linux 上的 SQL 代理程式的電子郵件警示 |Microsoft Docs
description: 本文說明如何在 Linux 上的 SQL Server 中使用 DB Mail 和電子郵件警示
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.date: 02/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: tbd
ms.openlocfilehash: f9ce71d799414171019143912bde19330742ec27
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984260"
---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>DB Mail 和 Linux 上的 SQL 代理程式的電子郵件警示

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟會示範如何設定 DB 電子郵件，並將它與 SQL Server Agent (**mssql server agent**) 在 Linux 上。 

## <a name="1-enable-db-mail"></a>1.啟用 DB 郵件

```sql
USE master 
GO 
sp_configure 'show advanced options',1 
GO 
RECONFIGURE WITH OVERRIDE 
GO 
sp_configure 'Database Mail XPs', 1 
GO 
RECONFIGURE  
GO  
```

## <a name="2-create-a-new-account"></a>2.建立新帳戶
```sql
EXECUTE msdb.dbo.sysmail_add_account_sp 
@account_name = 'SQLAlerts', 
@description = 'Account for Automated DBA Notifications', 
@email_address = 'sqlagenttest@gmail.com', 
@replyto_address = 'sqlagenttest@gmail.com', 
@display_name = 'SQL Agent', 
@mailserver_name = 'smtp.gmail.com', 
@port = 587, 
@enable_ssl = 1, 
@username = 'sqlagenttest@gmail.com', 
@password = '<password>' 
GO
```

## <a name="3-create-a-default-profile"></a>3.建立預設的設定檔

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4.Database Mail 設定檔中新增 Database Mail 帳戶
```sql
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp 
@profile_name = 'default', 
@principal_name = 'public', 
@is_default = 1 ; 
 ```
 
## <a name="5-add-account-to-profile"></a>5.將帳戶新增至設定檔 
```sql
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp   
@profile_name = 'default',   
@account_name = 'SQLAlerts',   
@sequence_number = 1;  
 ```
 
## <a name="6-send-test-email"></a>6.傳送測試電子郵件
> [!NOTE]
> 您可能必須移至您的電子郵件用戶端，並啟用 「 允許較不安全的用戶端傳送郵件 」。 並非所有的用戶端會辨識 DB 郵件的電子郵件服務精靈的形式。

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7.設定 DB 郵件設定檔使用 mssql conf 或環境變數
若要註冊您的資料庫郵件設定檔，您可以使用 mssql conf 公用程式或環境變數。 在此情況下，讓我們來呼叫我們的設定檔預設值。

```bash
# via mssql-conf
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8.設定操作員 SQLAgent 作業通知。 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9.'代理程式測試工作' 順利完成時傳送電子郵件 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>後續的步驟
如需有關如何使用 SQL Server Agent 來建立、 排程及執行工作的詳細資訊，請參閱 <<c0> [ 在 Linux 上執行的 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)。
