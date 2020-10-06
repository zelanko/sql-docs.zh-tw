---
description: 連接到伺服器 (Database Engine)
title: 連接到伺服器 (Database Engine)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 04/07/2020
ms.openlocfilehash: 2298bc5ad9a6be79d8ab48a42c579c2114bc1656
ms.sourcegitcommit: 27f95e50f11a98164e9e7a5130a3e00ac06b4cea
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/28/2020
ms.locfileid: "91412959"
---
# <a name="connect-to-server-database-engine"></a>連接到伺服器 (Database Engine)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 時，使用此對話方塊來檢視或指定選項。 在大多數的情況下，您可以在 [伺服器名稱] 方塊中輸入資料庫伺服器的電腦名稱，然後按一下 [連接] 來進行連接。 如果您要連線至具名執行個體，請使用電腦名稱，後面依序加上反斜線及執行個體名稱。 例如： `mycomputer\myinstance` 。 如果要連接到 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)]，請使用電腦名稱並於後面加上 **\sqlexpress**。
  
許多因素都可能影響連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的能力。 如需說明，請參閱下列資源：

- [教學課程第 1 課：連接至資料庫引擎](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  

- [對 SQL Server 資料庫引擎的連線進行疑難排解](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  

- [解決 SQL Server 的連線錯誤](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)   
  
## <a name="options"></a>選項。

**伺服器類型**  
從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../../includes/ssde_md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [ [!INCLUDE[ssDE](../../includes/ssde_md.md)]]、[ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)]]、[ [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]]、[ [!INCLUDE[ssEW](../../includes/ssew-md.md)]] 或 [ [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ]，再開始註冊新的伺服器。  
  
**伺服器名稱**  
選取要連接的伺服器執行個體。 預設會顯示上次連接的伺服器執行個體。  
  
> [!NOTE]  
> 若要連線至 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 的使用中使用者執行個體，請使用指定管道名稱的具名管道通訊協定 (例如 `np:\\.\pipe\3C3DF6B1-2262-47\tsql\query`) 來連線。 如需詳細資訊，請參閱 [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] 文件。  

> [!NOTE]  
> 連線通常會保存在「最近使用 (MRU)」歷程記錄中。 若要從 MRU 移除項目，只需按一下 [伺服器名稱] 下拉式方塊、選取要移除的伺服器名稱，然後按 **DEL** 鍵即可。  

**驗證**  
SSMS 目前的版本提供五種驗證模式，可在連線至 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的執行個體時使用。 如果您的 [驗證] 對話方塊與下列清單不相符，請至[下載 SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) 下載最新版本的 SSMS。  

> **Windows 驗證**  
> [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
> 
> **SQL Server 驗證**  
> 當使用者從非信任連接以指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。 可能的話，請使用 Windows 驗證或 Active Directory 密碼驗證。  
> 
> **Azure Active Directory - MFA 通用支援**  
> [Active Directory - 與 MFA 通用] 是支援 Azure Multi-Factor Authentication (MFA) 的互動式工作流程。 Azure MFA 有助於保護資料和應用程式的存取，同時又滿足使用者對簡單登入程序的需求。 它提供增強式驗證與一系列簡單的驗證選項 - 電話、簡訊、智慧卡與 PIN，或行動應用程式通知，讓使用者選擇他們喜好的方法。 當使用者帳戶進行 MFA 設定時，互動式驗證工作流程會透過快顯對話方塊、使用智慧卡等，要求額外的使用者互動。當使用者帳戶進行 MFA 設定時，使用者必須選取 Azure 通用驗證才能連接。 如果使用者帳戶不需要 MFA，使用者仍然可以使用其他兩個 Azure Active Directory 驗證選項。 如需詳細資訊，請參閱 [適用於與 SQL Database 和 SQL 資料倉儲搭配使用之 Azure AD MFA 的 SSMS 支援](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)。 如有必要，您可以按一下 [選項]，選取 [連線內容]索引標籤，然後完成 [AD 網域或租用戶識別碼] 方塊，來變更驗證登入的網域。  
> 
> **Azure Active Directory - 密碼**  
> Azure Active Directory 驗證系統使用 Azure Active Directory (Azure AD) 中的身分識別來連線至 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  如果您用來登入 Windows 的認證來自未與 Azure 同盟的網域，或是使用 Azure AD 根據初始或用戶端網域來使用 Azure AD 驗證時，請使用此方法連線至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 如需詳細資訊，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
> 
> **Active Directory - 整合式**  
> Azure Active Directory 驗證系統使用 Azure Active Directory (Azure AD) 中的身分識別來連線至 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 如果您使用來自同盟網域的 Azure Active Directory 認證登入 Windows，請使用此方法連線至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 如需詳細資訊，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。  
  
**使用者名稱**  
要用來連接的 Windows 使用者名稱。 只有在已選擇使用 [Active Directory - 密碼] 驗證進行連線時，才可以使用此選項。 當選取 [Windows 驗證] 或 [Azure Active Directory - 整合式] 驗證時，其為唯讀狀態。  
  
**登入**  
輸入要用來連接的登入。 這個選項只有在您選取了使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證] 或 [Active Directory 密碼驗證] 連線時才可以使用。  
  
> [!NOTE]  
> 連線通常會保存在「最近使用 (MRU)」歷程記錄中。 若要從 MRU 移除項目，只需按一下 [伺服器名稱] 下拉式方塊、選取要移除的伺服器名稱，然後按 **DEL** 鍵即可。 這是在 SSMS 18.5 中引進。

**密碼**  
輸入登入的密碼。 這個選項只有在您選取了使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證] 或 [Active Directory - 密碼] 驗證連線時才可以編輯。  

**[連接]**  
按一下以連線至伺服器。

**選項**  
按一下以顯示 [連線內容] 與 [其他連線參數] 索引標籤。
