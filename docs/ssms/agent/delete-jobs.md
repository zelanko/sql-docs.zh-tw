---
title: "刪除作業 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bd50bb466f4c34b38effd5b562131b46f8243d67
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="delete-jobs"></a>刪除作業
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 作業是 SQL Server Agent 循序執行的一系列指定作業。 根據預設，執行完成時不會刪除作業。 您可以刪除一個或多個 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業，無論作業成功或失敗。 您也可以設定 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在作業成功、失敗或完成時自動予以刪除。  
  
依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 [sp_delete_job (Transact-SQL)](http://msdn.microsoft.com/en-us/b85db6e4-623c-41f1-9643-07e5ea38db09) 系統預存程序以刪除作業。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
**系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_delete_job** 來刪除任何作業。 本身不是 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者只能刪除其本身所擁有的作業。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何刪除一個或多個 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業。|[刪除一個或多個作業](../../ssms/agent/delete-one-or-more-jobs.md)|  
|描述如何設定 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在作業成功、失敗或完成時自動予以刪除。|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
