---
title: Agent XPs 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6908c2c40f694b12e44ae98358ce0b95e8da4b13
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145010"
---
# <a name="agent-xps-server-configuration-option"></a>Agent XPs 伺服器組態選項
  使用 **代理程式 XP** 選項以啟用此伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程序。 未啟用此選項時，「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件總管」中就沒有 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent 節點可用。  
  
 當您使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 工具來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務時，就會自動啟用這些擴充預存程序。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
> [!NOTE]  
>  不論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務狀態為何，除非已啟用這些擴充預存程序，否則 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 物件總管不會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的內容。  
  
 可能的值為：  
  
-   **0**，表示無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程式 (預設值)。  
  
-   **1**，代表可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程式。  
  
 設定立即生效，伺服器不必停止再重新啟動。  
  
## <a name="examples"></a>範例  
 下列範例會啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程序。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Agent XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [自動化管理工作 &#40;SQL Server Agent&#41;](../../ssms/agent/sql-server-agent.md)   
 [啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  