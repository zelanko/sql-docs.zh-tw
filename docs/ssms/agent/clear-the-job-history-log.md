---
description: 清除作業歷程記錄
title: 清除作業歷程記錄
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fb9f95cd3621454b6e6b3aa99f1abd08df446acc
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035681"
---
# <a name="clear-the-job-history-log"></a>清除作業歷程記錄
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server Management Objects，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中刪除 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業記錄的內容。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>若要清除作業記錄檔  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，然後展開 **[作業]**。  
  
3.  以滑鼠右鍵按一下某個作業，然後按一下 **[檢視記錄]**。  
  
4.  在 **[記錄檔檢視器]** 中，選取您要清除其記錄的作業，然後執行下列其中一項：  
  
    -   按一下 **[刪除]**，然後按一下 **[刪除記錄]** 對話方塊中的 **[刪除所有的記錄]** 。 您可以刪除所有的作業記錄，也可以只刪除某個特定日期之前的記錄。 如果您要移除所有的作業記錄，請按一下 **[刪除所有的記錄]**。 如果您只要移除舊的作業記錄，請按一下 **[刪除在這之前的記錄]**，然後指定日期。  
  
    -   如果您要清除多重伺服器作業的記錄，請按一下 **[作業狀態]** 。 按一下 **[作業]**，按一下作業名稱，然後按一下 **[檢視遠端作業記錄]**。  
  
5.  按一下 **[刪除]** 。  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>若要清除作業記錄檔  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
**若要清除作業記錄檔**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobServer** 類別的 **PurgeJobHistory** 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)。  
