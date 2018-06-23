---
title: SQL Server Agent 屬性 (連接頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 48f107d115960c879a8f2818b62215c6a1c316b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035131"
---
# <a name="sql-server-agent-properties-connection-page"></a>SQL Server Agent 屬性 (連接頁面)
  使用此頁面檢視及修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間的連線設定。  
  
## <a name="options"></a>選項。  
 **別名本機主機伺服器**  
 指定用來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之本機執行個體的別名。 如果您無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的預設連接選項，請為執行個體定義別名，並在此處指定該別名。  
  
 **使用 Windows 驗證**  
 將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證設定為連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的驗證方法。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務執行身分帳戶連線。  
  
 **[使用 SQL Server 驗證]**  
 設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證為連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的驗證方法。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供驗證的目的在提供回溯相容性。 為了提升安全性，如果可能的話請使用 Windows 驗證。  
  
 **登入**  
 指定用來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的登入名稱。  
  
 **密碼**  
 指定用來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的密碼。  
  
  