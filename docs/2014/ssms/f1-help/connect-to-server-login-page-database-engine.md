---
title: 連接到伺服器 (登入頁面) 資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fe246a1f8baf1ab9f60ab1fa73e21e81c052aa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153698"
---
# <a name="connect-to-server-login-page-database-engine"></a>連接到伺服器 (登入頁面) Database Engine
  當連接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]時，使用此索引標籤來查看或指定選項。  
  
> [!NOTE]  
>  若要連結 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，必須以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 驗證模式設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需如何判斷驗證模式及變更驗證模式的詳細資訊，請參閱[變更伺服器驗證模式](../../database-engine/configure-windows/change-server-authentication-mode.md)。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型]**** 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
 透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎的實例時，您必須使用驗證，並在 [連線**到伺服器**] 對話方塊的 [**連接屬性**] 索引標籤上指定資料庫。請確定您選取 [**加密連接**] 核取方塊。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會連接到 **master**。 如果您指定使用者資料庫，您只會在物件總管中看到該資料庫與其物件。 如果您連接到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱[Azure SQL Database 總覽](/azure/sql-database/sql-database-technical-overview)。  
  
 **伺服器名稱**  
 選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
 **驗證**  
 當連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體時，有兩種可用的驗證模式。  
  
 透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫引擎的實例時，您必須使用驗證，並在 [連線**到伺服器**] 對話方塊的 [**連接屬性**] 索引標籤上指定資料庫。請確定您選取 [**加密連接**] 核取方塊。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會連接到 **master**。 如果您指定使用者資料庫，您只會在物件總管中看到該資料庫與其物件。 如果您連接到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱[Azure SQL Database 總覽](/azure/sql-database/sql-database-technical-overview)。  
  
 **Windows 驗證模式（Windows 驗證）**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
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
  
 **記住密碼**  
 按一下即可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存您輸入的密碼。 只有在您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接時，才能顯示此選項。  
  
 **連線**  
 按一下即可連接到上列所選的伺服器。  
  
 **選項**  
 按一下即可變更對話方塊，並隱藏其他伺服器連接選項，例如記住密碼。  
  
  
