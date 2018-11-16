---
title: Agent XPs 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Agent XPs option
- extended stored procedures [SQL Server], SQL Server Agent
ms.assetid: 2e1c6c64-5ce7-4357-98c7-ac7763a9f9de
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8f0f897fcc970ee95942fd9e72ce7e21af257fa2
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51599918"
---
# <a name="agent-xps-server-configuration-option"></a>Agent XPs 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 **代理程式 XP** 選項以啟用此伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程序。 未啟用此選項時，「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件總管」中就沒有 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Agent 節點可用。  
  
 當您使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 工具來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務時，就會自動啟用這些擴充預存程序。 如需詳細資訊，請參閱＜ [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md)＞。  
  
> [!NOTE]  
>  不論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務狀態為何，除非已啟用這些擴充預存程序，否則 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 物件總管不會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的內容。  
  
 可能的值為：  
  
-   **0**，表示無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程式 (預設值)。  
  
-   **1**，代表可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程式。  
  
 設定立即生效，伺服器不必停止再重新啟動。  
  
## <a name="example"></a>範例
 下列範例會啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 擴充預存程序。  

1. 從 Microsoft SQL Server Management Studio，連接到資料庫引擎。

2.  在標準列中，按一下 [新增查詢]。

3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 
  
```sql 
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
 [自動化管理工作 &#40;SQL Server Agent&#41;](https://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)   
 [啟動、停止或暫停 SQL Server Agent 服務](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  
  
