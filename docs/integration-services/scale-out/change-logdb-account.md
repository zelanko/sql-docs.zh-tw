---
title: "變更 SSIS Scale Out 記錄的帳戶 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcedbe0d2c2ef2c2089af1e2a8b31fbeb75ce2fc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-account-for-scale-out-logging"></a>變更 Scale Out 記錄的帳戶
在 Scale Out 中執行套件時，會將事件訊息記錄到 SSISDB 中，並自動建立使用者 **##MS_SSISLogDBWorkerAgentLogin##**。 此使用者使用 SQL Server 驗證登入。 若要變更帳戶，請遵循下列步驟：

## <a name="1-create-a-user-of-ssisdb"></a>1.建立 SSISDB 的使用者
如需建立資料庫使用者的指示，請參閱[建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)。

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2.將使用者新增至資料庫角色 ssis_cluster_worker

如需加入資料庫角色的指示，請參閱[加入角色](../../relational-databases/security/authentication-access/join-a-role.md)。

## <a name="3-update-logging-information-in-ssisdb"></a>3.更新 SSISDB 中的記錄資訊
呼叫預存程序 [catalog].[update_logdb_info]，參數為 Sql Server 名稱和連接字串。

#### <a name="example"></a>範例
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4.重新啟動 Scale Out 背景工作角色服務

> [!NOTE]
> 如果您使用 Windows 使用者帳戶進行記錄，其必須與執行 Scale Out 背景工作角色服務的帳戶一致。 否則會無法登入 SQL Server。
