---
title: "連接到伺服器 (登入頁面) 資料庫引擎 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1556c7facc4a671767fe2d6c061b4f6655ba521b
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="connect-to-server-login-page-database-engine"></a>連接到伺服器 (登入頁面) Database Engine
使用此索引標籤來檢視或指定連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 時的選項。  
  
> [!NOTE]  
> 若要連結 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證，必須以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 和 Windows 驗證模式設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 。 如需有關如何判斷驗證模式及變更驗證模式的詳細資訊，請參閱 [如何：變更伺服器驗證模式](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0)。  
  
## <a name="options"></a>選項。  
**伺服器類型**  
從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
當您透過 [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Database Engine 執行個體時，您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證，並在 [連接到伺服器] 對話方塊的 [連接屬性] 索引標籤上指定資料庫。 請務必選取 [加密連接] 核取方塊。  
  
根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 會連接到 **master**。 如果您指定使用者資料庫，您只會在物件總管中看到該資料庫與其物件。 如果您連接到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱 [Windows Azure SQL Database 概觀](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**伺服器名稱**  
選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
**驗證**  
當連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體時，有兩種可用的驗證模式。  
  
當您透過 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Database Engine 執行個體時，您必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證，並在 [連接到伺服器] 對話方塊的 [連接屬性] 索引標籤上指定資料庫。 請務必選取 [加密連接] 核取方塊。  
  
根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 會連接到 **master**。 如果您指定使用者資料庫，您只會在物件總管中看到該資料庫與其物件。 如果您連接到 **master**，您將能夠看到所有資料庫。 如需詳細資訊，請參閱 [Windows Azure SQL Database 概觀](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
**Windows 驗證**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
**SQL Server 驗證**  
當使用者從非信任連接以指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
> [!IMPORTANT]  
> 盡可能使用 Windows 驗證。  
  
**Active Directory 通用驗證**  
Active Directory 通用驗證是支援 Azure 多重要素驗證 (MFA) 的互動式工作流程。 Azure MFA 有助於保護資料和應用程式的存取，同時又滿足使用者對簡單登入程序的需求。 它提供增強式驗證與一系列簡單的驗證選項 — 電話、簡訊、智慧卡與 PIN，或行動應用程式通知，讓使用者選擇他們喜好的方法。 當使用者帳戶進行 MFA 設定時，互動式驗證工作流程會透過快顯對話方塊、使用智慧卡等，要求額外的使用者互動。當使用者帳戶進行 MFA 設定時，使用者必須選取 Azure 通用驗證才能連接。 如果使用者帳戶不需要 MFA，使用者仍然可以使用其他兩個 Azure Active Directory 驗證選項。 如需詳細資訊，請參閱 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)(SQL 資料庫和 SQL 資料倉儲的 Azure AD MFA SSMS 支援)。 至少需要 SSMS 16.3 版 (2016 年 8 月)。
  
**Active Directory 密碼驗證**  
Azure Active Directory 驗證機制使用 Azure Active Directory (Azure AD) 中的身分識別連接至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 。  如果您使用未與 Azure 同盟之網域的認證登入 Windows，或是使用 Azure AD 根據初始或用戶端網域來使用 Azure AD 驗證時，請使用此方法連接至 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**Active Directory 整合式驗證**  
Azure Active Directory 驗證機制使用 Azure Active Directory (Azure AD) 中的身分識別連接至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 。 如果您使用來自同盟網域的 Azure Active Directory 認證登入 Windows，請使用此方法連接至 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**使用者名稱**  
要用來連接的 Windows 使用者名稱。 這個選項只有在您選取了使用 [Active Directory 密碼驗證]連接時才可以使用。 當您選取 [Windows 驗證] 時它是唯讀的。  
  
**登入**  
輸入要用來連接的登入。 這個選項只有在您選取了使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證連接時才可以使用。  
  
**密碼**  
輸入登入的密碼。 只有在您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證連接時，才能編輯此選項。  
  
**記住密碼**  
按一下即可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 儲存您輸入的密碼。 只有在您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證連接時，才能顯示此選項。  
  
**連接**  
按一下即可連接到上列所選的伺服器。  
  
**選項。**  
按一下即可變更對話方塊，並隱藏其他伺服器連接選項，例如記住密碼。  
  

