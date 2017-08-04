---
title: "變更 SSIS 向外記錄的帳戶 |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec785459e5f9585776d83cde3f460c1e79367e46
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="change-the-account-for-scale-out-logging"></a>變更標尺出記錄的帳戶
當封裝中執行向外，事件會記錄這些訊息在 SSISDB 與自動建立使用者**# # MS_SSISLogDBWorkerAgentLogin # #**。 此使用者的登入使用 SQL Server 驗證。 若要變更的帳戶，如下所示執行下列步驟：

## <a name="1-create-a-user-of-ssisdb"></a>1.建立 SSISDB 的使用者
建立資料庫使用者的指示，請參閱[建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md)。

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2.將使用者加入資料庫角色 ssis_cluster_worker

聯結資料庫角色的指示，請參閱[加入角色](../../relational-databases/security/authentication-access/join-a-role.md)。

## <a name="3-update-logging-information-in-ssisdb"></a>3.在 SSISDB 中更新記錄資訊
呼叫預存程序 [catalog]。[update_logdb_info] 做為參數的 Sql Server 名稱和連接字串。

#### <a name="example"></a>範例
```tsql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4.標尺出 Worker 服務重新啟動

> [!NOTE]
> 如果您使用 Windows 使用者帳戶的記錄時，它必須是相同的帳戶執行標尺出 Worker 服務。 否則，請登入 SQL Server 將會失敗。
