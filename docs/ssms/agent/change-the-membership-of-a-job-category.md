---
title: 變更作業類別的成員資格
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
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a4e9c34de355a5e09dd2b0b299807d15cecffb38
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749172"
---
# <a name="change-the-membership-of-a-job-category"></a>變更作業類別的成員資格
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 管理物件，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中變更作業類別目錄的成員資格。  
  
作業類別目錄可幫助您組織作業，以便於篩選與分組。 您可以建立自己的作業類別目錄。 您還可以變更作業類別目錄中的 Microsoft SQL Server Agent 作業成員資格。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>變更作業類別目錄的成員資格  
  
1.  在 **[物件總管]** 中，按一下加號展開要編輯作業類別目錄所在的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  以滑鼠右鍵按一下 [作業]  資料夾，然後選取 [管理作業類別目錄]  。  
  
4.  在 [管理作業類別目錄 <伺服器名稱>]   對話方塊中，選取要編輯的作業類別目錄，然後按一下 [檢視作業]  。  
  
5.  選取 **[顯示所有作業]** 核取方塊。  
  
6.  若要將作業加入至類別目錄，在主要方格中選取該作業所對應之 **[選取]** 資料行中的核取方塊。 若要移除類別目錄中的作業，請清除該方塊。 完成後，請按一下 **[確定]** 。  
  
7.  關閉 [管理作業類別目錄 <伺服器名稱>]   對話方塊。  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>變更作業類別目錄的成員資格  
  
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
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
**變更作業類別目錄的成員資格**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobCategory** 類別。  
  
