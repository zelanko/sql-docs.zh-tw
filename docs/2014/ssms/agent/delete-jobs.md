---
title: 刪除作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: stevestein
ms.author: sstein
ms.openlocfilehash: f66387a1334f91c29b8edddad293d76064430b39
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995470"
---
# <a name="delete-jobs"></a>刪除作業
  作業是 SQL Server Agent 循序執行的一系列指定作業。 根據預設，執行完成時不會刪除作業。 您可以刪除一個或多個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，無論作業成功或失敗。 您也可以設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在作業成功、失敗或完成時自動予以刪除。  
  
 根據預設，系統管理員（ **sysadmin** ）固定伺服器角色的成員可以執行[Sp_delete_job，&#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)系統預存程式來刪除作業。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](sql-server-agent-fixed-database-roles.md)。  
  
 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_delete_job** 來刪除任何作業。 本身不是 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者只能刪除其本身所擁有的作業。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**本文**|  
|描述如何刪除一個或多個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。|[刪除一個或多個作業](delete-one-or-more-jobs.md)|  
|描述如何設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在作業成功、失敗或完成時自動予以刪除。|[自動刪除作業](automatically-delete-a-job.md)|  
  
  
