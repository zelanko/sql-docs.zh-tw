---
title: "為多伺服器環境選擇 Agent 服務帳戶 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d9ccc867f1b4e54ef3d304277a5b0ad6725765c
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>為多伺服器環境選擇適當的 SQL Server Agent 服務帳戶
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 您為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務所選擇的 Windows 帳戶會影響多伺服器環境的行為，如下所示：  
  
-   如果您是以不是本機 Windows Administrators 群組成員的帳戶來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務，則將目標伺服器編列至主要伺服器會失敗。 如果這麼做，則會傳回下列錯誤訊息：  
  
    「編列作業失敗。」  
  
    重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務，以解決這個問題。  
  
-   如果以本機系統帳戶執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務，則只有在主要伺服器和目標伺服器都位在相同電腦上時，才支援「主要伺服器-目標伺服器」作業。 如果您使用這個組態，則將目標伺服器編列至主要伺服器時，會傳回下列訊息：  
  
    「請確定 <目標伺服器電腦名稱> 的代理程式啟動帳戶有權限以 targetServer 的身分登入」。  
  
    您可以忽略此參考訊息。 編列作業應該順利完成。  
  
如需為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務選擇帳戶的詳細資訊，請參閱 [選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)。  
  
