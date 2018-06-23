---
title: 刪除作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
caps.latest.revision: 4
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: de97c584fd70b251471ddc0ce4c4f37bb9aa0d49
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132787"
---
# <a name="delete-jobs"></a>刪除作業
  作業是 SQL Server Agent 循序執行的一系列指定作業。 根據預設，執行完成時不會刪除作業。 您可以刪除一個或多個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，無論作業成功或失敗。 您也可以設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在作業成功、失敗或完成時自動予以刪除。  
  
 根據預設，成員**sysadmin**固定的伺服器角色可以執行[sp_delete_job &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)系統預存程序來刪除作業。 其他使用者必須被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **資料庫的下列其中一個** Agent 固定資料庫角色。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 如需這些角色權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](sql-server-agent-fixed-database-roles.md)。  
  
 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_delete_job** 來刪除任何作業。 本身不是 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者只能刪除其本身所擁有的作業。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何刪除一個或多個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。|[刪除一個或多個作業](delete-one-or-more-jobs.md)|  
|描述如何設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在作業成功、失敗或完成時自動予以刪除。|[Automatically Delete a Job](automatically-delete-a-job.md)|  
  
  
