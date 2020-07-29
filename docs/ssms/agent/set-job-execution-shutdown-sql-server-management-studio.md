---
title: 設定作業執行關機
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4c01bcc24c8d0fb41f56e87e1f02570a77a36ecd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759766"
---
# <a name="set-job-execution-shutdown"></a>設定作業執行關機

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)]，以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent 等待執行中作業完成的等候時間，之後 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent 便會自行結束。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
根據預設，**系統管理員**固定伺服器角色成員可以設定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 等待執行中作業完成的等候時間，之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 便會自行結束。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>若要設定作業執行關機  
  
1.  在 **[物件總管]** 中，按一下加號，展開要設定作業執行關機間隔的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  ，然後選取 [屬性]  。  
  
3.  在 **[選取頁面]** 底下，選取 **[作業的系統]** 。  
  
4.  設定 [關機逾時間隔]  \(以秒為單位)，以增加或減少關機的逾時間隔。 這決定了在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 自行結束前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會等待執行中作業完成的時間。  
  
