---
title: 執行 SQL Server Agent 作業工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqlserveragentjobtask.f1
helpviewer_keywords:
- Execute SQL Server Agent Job task [Integration Services]
- jobs [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: 3aa3bc0e-1a1c-452e-81b8-b4e3422ea053
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ead21855d754a9e5b48572e5576b311db5b32983
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37173259"
---
# <a name="execute-sql-server-agent-job-task"></a>執行 SQL Server Agent 作業工作
  「執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業」工作會執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 服務，可執行 SQL Server 執行個體中所定義的作業。 您可以建立執行 Transact-SQL 陳述式和 ActiveX 指令碼的作業、執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和「複寫維護」工作，或執行封裝。 您也可以設定作業來監視 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以及引發警示。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業通常可用來自動化重複執行的工作。 如需詳細資訊，請參閱 [實作作業](../../ssms/agent/implement-jobs.md)。  
  
 封裝可藉由使用「執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業」工作，執行與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件有關的管理工作。 例如， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業可執行 **sp_enum_dtspackages** 這類系統預存程序，以取得資料夾中的封裝清單。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 必須先執行，本機或多伺服器管理作業才能自動執行。  
  
 此工作會封裝 **sp_start_job** 系統程序，並將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的名稱傳遞至程序作為引數。 如需詳細資訊，請參閱 [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql)。  
  
## <a name="configuring-the-execute-sql-server-agent-job-task"></a>設定執行 SQL Server Agent 作業工作  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」設定屬性 這項工作位於「 **設計師」中** [工具箱] **的** [維護計畫工作] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 區段。  
  
 如需有關可在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請按下列主題：  
  
-   [執行 SQL Server Agent 作業工作 &#40;維護計畫&#41;](../../relational-databases/maintenance-plans/execute-sql-server-agent-job-task-maintenance-plan.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
  
