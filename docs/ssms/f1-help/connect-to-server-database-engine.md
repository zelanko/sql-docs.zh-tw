---
title: "連接到伺服器 (資料庫引擎) | Microsoft Docs"
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
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d421bcb09ec7ebde28b5d1cce6eca2263cfb1c48
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="connect-to-server-database-engine"></a>連接到伺服器 (Database Engine)
連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 時，使用此對話方塊來檢視或指定選項。 在大多數的情況下，您可以在 [伺服器名稱] 方塊中輸入資料庫伺服器的電腦名稱，然後按一下 [連接] 來進行連接。 如果要連接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，請使用電腦名稱並於後面加上 **\sqlexpress**。  
  
許多因素都可能影響連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的能力。  
  
## <a name="options"></a>選項。  
**伺服器類型**  
從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [ [!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]]、[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]]、[ [!INCLUDE[ssEW](../../includes/ssew_md.md)]] 或 [ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] ]，再開始註冊新的伺服器。  
  
**伺服器名稱**  
選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
> [!NOTE]  
> 若要連接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 的使用中使用者執行個體，請使用指定管道名稱的具名管道通訊協定進行連接，例如 np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query。如需詳細資訊，請參閱 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文件集。  
  
**驗證**  
當連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體時，有三種可用的驗證模式。  
  
**Windows 驗證**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
**SQL Server 驗證**  
當使用者從非信任連接以指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
> [!IMPORTANT]  
> 可能的話，請使用 Windows 驗證或 Active Directory 密碼驗證。  
  
**Active Directory 通用驗證**  
Active Directory 通用驗證是支援 Azure 多重要素驗證 (MFA) 的互動式工作流程。 Azure MFA 有助於保護資料和應用程式的存取，同時又滿足使用者對簡單登入程序的需求。 它提供增強式驗證與一系列簡單的驗證選項 — 電話、簡訊、智慧卡與 PIN，或行動應用程式通知，讓使用者選擇他們喜好的方法。 當使用者帳戶進行 MFA 設定時，互動式驗證工作流程會透過快顯對話方塊、使用智慧卡等，要求額外的使用者互動。當使用者帳戶進行 MFA 設定時，使用者必須選取 Azure 通用驗證才能連接。 如果使用者帳戶不需要 MFA，使用者仍然可以使用其他兩個 Azure Active Directory 驗證選項。 如需詳細資訊，請參閱 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)(SQL 資料庫和 SQL 資料倉儲的 Azure AD MFA SSMS 支援)。 至少需要 SSMS 16.3 版 (2016 年 8 月)。

**Active Directory 密碼驗證**  
Azure Active Directory 驗證機制使用 Azure Active Directory (Azure AD) 中的身分識別連接至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 。  如果您使用未與 Azure 同盟之網域的認證登入 Windows，或是使用 Azure AD 根據初始或用戶端網域來使用 Azure AD 驗證時，請使用此方法連接至 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**Active Directory 整合式驗證**  
Azure Active Directory 驗證機制使用 Azure Active Directory (Azure AD) 中的身分識別連接至 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] 。 如果您使用來自同盟網域的 Azure Active Directory 認證登入 Windows，請使用此方法連接至 [!INCLUDE[ssSDS](../../includes/sssds_md.md)] 。 如需詳細資訊，請參閱 [使用 Azure Active Directory 驗證連線到 SQL 資料庫](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**使用者名稱**  
要用來連接的 Windows 使用者名稱。 這個選項只有在您選取了使用 [Active Directory 密碼驗證]連接時才可以使用。 當您選取 [Windows 驗證] 時它是唯讀的。  
  
**登入**  
輸入要用來連接的登入。 這個選項只有在您選取了使用 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證] 或 [Active Directory 密碼驗證] 連接時才可以使用。  
  
**密碼**  
輸入登入的密碼。 這個選項只有在您選取了使用 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證] 或 [Active Directory 密碼驗證] 連接時才可以編輯。  
  
**連接**  
按一下即可連接到上列所選的伺服器。  
  
**選項。**  
按一下即可顯示其他伺服器連接選項，例如，註冊伺服器與記住密碼。  
  

