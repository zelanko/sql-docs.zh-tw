---
title: SQL Server Agent 屬性 (作業系統頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 728f3cc395ec9e02b3e64236aa52e5b6cf99d8ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202348"
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server Agent 屬性 (作業系統頁面)
  使用此頁面來檢視和修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務管理作業的方式。  
  
## <a name="options"></a>選項。  
 **關機逾時間隔 (以秒為單位)**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 在關機之前，要等候作業完成的秒數。 如果在指定的時間間隔之後作業仍在執行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會強制停止作業。  
  
 **使用非管理員 Proxy 帳戶**  
 設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的非管理員 Proxy 帳戶。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新的版本支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Agent 版本時，才可以使用此選項。  
  
 **使用者名稱**  
 輸入非管理員 Proxy 帳戶的使用者名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Agent 版本時，才可以使用此選項。  
  
 **密碼**  
 輸入非管理員 Proxy 帳戶的使用者密碼。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新的版本支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Agent 版本時，才可以使用此選項。  
  
 **網域**  
 輸入非系統管理 Proxy 帳戶的使用者網域。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援多個 Proxy，因此只有在管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Agent 版本時，才可以使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [實作作業](implement-jobs.md)  
  
  
