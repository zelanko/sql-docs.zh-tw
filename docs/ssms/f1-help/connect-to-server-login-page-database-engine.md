---
title: 連接到伺服器 (登入頁面) 資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 793d74393603d2ff535b501c64f4a35ef35eabc0
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542211"
---
# <a name="connect-to-server-login-page-database-engine"></a>連接到伺服器 (登入頁面) Database Engine
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用此索引標籤來檢視或指定連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]時的選項。 在大多數的情況下，您可以在 [伺服器名稱] 方塊中輸入資料庫伺服器的電腦名稱，然後按一下 [連接] 來進行連接。 如果您要連線至具名執行個體，請使用電腦名稱，後面依序加上反斜線及執行個體名稱。 例如， `mycomputer\myinstance`。 如果要連接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，請使用電腦名稱並於後面加上 **\sqlexpress**。  
  
許多因素都可能影響連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的能力。 如需說明，請參閱下列資源：  
- [教學課程第 1 課：連線至資料庫引擎](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [對 SQL Server 資料庫引擎的連線進行疑難排解](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [解決 SQL Server 的連線錯誤](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)    
  
> [!NOTE]  
> 若要連結 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，必須以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 驗證模式設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需有關如何判斷驗證模式及變更驗證模式的詳細資訊，請參閱 [如何：變更伺服器驗證模式](../../database-engine/configure-windows/change-server-authentication-mode.md)。  
  
## <a name="options"></a>選項。  
**伺服器類型**  
從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
當您透過 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 執行個體時，您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，並在 [連接到伺服器] 對話方塊的 [連接屬性] 索引標籤上指定資料庫。請務必選取 [加密連接] 核取方塊。  
  
根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會連接到 **master**。 如果您指定使用者資料庫，就只會看到該資料庫及其在物件總管中的物件。 如果您連線到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱 [Windows Azure SQL Database 概觀](https://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**伺服器名稱**  
選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
**驗證**  
SSMS 目前的版本提供五種驗證模式，可在連線至 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的執行個體時使用。 如果您的 [驗證] 對話方塊與下列清單不相符，請至[下載 SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) 下載最新版本的 SSMS。     
  
當您透過 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Engine 執行個體時，您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，並在 [連接到伺服器] 對話方塊的 [連接屬性] 索引標籤上指定資料庫。請務必選取 [加密連接] 核取方塊。  
  
根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會連接到 **master**。 如果您在連線至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 時指定使用者資料庫，就只會看到該資料庫及其在物件總管中的物件。 如果您連線到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱 [Windows Azure SQL Database 概觀](https://go.microsoft.com/fwlink/?LinkId=163948)。  
  
  > **Windows 驗證**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
  > **SQL Server 驗證**  
當使用者從非信任連接以指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。 盡可能使用 Windows 驗證。  
  
  > **Active Directory - 與 MFA 支援通用**  
[Active Directory - 與 MFA 通用] 是支援 Azure Multi-Factor Authentication (MFA) 的互動式工作流程。 Azure MFA 有助於保護資料和應用程式的存取，同時又滿足使用者對簡單登入程序的需求。 它提供增強式驗證與一系列簡單的驗證選項 - 電話、簡訊、智慧卡與 PIN，或行動應用程式通知，讓使用者選擇他們喜好的方法。 當使用者帳戶進行 MFA 設定時，互動式驗證工作流程會透過快顯對話方塊、使用智慧卡等，要求額外的使用者互動。當使用者帳戶進行 MFA 設定時，使用者必須選取 Azure 通用驗證才能連接。 如果使用者帳戶不需要 MFA，使用者仍然可以使用其他兩個 Azure Active Directory 驗證選項。 如需詳細資訊，請參閱 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)(SQL 資料庫和 SQL 資料倉儲的 Azure AD MFA SSMS 支援)。 如有必要，您可以按一下 [選項]，選取 [連線內容]索引標籤，然後完成 [AD 網域或租用戶識別碼] 方塊，來變更驗證登入的網域。  

  > **Active Directory - 密碼**  
Azure Active Directory 驗證機制使用 Azure Active Directory (Azure AD) 中的身分識別連接至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。  如果您用來登入 Windows 的認證來自未與 Azure 同盟的網域，或是使用 Azure AD 根據初始或用戶端網域來使用 Azure AD 驗證時，請使用此方法連線至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
  > **Active Directory - 整合式**  
Azure Active Directory 驗證機制使用 Azure Active Directory (Azure AD) 中的身分識別連接至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。 如果您使用來自同盟網域的 Azure Active Directory 認證登入 Windows，請使用此方法連線至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**User name**  
要用來連接的 Windows 使用者名稱。 這個選項只有在您選取了使用  **Active Directory 密碼驗證**時，使用此對話方塊來檢視或指定選項。 當您選取 [Windows 驗證] 或 [Active Directory - 整合式] 驗證時，其為唯讀狀態。  
  
**登入**  
輸入要用來連接的登入。 這個選項只有在您選取了使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證] 或 [Active Directory 密碼驗證] 連線時才可以使用。  
  
**密碼**  
輸入登入的密碼。 這個選項只有在您選取了使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證] 或 [Active Directory - 密碼] 驗證連線時才可以編輯。  
  
**記住密碼**  
按一下即可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 儲存您輸入的密碼。 只有在您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證連接時，才能顯示此選項。  
  
**[連接]**  
按一下以連線至伺服器。  
  
**選項。**  
按一下以顯示 [連線內容] 與 [其他連線參數] 索引標籤。  
   
  
