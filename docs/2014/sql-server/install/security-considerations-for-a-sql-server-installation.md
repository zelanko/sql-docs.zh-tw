---
title: SQL Server 安裝的安全性考量 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [SQL Server]
- server message blocks [SQL Server]
- disabling protocols
- security [SQL Server], installations
- protocols [SQL Server], disabling
- NetBIOS [SQL Server]
- services [SQL Server], security
- SMB [SQL Server]
- isolating services [SQL Server]
- Setup [SQL Server], security
- low SQL Server installation privileges
- NTFS [SQL Server]
- physical security [SQL Server]
- file system security [SQL Server]
- installing SQL Server, security
ms.assetid: cf96155f-30a8-48b7-8d6b-24ce90dafdc7
caps.latest.revision: 48
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8d17d471020a4b6960307c6718caf4624579da8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166099"
---
# <a name="security-considerations-for-a-sql-server-installation"></a>SQL Server 安裝的安全性考量
  安全性對於每一個產品和每一項業務都很重要。 只要遵循簡單的最佳做法，就可以避免許多安全性漏洞。 本主題會討論一些您在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前和安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後應該考慮的安全性最佳做法。 特定功能的參考主題中會包括那些功能的安全性指南。  
  
## <a name="before-installing-includessnoversionincludesssnoversion-mdmd"></a>安裝之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 設定伺服器環境時，請遵循這些最佳做法：  
  
