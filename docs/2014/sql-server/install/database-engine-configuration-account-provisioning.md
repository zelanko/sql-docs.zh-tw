---
title: Database Engine 組態-帳戶提供 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69885ad9affb87ea160231fa6f6d42d0fef7ea6c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099048"
---
# <a name="database-engine-configuration---account-provisioning"></a>Database Engine 組態 - 帳戶提供
  您可以使用此頁面來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性模式，以及加入 Windows 使用者或群組做為 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的管理員。  
  
## <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>執行[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時的考量  
 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上， **BUILTIN\Administrators** 群組是提供成 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的登入，而且本機 Administrators 群組的成員可以使用其管理員認證登入。 使用較高的權限並非最佳做法。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中， **BUILTIN\Administrators** 群組並未提供成登入。 因此，您應該為每個管理使用者建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，並在安裝新的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]執行個體期間，將該登入加入至系統管理員 (sysadmin) 固定伺服器角色。 您也應該針對用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式作業的 Windows 帳戶進行上述作業。 這些作業包括複寫代理程式作業。  
  
## <a name="options"></a>選項。  
 **安全性模式** - 為您的安裝選取 Windows 驗證或混合模式驗證。  
  
 **Windows 主體提供** - 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，Windows Builtin\Administrator 本機群組置於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員伺服器角色中，可有效授與 Windows 管理員對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的存取權。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，Builtin\Administrator 群組不會提供在系統管理員 (sysadmin) 伺服器角色中。 您應該改在安裝期間針對新的安裝明確提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員。  
  
> [!IMPORTANT]  
>  您必須在安裝期間針對新的安裝明確提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員。 要等到您完成此步驟之後，安裝程式才允許您繼續。  
  
 **指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理員** - 您必須為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體指定至少一個 Windows 主體。 若要加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式執行所用的帳戶，請按一下 [目前使用者] 按鈕。 若要從系統管理員清單中加入或移除帳戶，請按一下 **[加入]** 或 **[移除]**，然後編輯在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中將會有管理員權限的使用者、群組或電腦清單。  
  
 當您完成清單的編輯之後，請按一下 [確定]，然後在組態對話方塊中確認管理員的清單。 當此清單完成時，請按 **[下一步]**。  
  
 如果您選取混合模式驗證，您必須為內建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員 (SA) 帳戶提供登入認證。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 驗證模式**  
 當使用者透過 Windows 使用者帳戶連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用作業系統中的 Windows 主體 Token 來驗證帳戶名稱和密碼。 這是預設驗證模式，比混合模式更加安全。 Windows 驗證利用 Kerberos 安全性通訊協定，在增強式密碼的複雜驗證方面提供密碼原則強化，並提供對帳戶鎖定的支援，同時支援密碼逾期。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 絕對不可設定空白或弱式 sa 密碼。  
  
 **混合模式 (Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證)**  
 允許使用者利用 Windows 驗證或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來連接。 透過 Windows 使用者帳戶連接的使用者可以使用 Windows 已驗證的信任連接。  
  
 如果您必須選擇混合模式驗證，而且需要使用 SQL 登入來配合舊版應用程式，則您必須為所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶設定增強式密碼。  
  
> [!NOTE]  
>  提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的目的，只是為了回溯相容性。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **輸入密碼**  
 輸入並確認系統管理員 (sa) 登入。 密碼是對抗入侵者的第一道防線，因此，設定增強式密碼對於系統的安全性很重要。 不得設定空白或弱式 sa 密碼。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密碼可包含 1 到 128 個字元，包括字母、符號和數字的任意組合。 如果您選擇混合模式驗證，則在您可以繼續到安裝精靈的下一頁之前，必須先輸入增強式 sa 密碼。  
  
 **增強式密碼方針**  
 增強式密碼不會很快被猜到，使用電腦程式也不容易破解。 增強式密碼不得使用禁止條件或詞彙，包括：  
  
-   空白或 NULL 條件  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 增強式密碼不得為與安裝電腦相關的下列詞彙：  
  
-   目前登入機器的使用者名稱。  
  
-   電腦名稱。  
  
 增強式密碼的長度必須為 8 個字元以上，且至少滿足下列四項準則中的三項：  
  
-   必須包含大寫字母。  
  
-   必須包含小寫字母。  
  
-   必須包含數字。  
  
-   必須包含非英數字元；例如 #、% 或 ^。  
  
 此頁面中輸入的密碼必須符合增強式密碼原則的需求。 如果您有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的任何自動化作業，請確定此密碼符合增強式密碼原則的需求。  
  
## <a name="related-content"></a>相關內容  
 如需有關選擇 Windows 驗證和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證之比較的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的**選擇驗證模式**主題。  
  
 如需選擇帳戶以執行 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的**設定 Windows 服務帳戶與權限**主題。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
