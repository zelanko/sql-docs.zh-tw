---
title: "DB 郵件和電子郵件警示，在 Linux 上的 SQL 代理程式與 |Microsoft 文件"
description: "本主題描述如何使用 SQL Server on Linux 的 DB 郵件和電子郵件警示"
author: meet-bhagdev
ms.author: meetb
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: tbd
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 77eed5cce942dbb91b0b9eb5afbd9ad11403e1d2
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>DB 郵件和電子郵件警示，在 Linux 上的 SQL 代理程式

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

下列步驟說明如何設定 DB 電子郵件，並使用它搭配 SQL Server Agent (**mssql server agent**) 在 Linux 上。 

> [!NOTE]
> 若要使用 SQL Server on Linux DB 郵件，您需要使用 SQL Server 2017 RC1 或更新版本。

## <a name="prerequisites"></a>必要條件

- SQL Server 2017 RC1 和更新版本
- SQL Server Agent v14.0.800.90 2 和更新版本 （如果您打算使用的電子郵件警示）

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

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4.將 Database Mail 帳戶加入至 Database Mail 設定檔
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
> 您可能必須移至您的電子郵件用戶端，並啟用 「 允許較不安全的用戶端傳送郵件 」。 並非所有的用戶端會辨識 DB 郵件做為電子郵件服務精靈。

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7.設定 DB 郵件設定檔使用 mssql conf 或環境變數
若要註冊您的資料庫郵件設定檔，您可以使用 mssql conf 公用程式或環境變數。 在此情況下，讓我們呼叫預設的設定檔。

```bash
# via mssql-conf
sudo /opt/mssq/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8.設定 SQLAgent 作業通知的操作員 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9.'測試代理程式作業' 成功時傳送電子郵件 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>後續的步驟
如需有關如何使用 SQL Server Agent 來建立、 排程及執行工作的詳細資訊，請參閱[在 Linux 上執行的 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)。

