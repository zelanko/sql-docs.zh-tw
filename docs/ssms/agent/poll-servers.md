---
title: 輪詢伺服器
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- target servers [SQL Server], polling interval
- polling master servers [SQL Server]
- server polling [SQL Server]
- master servers [SQL Server], polling
- polling interval [SQL Server]
ms.assetid: 96f5fd43-3edd-4418-9dd0-4d34e618890e
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 687b666443900dca8bcf5bde6b7bb15bb3c5c7fa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247603"
---
# <a name="poll-servers"></a>輪詢伺服器
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

在實作多伺服器管理時，目標伺服器會定期連絡主要伺服器，來上傳已執行作業的相關資訊，並下載新的作業。 連絡主要伺服器的程序稱為「伺服器輪詢」  ，它會以定期的「輪詢間隔」  來進行。  
  
## <a name="polling-intervals"></a>輪詢間隔  
輪詢間隔 (預設值為一分鐘) 可控制目標伺服器連接到主要伺服器，以下載指示與上傳作業執行結果的頻率。  
  
當目標伺服器輪詢主要伺服器時，它會從 **msdb** 資料庫中的 **sysdownloadlist** 資料表讀取指派給目標伺服器的作業。 這些作業控制了多伺服器作業與目標伺服器各種不同方面的行為。 作業的範例包括刪除作業、插入作業、啟動作業與更新目標伺服器的輪詢時間間隔。  
  
作業是以下列兩種方法之一傳送到 **sysdownloadlist** 資料表：  
  
-   使用 **sp_post_msx_operation** 預存程序直接傳送。  
  
-   使用其他的作業預存程序間接傳送。  
  
如果您使用作業預存程序來修改多伺服器作業排程或作業步驟，或使用 SQL Distributed Management Objects (SQL-DMO) 來控制多伺服器作業，請在修改多伺服器作業的步驟或排程後，發出下列命令：  
  
```  
EXECUTE msdb.dbo.sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
發出此命令可確保同步處理目標伺服器與目前的作業定義。  
  
如果使用下列項目，則不需要明確發佈作業：  
  
-   可控制多伺服器作業的 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
-   不會修改作業排程或作業步驟的作業預存程序。  
  
**若要強制目標伺服器輪詢主要伺服器**  
  
-   [Transact-SQL](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/085deef8-2709-4da9-bb97-9ab32effdacf)  
  
## <a name="see-also"></a>另請參閱  
[管理事件](../../ssms/agent/manage-events.md)  
  