-   [加強實體安全性](#physical_security)  
  
-   [使用防火牆](#firewalls)  
  
-   [隔離服務](#isolated_services)  
  
-   [設定安全檔案系統](#sa_with_least_privileges)  
  
-   [停用 NetBIOS 和伺服器訊息區塊](#disabled_protocols)  
  
-   [在網域控制站上安裝 SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md#Install_DC)  
  
###  <a name="physical_security"></a> Enhance Physical Security  
 實體和邏輯隔離，構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性的基礎。 若要加強 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的實體安全性，請執行下列工作：  
  
-   將伺服器放在只有獲得授權的人員能夠存取的地點。  
  
-   將主控資料庫的電腦放在實體保護位置中，最好是有上鎖的電腦機房，裡面有水災偵測和火災偵測或控制系統的監視功能。  
  
-   在公司內部網路的安全區域中安裝資料庫，而且請勿將 SQL Server 直接連接到網際網路。  
  
-   定期備份所有資料，並在遠端位置保護備份安全。  
  
###  <a name="firewalls"></a> Use Firewalls  
 防火牆對於保護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的安全非常重要。 如果您遵照這些方針，防火牆將是最有效的：  
  
-   將防火牆放在伺服器和網際網路之間。 啟用您的防火牆。 如果防火牆已關閉，請將它開啟。 如果防火牆已開啟，請勿將它關閉。  
  
-   將網路分割成防火牆所隔開的安全區域。 封鎖所有傳輸，然後選擇性地只准許必要的傳輸。  
  
-   在多層環境中，請使用多個防火牆來建立篩選的子網路。  
  
-   當您在 Windows 網域內安裝伺服器時，請設定內部防火牆允許 Windows 驗證。  
  
-   如果應用程式使用分散式交易，您可能必須設定防火牆，好讓 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 傳輸可以在個別 MS DTC 執行個體之間流動。 您也必須設定防火牆，好讓 MS DTC 與資源管理員 (如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 之間的傳輸可以流動。  
  
 如需預設 Windows 防火牆設定的詳細資訊以及影響 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
###  <a name="isolated_services"></a> Isolate Services  
 隔離服務減少一個遭到破壞的服務被用來破壤其他服務的風險。 若要隔離服務，請考慮下列方針：  
  
-   在個別 Windows 帳戶下執行個別的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 請盡可能針對每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務使用低權限的個別 Windows 或本機使用者帳戶。 如需詳細資訊，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
###  <a name="sa_with_least_privileges"></a> Configure a Secure File System  
 使用正確的檔案系統會增加安全性。 如果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝，您應該執行下列工作：  
  
-   使用 NTFS 檔案系統 (NTFS)。 NTFS 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的慣用檔案系統，因為它比 FAT 檔案系統更穩定，而且具有更高的可復原性。 NTFS 也會啟用一些安全性選項，例如檔案和目錄存取控制清單 (ACL) 及加密檔案系統 (EFS) 檔案加密。 在安裝期間， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會在偵測到 NTFS 時，對登錄機碼和檔案設定適當的 ACL。 這些權限不應該變更。 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本可能不支援在含有 FAT 檔案系統的電腦上安裝。  
  
    > [!NOTE]  
    >  如果您使用 EFS，資料庫檔案將會在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帳戶識別下加密。 只有這個帳戶才能夠解密該檔案。 如果您必須變更執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帳戶，您應該先在舊的帳戶下解密檔案，然後在新的帳戶下重新加密檔案。  
  
-   針對重要資料檔使用獨立磁碟容錯陣列 (RAID)。  
  
###  <a name="disabled_protocols"></a> Disable NetBIOS and Server Message Block  
 周邊網路中的伺服器應該停用所有非必要的通訊協定，包括 NetBIOS 和伺服器訊息區塊 (SMB) 在內。  
  
 NetBIOS 使用下列通訊埠：  
  
-   UDP/137 (NetBIOS 名稱服務)  
  
-   UDP/138 (NetBIOS 資料包服務)  
  
-   TCP/139 (NetBIOS 工作階段服務)  
  
 SMB 使用下列通訊埠：  
  
-   TCP/139  
  
-   TCP/445  
  
 Web 伺服器和網域名稱系統 (DNS) 伺服器不需要 NetBIOS 或 SMB。 在這些伺服器上，請停用這兩種通訊協定以減少使用者列舉的威脅。  
  
###  <a name="Install_DC"></a> 在網域控制站上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 基於安全性理由，不建議您在網域控制站上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會封鎖當做網域控制站之電腦上的安裝，但適用以下限制：  
  
-   您無法以本機服務帳戶在網域控制站上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域成員變成網域控制站。 在您將主機電腦變更為網域控制站之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域控制站變成網域成員。 在您將主機電腦變更為網域成員之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式無法在唯讀的網域控制站上建立安全性群組或提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。 在此狀況中，安裝程式將會失敗。  
  
## <a name="during-or-after-installation-of-includessnoversionincludesssnoversion-mdmd"></a>安裝時或安裝後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 安裝之後，您可以遵照關於帳戶和驗證模式的這些最佳做法，來加強 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的安全性：  
  
 **服務帳戶**  
  
-   使用可能的最低權限來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
-   將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務與低權限的 Windows 本機使用者帳戶或網域使用者帳戶產生關聯。  
  
-   如需詳細資訊，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
 **驗證模式**  
  
-   需要 Windows 驗證才能連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   使用 Kerberos 驗證。 如需詳細資訊，請參閱 [註冊 Kerberos 連接的服務主體名稱](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。  
  
 **增強式密碼**  
  
-   一律指派增強式密碼至`sa`帳戶。  
  
-   一律啟用檢查密碼強度和逾期的密碼原則。  
  
-   對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入一律使用增強式密碼。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 安裝期間會在 BUILTIN\Users 群組中加入一個登入。 這個登入可讓電腦上所有經過驗證的使用者以 public 角色成員的身分存取 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 執行個體。 BUILTIN\Users 登入可以安全地移除，藉此限制擁有個別登入或為其他擁有登入之 Windows 群組成員的電腦使用者對 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的存取。  
  
## <a name="see-also"></a>另請參閱  
 [硬體和 Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)   
 [網路通訊協定和網路程式庫](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)   
 [註冊 Kerberos 連接的服務主體名稱](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
  
