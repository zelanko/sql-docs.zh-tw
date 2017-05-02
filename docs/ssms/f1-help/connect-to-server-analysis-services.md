---
title: "連接到伺服器 (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.analysisserver.f1
ms.assetid: 7e277d22-8d4b-422e-8882-7c5dd7a6d915
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 73451189bc401a4167c65261f3adcc5aabb6627c
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-analysis-services"></a>連接到伺服器 (Analysis Services)
連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 時，使用此對話方塊來檢視或指定選項。  
  
## <a name="options"></a>選項。  
**伺服器類型**  
從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從已註冊的伺服器註冊伺服器時，[伺服器類型]**** 方塊會呈現唯讀，並會與已註冊的伺服器元件中所顯示的伺服器類型進行比對。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [ [!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
**伺服器名稱**  
選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
**驗證**  
當連接到 Analysis Services 的執行個體時，支援下列驗證模式： [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 驗證。  
  
**Windows 驗證模式 (Windows 驗證)**  
**Windows 驗證** 模式允許使用者透過 Windows 使用者帳戶連接。  
  
**使用者名稱**  
這個選項在此版本中無法使用。 輸入要用來連接的使用者名稱。 只有在您選取使用 **Windows 驗證**連接時，才能使用此選項。  
  
**密碼**  
這個選項在此版本中無法使用。 輸入登入的密碼。 只有在您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證連接時，才能編輯此選項。  
  
**連接**  
按一下即可連接到上列所選的伺服器。  
  
**選項。**  
按一下即可顯示其他伺服器連接選項，例如，註冊伺服器與記住密碼。  
  

