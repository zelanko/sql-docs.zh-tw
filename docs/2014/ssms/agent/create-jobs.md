---
title: 建立作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 986e38ef42fe1af2aba8ba1625225a336f29158d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162460"
---
# <a name="create-jobs"></a>建立作業
  作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 循序執行的一系列指定作業。 一項作業可執行大範圍的活動，包括執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、命令提示字元應用程式、Microsoft ActiveX 指令碼、Integration Services 封裝、Analysis Services 命令及查詢，或是「複寫」作業。 作業可執行重複性或可排程的工作，並可自動產生警示，通知使用者作業的狀態，進而大量地簡化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的管理程序。  
  
 若要建立作業，使用者必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色或 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 只有作業擁有者或隸屬 **sysadmin** 角色的成員可以編輯作業。 隸屬 **sysadmin** 角色的成員可以將作業擁有權指定給其他使用者，無論作業擁有者是誰，都可以執行任何作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](sql-server-agent-fixed-database-roles.md)。  
  
 您可以撰寫作業，讓它在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機執行個體或是整個企業的多個執行個體上執行。 若要在多個伺服器上執行作業，您必須設定至少一個主要伺服器與一或多個目標伺服器。 如需主要及目標伺服器的詳細資訊，請參閱 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會將作業及作業步驟資訊記錄在作業記錄中。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。|[建立作業](create-a-job.md)|  
|描述如何將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的擁有權重新指派給其他使用者。|[Give Others Ownership of a Job](give-others-ownership-of-a-job.md)|  
|描述如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的作業記錄。|[Set Up the Job History Log](set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>另請參閱  
 [管理作業步驟](manage-job-steps.md)   
 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)   
 [建立及附加排程至作業](create-and-attach-schedules-to-jobs.md)   
 [執行工作](run-jobs.md)   
 [檢視或修改作業](view-or-modify-jobs.md)  
  
  
