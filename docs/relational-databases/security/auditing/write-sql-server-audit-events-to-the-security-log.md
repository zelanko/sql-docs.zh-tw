---
title: 將 SQL Server Audit 事件寫入安全性記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 09/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], Security Log
- server audit [SQL Server]
- audits [SQL Server], writing to Security Log
- security logs [SQL Server]
ms.assetid: 6fabeea3-7a42-4769-a0f3-7e04daada314
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 401da6b1db47b518aa0bbf2f715e6044cf891c59
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="write-sql-server-audit-events-to-the-security-log"></a>將 SQL Server Audit 事件寫入安全性記錄檔  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在高度安全性的環境中，Windows 安全性記錄檔是寫入記錄物件存取之事件的適當位置。 雖然支援其他稽核位置，但是這些位置容易遭算改。  
  
 將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 伺服器稽核寫入 Windows 安全性記錄檔有兩個重要需求：  
  
-   稽核物件存取設定必須設定為可擷取事件。 稽核原則工具 (`auditpol.exe`) 會在 **audit object access** 類別目錄中公開各種子原則設定。 若要允許 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 稽核物件存取，請設定 **application generated** 設定。  
-   執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務所使用的帳戶必須擁有 [產生安全性稽核]  權限，才能寫入 Windows 安全性記錄檔。 根據預設，LOCAL SERVICE 和 NETWORK SERVICE 帳戶都擁有這個權限。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 是在其中一個帳戶底下執行，就不需要進行這個步驟。  
-   為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶提供登錄區的完整權限`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Security`。  

  > [!IMPORTANT]  
  > [!INCLUDE[ssnoteregistry-md](../../../includes/ssnoteregistry-md.md)]   
  
如果 Windows 稽核原則設定為寫入 Windows 安全性記錄檔，它就可能會影響 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 稽核，而且如果稽核原則的設定不正確，甚至可能會遺失事件。 一般而言，Windows 安全性記錄檔會設定為覆寫較舊的事件。 這樣做會保留最近的事件。 不過，如果 Windows 安全性記錄檔並非設定為覆寫較舊的事件，只要安全性記錄檔已滿，系統就會發出 Windows 事件 1104 (記錄檔已滿)。 此時：  
-   系統將不會記錄其他安全性事件。  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 將無法偵測出系統無法在安全性記錄檔中記錄事件，進而導致可能遺失稽核事件。  
-   在方塊管理員修正安全性記錄檔之後，記錄行為才會返回正常狀態。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 電腦的管理員應該了解安全性記錄檔的本機設定可以由網域原則覆寫。 在此情況下，網域原則可能會覆寫子類別目錄設定 (**auditpol /get /subcategory:"application generated"**)。 這可能會影響 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 記錄事件的功能，讓它無法偵測出系統無法繼續記錄 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 正嘗試稽核的事件。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須是 Windows 管理員才能設定這些設定。  
  
##  <a name="auditpolAccess"></a> 使用 auditpol 在 Windows 中設定稽核物件存取設定  
  
1.  以系統管理權限開啟命令提示字元。  
  
    1.  在 [開始] 功能表上，依序指向 [所有程式] 和 [附屬應用程式]、以滑鼠右鍵按一下 [命令提示字元]，然後按一下 [以系統管理員身分執行]。  
  
    2.  如果開啟 **[使用者帳戶控制]** 對話方塊，請按一下 **[繼續]**。  
  
2.  執行下列陳述式，以便啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的稽核。  
  
    ```  
    auditpol /set /subcategory:"application generated" /success:enable /failure:enable  
    ```  
  
3.  關閉 [命令提示字元] 視窗。  
  
##  <a name="secpolAccess"></a> 使用 secpol 將 generate security audits 權限授與帳戶  
  
1.  在任何 Windows 作業系統的 **[開始]** 功能表上，按一下 **[執行]**。  
  
2.  輸入 **secpol.msc** ，然後按一下 **[確定]**。 如果出現 **[使用者存取控制]** 對話方塊，請按一下 **[繼續]**。  
  
3.  在本機安全性原則工具中，依序展開 **[安全性設定]** 和 **[本機原則]**，然後按一下 **[使用者權限指派]**。  
  
4.  在結果窗格中，按兩下 [產生安全性稽核]。  
  
5.  在 **[本機安全性設定]** 索引標籤上，按一下 **[新增使用者或群組]**。  
  
6.  在 [選取使用者、電腦或群組] 對話方塊中，輸入使用者帳戶的名稱 (例如 **domain1\user1**) 並按一下 [確定]，或按一下 [進階] 並搜尋帳戶。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
8.  關閉安全性原則工具。  
  
9. 重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以啟用此設定。  
  
##  <a name="secpolPermission"></a> 使用 secpol 在 Windows 中設定稽核物件存取設定  
  
1.  如果作業系統是 [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] 或 Windows Server 2008 之前的版本，請在 **[開始]** 功能表上，按一下 **[執行]**。  
  
2.  輸入 **secpol.msc** ，然後按一下 **[確定]**。 如果出現 **[使用者存取控制]** 對話方塊，請按一下 **[繼續]**。  
  
3.  在本機安全性原則工具中，依序展開 **[安全性設定]** 和 **[本機原則]**，然後按一下 **[稽核原則]**。  
  
4.  在結果窗格中，按兩下 [稽核物件存取]。  
  
5.  在 **[本機安全性設定]** 索引標籤的 **[稽核這些嘗試]** 區域中，同時選取 **[成功]** 和 **[失敗]**。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  關閉安全性原則工具。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Audit &#40;Database Engine&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
