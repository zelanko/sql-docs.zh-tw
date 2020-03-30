---
title: 搭配 Linux 上 SQL Agent 的 DB Mail 和電子郵件警示
description: 本文描述如何搭配 Linux 上的 SQL Server 來使用 DB Mail 和電子郵件警示
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: tbd
ms.openlocfilehash: 31f8931f6e0eddc67b2e58ae794631a9ae6555b7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68077453"
---
# <a name="db-mail-and-email-alerts-with-sql-agent-on-linux"></a>搭配 Linux 上 SQL Agent 的 DB Mail 和電子郵件警示

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

下列步驟說明如何設定 DB Mail 並將其與 Linux 上的 SQL Server Agent (**mssql-server-agent**) 搭配使用。 

## <a name="1-enable-db-mail"></a>1.啟用 DB Mail

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

## <a name="3-create-a-default-profile"></a>3.建立預設設定檔

```sql
EXECUTE msdb.dbo.sysmail_add_profile_sp 
@profile_name = 'default', 
@description = 'Profile for sending Automated DBA Notifications' 
GO
```

## <a name="4-add-the-database-mail-account-to-a-database-mail-profile"></a>4.將 Database Mail 帳戶新增至 Database Mail 設定檔
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
> 您可能必須前往您的電子郵件用戶端，並啟用「允許較不安全的用戶端傳送郵件」。 並非所有用戶端都會將 DB Mail 辨識為電子郵件精靈。

```
EXECUTE msdb.dbo.sp_send_dbmail 
@profile_name = 'default', 
@recipients = 'recipient-email@gmail.com', 
@Subject = 'Testing DBMail', 
@Body = 'This message is a test for DBMail' 
GO
```

## <a name="7-set-db-mail-profile-using-mssql-conf-or-environment-variable"></a>7.使用 mssql-conf 或環境變數來設定 DB Mail 設定檔
您可以使用 mssql-conf 公用程式或環境變數來註冊您的 DB Mail 設定檔。 在此情況下，我們將呼叫設定檔預設值。

```bash
# via mssql-conf
sudo /opt/mssql/bin/mssql-conf set sqlagent.databasemailprofile default
# via environment variable
MSSQL_AGENT_EMAIL_PROFILE=default
```

## <a name="8-set-up-an-operator-for-sqlagent-job-notifications"></a>8.設定 SQLAgent 作業通知的運算子 

```sql
EXEC msdb.dbo.sp_add_operator 
@name=N'JobAdmins',  
@enabled=1, 
@email_address=N'recipient-email@gmail.com',  
@category_name=N'[Uncategorized]' 
GO 
```

## <a name="9-send-email-when-agent-test-job-succeeds"></a>9.「代理程式測試作業」成功時傳送電子郵件 

```
EXEC msdb.dbo.sp_update_job 
@job_name='Agent Test Job', 
@notify_level_email=1, 
@notify_email_operator_name=N'JobAdmins' 
GO
```

## <a name="next-steps"></a>後續步驟
如需如何使用 SQL Server Agent 來建立、排程和執行作業的詳細資訊，請參閱[在 Linux 上執行 SQL Server Agent 作業](sql-server-linux-run-sql-server-agent-job.md)。
