---
title: "實作作業 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2c24813e306a43cf1adce27f71afe7c209194d53
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="implement-jobs"></a>實作作業
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業，使例行性管理工作自動化，並重複執行它們，使管理更有效率。  
  
作業是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 循序執行的一系列指定作業。 作業可執行各式各樣的活動，包括執行 [!INCLUDE[tsql](../../includes/tsql_md.md)] 指令碼、命令列應用程式、Microsoft ActiveX Script、Integration Services 封裝、Analysis Services 命令和查詢，或複寫工作。 作業可執行重複性工作或可排程的工作，而且可產生警示，將作業狀態自動通知使用者，藉此大幅簡化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的管理。  
  
您可以手動執行作業，或將作業設定為根據排程或為了回應警示而執行。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|包含有關建立作業及指派擁有權的資訊。|[建立作業](../../ssms/agent/create-jobs.md)|  
|包含有關將作業組織成類別目錄的資訊。|[組織作業](../../ssms/agent/organize-jobs.md)|  
|包含關於您可以建立的不同種類作業步驟及如何管理它們的資訊。|[管理作業步驟](../../ssms/agent/manage-job-steps.md)|  
|包含關於如何定義作業何時開始執行及作業執行頻率等資訊。|[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|包含關於手動執行作業 (沒有排程) 的資訊。|[執行作業](../../ssms/agent/run-jobs.md)|  
|包含關於如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 回應作業的資訊。 例如，您可以設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 在作業完成時通知管理者。|[指定作業回應](../../ssms/agent/specify-job-responses.md)|  
|包含關於如何檢視現有的作業、其執行的記錄及如何修改它們等資訊。|[檢視或修改作業](../../ssms/agent/view-or-modify-jobs.md)|  
|包含如何刪除作業的相關資訊。|[刪除作業](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>另請參閱  
[實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)  
  
