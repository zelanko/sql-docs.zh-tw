---
title: 建立作業 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 67231b2cfeb63d83198036da9c1603adb27b9396
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="create-jobs"></a>建立作業
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 循序執行的一系列指定作業。 一項作業可執行大範圍的活動，包括執行 [!INCLUDE[tsql](../../includes/tsql_md.md)] 指令碼、命令提示字元應用程式、Microsoft ActiveX 指令碼、Integration Services 封裝、Analysis Services 命令及查詢，或是「複寫」作業。 作業可執行重複性或可排程的工作，並可自動產生警示，通知使用者作業的狀態，進而大量地簡化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的管理程序。  
  
若要建立作業，使用者必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 固定資料庫角色或 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 只有作業擁有者或隸屬 **sysadmin** 角色的成員可以編輯作業。 隸屬 **sysadmin** 角色的成員可以將作業擁有權指定給其他使用者，無論作業擁有者是誰，都可以執行任何作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 固定資料庫角色的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
您可以撰寫作業，讓它在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的本機執行個體或是整個企業的多個執行個體上執行。 若要在多個伺服器上執行作業，您必須設定至少一個主要伺服器與一或多個目標伺服器。 如需主要及目標伺服器的詳細資訊，請參閱 [將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會將作業及作業步驟資訊記錄在作業記錄中。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業。|[建立作業](../../ssms/agent/create-a-job.md)|  
|描述如何將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業的擁有權重新指派給其他使用者。|[Give Others Ownership of a Job](../../ssms/agent/give-others-ownership-of-a-job.md)|  
|描述如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的作業記錄。|[Set Up the Job History Log](../../ssms/agent/set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>另請參閱  
[管理作業步驟](../../ssms/agent/manage-job-steps.md)  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[執行作業](../../ssms/agent/run-jobs.md)  
[檢視或修改作業](../../ssms/agent/view-or-modify-jobs.md)  
  
