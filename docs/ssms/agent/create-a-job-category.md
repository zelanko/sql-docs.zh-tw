---
title: 建立作業類別目錄
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2b5721464d63893a917bb0036491eacbb7ca4c8f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245935"
---
# <a name="create-a-job-category"></a>建立作業類別目錄
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 管理物件，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立作業類別目錄。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 提供了內建作業類別目錄，您可將作業指派給這些內建作業類別目錄，或可建立作業類別目錄並指派其作業。 作業類別目錄可幫助您組織作業，以便於篩選與分組。 例如，您可以將所有的資料庫備份作業整理在資料庫維護類別中。 您也可以建立您自己的作業類別。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
多伺服器類別只存在於主要伺服器上。 主要伺服器上只有一個預設作業類別目錄：**未分類 (多伺服器)** 。 下載多伺服器作業之後，其類別目錄會變更為目標伺服器上的 **[來自 MSX 的作業]** 。  
  
### <a name="security"></a><a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>若要建立作業類別目錄  
  
1.  在 **[物件總管]** 中，按一下加號展開要建立作業類別目錄所在的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  以滑鼠右鍵按一下 [作業]  資料夾，然後選取 [管理作業類別目錄]  。  
  
4.  在 [管理作業類別目錄 <伺服器名稱>] 對話方塊中，按一下 [新增]。  
  
5.  在新對話方塊的 **[名稱]** 方塊中，輸入新作業類別目錄的名稱。  
  
6.  選取 **[顯示所有作業]** 核取方塊。 選取對應於作業的方塊，為新的類別目錄選取一個或多個作業。  
  
7.  按一下 [確定]  。  
  
8.  在 [管理作業類別目錄 <伺服器名稱>] 對話方塊中，按一下 [重新整理]，以確定新作業類別目錄為作用中。 如果一切如預期，關閉此對話方塊。  
  
如需這些對話方塊的詳細資訊，請參閱 [作業類別目錄 - 管理作業類別目錄](../../ssms/agent/job-categories-manage-job-categories.md) 和 [作業類別目錄屬性 - 新作業類別目錄](../../ssms/agent/job-categories-properties-new-job-category.md)。  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>若要建立作業類別目錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_category (Transact-SQL)](https://msdn.microsoft.com/6cca32cd-d941-4378-aed6-a7c90cb7520a)。  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
**若要建立作業類別目錄**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 **JobCategory** 類別。 如需範例程式碼，請參閱 [使用 SQL Server Agent 排程自動管理工作](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)。  
  
