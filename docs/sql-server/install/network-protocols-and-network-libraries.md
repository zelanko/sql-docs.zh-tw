---
title: "網路通訊協定和網路程式庫 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- protocols [SQL Server]
- configuration options [SQL Server], protocols
- network libraries [SQL Server]
- protocols [SQL Server], about network protocols
- pipes [SQL Server]
- network protocols [SQL Server]
- default SQL Server configurations
- library [SQL Server]
- network protocols [SQL Server], about network protocols
- configuration options [SQL Server], libraries
ms.assetid: 8cd437f6-9af1-44ce-9cb0-4d10c83da9ce
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6a89bec1046eab92432ffa53a8de3618903f7ab6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="network-protocols-and-network-libraries"></a>網路通訊協定和網路程式庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  伺服器可以一次接聽或監視多個網路通訊協定。 然而，必須設定每個通訊協定。 如果未設定特定的通訊協定，則伺服器將無法接聽該通訊協定。 安裝之後，您可以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來變更通訊協定組態。  
  
## <a name="default-sql-server-network-configuration"></a>預設 SQL Server 網路組態  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體會設定成使用 TCP/IP 通訊埠 1433 及具名管道 \\\\.\pipe\sql\query。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體會設定成使用 TCP 動態通訊埠，而該通訊埠的通訊埠編號則由作業系統指派。  
  
 如果您無法使用動態通訊埠位址 (例如，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接必須通過已設定成通過特定通訊埠位址的防火牆伺服器時)。 選取未指派的通訊埠編號。 通訊埠編號指派是由 Internet Assigned Numbers Authority 所管理，而且列於 [http://www.iana.org](http://go.microsoft.com/fwlink/?LinkId=48844)。  
  
 為了加強安全性，安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時不會完全啟用網路連接。 若要在安裝程式完成之後啟用、停用和設定網路通訊協定，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路組態區域。  
  
## <a name="server-message-block-protocol"></a>伺服器訊息區塊通訊協定  
 周邊網路中的伺服器應該停用所有非必要的通訊協定，包括伺服器訊息區塊 (SMB) 在內。 Web 伺服器和網域名稱系統 (DNS) 伺服器不需要 SMB。 若要還擊使用者列舉方面的威脅，應該停用這個通訊協定。  
  
> [!WARNING]  
>  停用伺服器訊息區塊將會封鎖 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Windows 叢集服務存取遠端檔案共用。 如果您要或打算要執行下列其中一項，則不要停用 SMB：  
>   
>  -   使用 Windows 叢集節點和檔案共用多數仲裁模式  
> -   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間指定 SMB 檔案共用做為資料目錄  
> -   在 SMB 檔案共用上建立資料庫檔案  
  
#### <a name="to-disable-smb"></a>若要停用 SMB  
  
1.  在 [開始] 功能表上，指向 [設定]，然後按一下 [網路和撥號連線]。  
  
     以滑鼠右鍵按一下[網際網路方向連線]，然後按一下 [內容]。  
  
2.  選取 **[Client for Microsoft Networks]** 核取方塊，再按一下 **[解除安裝]**。  
  
3.  請遵照解除安裝步驟。  
  
4.  選取 **[Microsoft 網路的檔案和印表機共用]**，再按一下 **[解除安裝]**。  
  
5.  請遵照解除安裝步驟。  
  
#### <a name="to-disable-smb-on-servers-accessible-from-the-internet"></a>若要在可從網際網路存取的伺服器上停用 SMB  
  
-   在 [本機區域連線內容] 中，使用 [傳輸控制通訊協定/網際網路通訊協定 (TCP/IP)] 內容對話方塊來移除 [File and Printer Sharing for Microsoft Networks] 和 [Client for Microsoft Networks]。  
  
## <a name="endpoints"></a>端點  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 導入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接的新概念；伺服器端的連接是以 [!INCLUDE[tsql](../../includes/tsql-md.md)]*「端點」*(endpoint) 的概念來表示。 可對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 端點授與、撤銷和拒絕權限。 依預設，所有使用者對端點都有存取權限，除非權限遭到系統管理員 (sysadmin) 群組的成員或端點擁有者拒絕或撤銷。 GRANT、REVOKE 和 DENY ENDPOINT 語法使用的是系統管理員必須從端點之目錄檢視中取得的端點識別碼。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會建立所有支援之網路通訊協定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 端點，也會針對專用管理員連接建立這類端點。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 安裝程式所建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 端點如下：  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 本機電腦  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 具名管道  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 預設 TCP  
  
 如需端點的詳細資訊，請參閱[設定 Database Engine 接聽多個 TCP 通訊埠](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md)和[端點目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路設定的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》的下列文章：  
  
-   [伺服器網路組態](../../database-engine/configure-windows/server-network-configuration.md)  
  
## <a name="see-also"></a>另請參閱  
 [介面區組態](../../relational-databases/security/surface-area-configuration.md)   
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)  
  
  
