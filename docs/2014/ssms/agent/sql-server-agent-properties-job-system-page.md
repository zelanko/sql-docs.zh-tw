---
title: SQL Server Agent 屬性 (作業系統頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8dceeba78e639ecbe2fd81fbdb1021293e75cf8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63246076"
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server Agent 屬性 (作業系統頁面)
  使用此頁面來查看和修改 Agent 服務[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理作業的方式。  
  
## <a name="options"></a>選項。  
 **關機逾時間隔（以秒為單位）**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在關機之前，要等候作業完成的秒數。 如果在指定的時間間隔之後作業仍在執行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會強制停止作業。  
  
 **使用非系統管理員 proxy 帳戶**  
 設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的非管理員 Proxy 帳戶。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]和更新的版本支援多個 proxy，因此只有在管理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前的 Agent 版本時， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]才適用此選項。  
  
 **使用者名稱**  
 輸入非管理員 Proxy 帳戶的使用者名稱。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Agent 版本時，才可以使用此選項。  
  
 **密碼**  
 輸入非管理員 Proxy 帳戶的使用者密碼。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]和更新的版本支援多個 proxy，因此只有在管理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前的 Agent 版本時， [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]才適用此選項。  
  
 **網域**  
 輸入非系統管理 Proxy 帳戶的使用者網域。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Agent 版本時，才可以使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [實作作業](implement-jobs.md)  
  
  
