---
title: 連接到伺服器 (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectoserverunknownservertype.f1
- sql12.swb.connection.login.sqlserver.f1
- sql12.swb.connection.login.sqlce.f1
- sql12.swb.manageSS2k.f1
- sql12.swb.connecttoce.f1
- sql12.swb.connecttoce.connectionproperties.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: beb7afac36d1183fc9142874f4c2de1589ff0df2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189958"
---
# <a name="connect-to-server-database-engine"></a>連接到伺服器 (Database Engine)
  使用此對話方塊可在連線到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 時檢視或指定選項。 在大多數的情況下，您可以在 [伺服器名稱] 方塊中輸入資料庫伺服器的電腦名稱，然後按一下 [連接] 來進行連接。 如果要連接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，請使用電腦名稱並於後面加上 **\sqlexpress**。  
  
 許多因素都可能影響連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的能力。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)]]、[ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]]、[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]]、[ [!INCLUDE[ssEW](../../includes/ssew-md.md)]] 或 [ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ]，再開始註冊新的伺服器。  
  
 **伺服器名稱**  
 選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
> [!NOTE]  
>  若要連接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的使用中使用者執行個體，請使用指定管道名稱的具名管道通訊協定進行連接，例如 np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query。如需詳細資訊，請參閱 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 文件集。  
  
 **驗證**  
 當連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體時，有兩種可用的驗證模式。  
  
 **Windows 驗證模式 (Windows 驗證)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
 **SQL Server 驗證**  
 當使用者從非信任連接以指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。  
  
 **使用者名稱**  
 輸入要用來連接的使用者名稱。 只有在您選取使用 Windows 驗證連接時，才能使用此選項。  
  
 **登入**  
 輸入要用來連接的登入。 這個選項只有在您選取了使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接時才可以使用。  
  
 **密碼**  
 輸入登入的密碼。 只有在您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接時，才能編輯此選項。  
  
 **[連接]**  
 按一下即可連接到上列所選的伺服器。  
  
 **選項。**  
 按一下即可顯示其他伺服器連接選項，例如，註冊伺服器與記住密碼。  
  
  
