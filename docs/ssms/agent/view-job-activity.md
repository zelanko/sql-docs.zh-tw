---
title: 檢視作業活動 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 33cf01dda6f512428090d0c12654f43e1b03c0ab
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65103179"
---
# <a name="view-job-activity"></a>檢視作業活動
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中檢視 [!INCLUDE[tsql](../../includes/tsql-md.md)]Agent 作業的執行階段狀態。  
  
當 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動時，會建立新的工作階段，並且會在 **sysjobactivity** 資料庫的 **sysjobactivity** 資料表中填入已定義的所有現存作業。 此資料表會記錄目前的作業活動及狀態。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 中的「作業活動監視器」來檢視作業目前的狀態。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務突然終止，您可以參考 **sysjobactivity** 資料表，查看服務終止時正在執行的作業。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [安全性](#Security)  
  
-   **若要使用下列項目檢視作業活動：**  
  
    [Transact-SQL](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>開始之前  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-view-job-activity"></a>若要檢視作業活動  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**。  
  
3.  在 [作業活動監視器]一，然後按一下 [檢視作業活動]。  
  
4.  您可以在 **[作業活動監視器]** 中檢視為此伺服器定義之每項作業的詳細資訊。  
  
5.  以滑鼠右鍵按一下作業以啟動、停止、啟用或停用作業，重新整理其顯示在「作業活動監視器」中的狀態，將其刪除，或是檢視其記錄或屬性。  若要啟動、停止、啟用或停用，或是重新整理多個作業，請在「作業活動監視器」中選取數個資料列，並以滑鼠右鍵按一下選取範圍。  
  
6.  若要更新「作業活動監視器」，請按一下 **[重新整理]**。 若不要檢視那麼多資料列，請按一下 **[篩選]** ，並輸入篩選參數。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-view-job-activity"></a>若要檢視作業活動  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_help_jobactivity (TRANSACT-SQL)](https://msdn.microsoft.com/d344864f-b4d3-46b1-8933-b81dec71f511)。  
  
