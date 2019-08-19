---
title: 將作業指派至作業類別目錄 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], assigning
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- SQL Server Agent jobs, assigning
- assigning job to category
ms.assetid: a9ea65a2-1d73-4582-a335-63adeb450cb6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ff6fa55f2c4accc16a89758d0687519d76b51f6c
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553370"
---
# <a name="assign-a-job-to-a-job-category"></a>將作業指派至作業類別目錄

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中將 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業指派到作業類別目錄。  
  
作業類別目錄可幫助您組織作業，以便於篩選與分組。 例如，您可以將所有的資料庫備份作業整理在資料庫維護類別中。 您可以將作業指派到內建的作業類別目錄，您也可以建立使用者自訂的作業類別目錄，然後將作業指派給它。  

## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>若要將作業指派至作業類別目錄  
  
1.  在 **[物件總管]** 中，按一下加號展開要將作業指派至作業類別目錄的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  按一下加號展開 **[作業]** 資料夾。  
  
4.  以滑鼠右鍵按一下要編輯的作業，然後選取 [屬性]  。  
  
5.  在 [作業屬性 - _job\_name_]  對話方塊的 [類別目錄]  清單中，選取您要指派給作業的作業類別目錄。  
  
6.  按一下 [確定]  。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>若要將作業指派至作業類別目錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_update_job (Transact-SQL)](https://msdn.microsoft.com/cbdfea38-9e42-47f3-8fc8-5978b82e2623)。  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**若要將作業指派至作業類別目錄**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobCategory** 類別。  
  
