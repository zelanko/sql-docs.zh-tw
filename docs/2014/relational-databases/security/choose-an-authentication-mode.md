---
title: 選擇驗證模式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.authenticationmode.f1
helpviewer_keywords:
- sa account
- authentication modes
- trusted connection
- SQL Server Installation Wizard, Authentication Mode page
- choose authentication mode
- authentication [SQL Server], choosing a mode
- Windows authentication [SQL Server]
- mixed mode authentication
- mixed authentication mode
- SQL authentication mode
ms.assetid: ff7a6a48-3d38-4209-aa0f-7d6c0a8c64ef
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 5e06e33048548baad245bee78b9989e9c4cc700b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63011336"
---
# <a name="choose-an-authentication-mode"></a>選擇驗證模式
  在安裝期間，您必須選取 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的驗證模式。 有兩個可能的模式：Windows 驗證模式和混合的模式。 Windows 驗證模式會啟用 Windows 驗證並停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 混合模式會啟用 Windows 驗證及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 Windows 驗證一定可用而且無法停用。  
  
## <a name="configuring-the-authentication-mode"></a>設定驗證模式  
 如果您在安裝期間選取混合模式驗證，就必須為名為 sa 的內建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員帳戶提供並確認增強式密碼。 sa 帳戶會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接。  
  
 如果您在安裝期間選取 Windows 驗證，安裝程式就會針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證建立 sa 帳戶，但是此帳戶是停用的。 如果您之後變更為混合模式驗證，而且想要使用 sa 帳戶，就必須啟用此帳戶。 任何 Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶都可以設定為系統管理員。 由於 sa 帳戶是已知的而且經常成為惡意使用者的攻擊目標，因此除非您的應用程式需要 sa 帳戶，否則請勿啟用此帳戶。 此外，絕對不可針對 sa 帳戶設定空白或弱式密碼。 若要從 Windows 驗證模式變更為混合模式驗證，並且使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請參閱 [變更伺服器驗證模式](../../database-engine/configure-windows/change-server-authentication-mode.md)。  
  
## <a name="connecting-through-windows-authentication"></a>透過 Windows 驗證進行連接  
 當使用者透過 Windows 使用者帳戶連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用作業系統中的 Windows 主體 Token 來驗證帳戶名稱和密碼。 這代表 Windows 已確認使用者身分。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會要求您輸入密碼，而且不會執行身分驗證。 Windows 驗證是預設驗證模式，而且比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證更安全。 Windows 驗證會使用 Kerberos 安全性通訊協定、在增強式密碼的複雜驗證方面提供密碼原則強化、提供對帳戶鎖定的支援，而且支援密碼逾期。 使用 Windows 驗證所建立的連接有時候稱為信任連接，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會信任 Windows 所提供的認證。  
  
 使用 Windows 驗證，可以在網域層級建立 Windows 群組，也可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立整個群組的登入。 從網域層級管理存取可簡化帳戶管理。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="connecting-through-sql-server-authentication"></a>透過 SQL Server 驗證進行連接  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立不是以 Windows 使用者帳戶為基礎的登入。 其使用者名稱和密碼都是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所建立而且儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接的使用者必須在每次連接時提供其認證 (登入和密碼)。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證時，所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶都必須設定增強式密碼。 如需增強式密碼的指導方針，請參閱 [增強式密碼](strong-passwords.md)。  
  
 有三個選擇性密碼原則可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入使用。  
  
-   使用者必須在下次登入時變更密碼  
  
     要求使用者在下次連接時變更密碼。 變更密碼的功能是由 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]提供的。 如果使用這個選項，協力廠商軟體開發人員應該提供這項功能。  
  
-   強制執行密碼逾期  
  
     針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入強制執行電腦的最大密碼存在時間原則。  
  
-   強制執行密碼原則  
  
     針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入強制執行電腦的 Windows 密碼原則。 這包括密碼長度和複雜性。 這項功能相依於 `NetValidatePasswordPolicy` API，而這個 API 只有 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 和更新版本才有。  
  
#### <a name="to-determine-the-password-policies-of-the-local-computer"></a>判斷本機電腦的密碼原則  
  
1.  在 **[開始]** 功能表上，按一下 **[執行]** 。  
  
2.  在 [**執行**] 對話方塊中，輸入`secpol.msc`，然後按一下 **[確定]** 。  
  
3.  在 [本機安全性設定]  應用程式中，依序展開 [安全性設定]  和 [帳戶原則]  ，然後按一下 [密碼原則]  。  
  
     密碼原則就會描述在結果窗格中。  
  
### <a name="disadvantages-of-sql-server-authentication"></a>SQL Server 驗證的缺點  
  
-   如果某位使用者是擁有 Windows 登入和密碼的 Windows 網域使用者，則仍然必須提供其他 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 登入和密碼才能連接。 追蹤多個名稱和密碼對於許多使用者而言很困難。 此外，每次連接至資料庫就必須提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證可能會造成困擾。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證無法使用 Kerberos 安全性通訊協定。  
  
-   Windows 提供了不適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的其他密碼原則。  
  
-   加密的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入密碼在連接時必須透過網路傳遞。 自動連接的某些應用程式會將密碼儲存在用戶端。 這些是額外的攻擊點。  
  
### <a name="advantages-of-sql-server-authentication"></a>SQL Server 驗證的優點  
  
-   可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的舊版應用程式以及協力廠商所提供的應用程式。  
  
-   可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援具有混合作業系統的環境，其中 Windows 網域無法驗證所有使用者。  
  
-   可讓使用者從未知或未受信任的網域連接。 例如，既有客戶使用所指派 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入連接來接收訂單狀態的應用程式。  
  
-   可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 Web 架構應用程式，其中使用者會建立自己的識別。  
  
-   可讓軟體開發人員根據已知的現有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，使用複雜的權限階層來散發其應用程式。  
  
    > [!NOTE]  
    >  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證不會限制安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦上本機管理員的權限。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
