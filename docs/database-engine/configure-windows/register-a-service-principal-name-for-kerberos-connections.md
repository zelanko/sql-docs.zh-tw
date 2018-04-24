---
title: 註冊 Kerberos 連接的服務主體名稱 | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
caps.latest.revision: 59
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: fe8e537bb8d01784f68dd168ba84df9d6daac4db
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>註冊 Kerberos 連接的服務主體名稱
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 Kerberos 驗證，需要符合下列兩個條件：  
  
-   用戶端和伺服器電腦必須屬於相同的 Windows 網域，或在受信任的網域中。  
  
-   必須向 Active Directory 登錄「服務主要名稱」(SPN)，而 Active Directory 的角色如同 Windows 網域中的「金鑰發佈中心」。 登錄後的 SPN 會對應至啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體服務的 Windows 帳戶。 如果尚未執行 SPN 註冊或註冊作業失敗，則 Windows 安全層無法判斷與 SPN 相關聯的帳戶，因此不會使用 Kerberos 驗證。  
  
    > [!NOTE]  
    >  如果伺服器無法自動註冊 SPN，則必須手動註冊 SPN。 請參閱 [手動 SPN 註冊](#Manual)。  
  
您可以透過查詢 sys.dm_exec_connections 動態管理檢視，驗證連接是否使用 Kerberos。 請執行下列查詢並檢查 auth_scheme column 的值 (如果有啟用 Kerberos，該值將為 "KERBEROS")。  
  
```sql  
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;  
```  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 是一種診斷工具，可幫助排除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發生的 Kerberos 相關連接問題。 如需詳細資訊，請參閱 [Microsoft Kerberos Configuration Manager for SQL Server](http://www.microsoft.com/download/details.aspx?id=39046)。  
  
##  <a name="Role"></a> SPN 在驗證中的角色  
 當應用程式開啟連接並使用 Windows 驗證時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會傳遞 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦名稱、執行個體名稱，並選擇性地傳遞 SPN。 如果連接傳遞 SPN，則會在不進行任何變更的情況下使用該 SPN。  
  
 如果連接未通過 SPN，則會根據使用的通訊協定、伺服器名稱和執行個體名稱建構預設的 SPN。  
  
 在前述兩種狀況中，SPN 都會傳送到「金鑰散佈中心」，以取得安全性 Token 來驗證連接。 如果無法取得安全性 Token，則驗證會使用 NTLM。  
  
 服務主要名稱 (SPN) 是用戶端用以唯一識別服務執行個體的名稱。 Kerberos 驗證服務可以使用 SPN 來驗證服務。 當用戶端想要連接到服務時，它會尋找服務的執行個體、撰寫該執行個體的 SPN、連接到服務，然後呈現服務的 SPN 以進行驗證。  
  
> [!NOTE]  
>  本主題提供的資訊也適用於使用群集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態。  
  
 Windows 驗證是 SQL Server 驗證使用者的慣用方法。 使用 Windows 驗證的用戶端是透過 NTLM 或 Kerberos 進行驗證。 在 Active Directory 環境中，永遠會先嘗試 Kerberos 驗證。 使用具名管道的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 使用者無法使用 Kerberos 驗證。  
  
##  <a name="Permissions"></a> 權限  
 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務啟動時，它會嘗試註冊服務主體名稱 (SPN)。 如果啟動 SQL Server 的帳戶無權在 Active Directory 網域服務中註冊 SPN，這個呼叫就會失敗，而且在應用程式事件記錄檔與 SQL Server 錯誤記錄檔中會記錄警告訊息。 若要註冊 SPN， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須在內建帳戶下執行，例如 Local System (不建議) 或 NETWORK SERVICE，或是在具有註冊 SPN 之權限的帳戶下執行 (例如網域管理員帳戶)。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在  [!INCLUDE[win7](../../includes/win7-md.md)] 或  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 作業系統上執行時，您可以使用虛擬帳戶或受管理的服務帳戶 (MSA) 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 虛擬帳戶和 MSA 都可以註冊 SPN。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並未在這些帳戶的其中一個之下執行，SPN 就不會在啟動時註冊，而且網域管理員必須手動註冊 SPN。  
  
> [!NOTE]  
>  當 Windows 網域設定為在小於 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Windows Server 2008 R2 的功能層級上執行時，受管理的服務帳戶將沒有針對 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務註冊 SPN 的必要權限。 如果需要 Kerberos 驗證，則網域管理員應該在受管理的服務帳戶上手動註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SPN。  
  
 KB 文件 [How to use Kerberos authentication in SQL Server](http://support.microsoft.com/kb/319723)(如何在 SQL Server 中使用 Kerberos 驗證) 包含如何將讀取或寫入權限授與非網域管理員帳戶之 SPN 的資訊。  
  
 [How to Implement Kerberos Constrained Delegation with SQL Server 2008](http://technet.microsoft.com/library/ee191523.aspx)(如何使用 SQL Server 2008 實作 Kerberos 受限委派) 提供額外資訊  
  
##  <a name="Formats"></a> SPN 格式  
 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開始，SPN 格式就有了變動，以便能夠在 TCP/IP、具名管道和共用記憶體上支援 Kerberos 驗證。 具名和預設執行個體支援的 SPN 格式如下所示。  
  
**具名執行個體**  
  
-   **MSSQLSvc/\<FQDN>:[\<連接埠> | \<執行個體名稱>]**，其中：  
  
    -   **MSSQLSvc** 是所註冊的服務。  
  
    -   **\<FQDN>** 是伺服器的完整網域名稱。  
  
    -   **\<連接埠>** 是 TCP 通訊埠編號。  
  
    -   **\<執行個體名稱>** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
**預設執行個體**  
  
-   **MSSQLSvc/\<FQDN>:\<連接埠>** | **MSSQLSvc/\<FQDN>**，其中：  
  
    -   **MSSQLSvc** 是所註冊的服務。  
  
    -   **\<FQDN>** 是伺服器的完整網域名稱。  
  
    -   **\<連接埠>** 是 TCP 通訊埠編號。  
  
    > [!NOTE]
    > 新的 SPN 格式不需要通訊埠編號。 這表示，不使用通訊埠編號的多重通訊埠伺服器或通訊協定可以使用 Kerberos 驗證。  
   
|||  
|-|-|  
|MSSQLSvc/\<FQDN>:<port>|使用 TCP 時，此為提供者產生的預設 SPN。 \<連接埠> 是 TCP 通訊埠編號。|  
|MSSQLSvc/\<FQDN>|使用 TCP 以外的通訊協定時，此為提供者針對預設執行個體所產生的預設 SPN。 \<FQDN> 是完整網域名稱。|  
|MSSQLSvc/\<FQDN>:\<執行個體名稱>|使用 TCP 以外的通訊協定時，此為提供者針對具名執行個體所產生的預設 SPN。 \<執行個體名稱> 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|  

> [!NOTE]  
> 在 TCP/IP 連接的情況下，由於 TCP 通訊埠包含於 SPN 中，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須啟用 TCP 通訊協定，使用者才能使用 Kerberos 驗證進行連接。 

##  <a name="Auto"></a> 自動 SPN 註冊  
 當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體啟動時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的 SPN。 當此執行個體停止時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會嘗試取消註冊 SPN。 如果是 TCP/IP 連接，SPN 會以 MSSQLSvc/\<FQDN>:\<tcpport> 格式註冊。具名執行個體和預設執行個體都會註冊為 MSSQLSvc (根據 \<tcpport> 值來區分執行個體)。  
  
 如果是支援 Kerberos 的其他連接，SPN 會針對具名執行個體來以 MSSQLSvc/\<FQDN>/\<執行個體名稱> 格式註冊。 用來註冊預設執行個體的格式為 MSSQLSvc/\<FQDN>。  
  
 如果服務帳戶缺少這些動作所需的權限，可能需要手動介入才能註冊或取消註冊 SPN。  
  
##  <a name="Manual"></a> 手動 SPN 註冊  
若要手動註冊 SPN，管理員必須使用 Microsoft [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 支援工具所隨附的 Setspn.exe 工具。 如需詳細資訊，請參閱 [Windows Server 2003 Service Pack 1 支援工具](http://support.microsoft.com/kb/892777) KB 文件。  
  
Setspn.exe 是一個命令列工具，可讓您讀取、修改及刪除服務主要名稱 (SPN) 目錄屬性。 此工具也可讓您檢視目前的 SPN、重設此帳戶的預設 SPN，或是加入或刪除補充 SPN。  
  
下列範例說明使用網域使用者帳戶手動註冊 SPN，以進行 TCP/IP 連線的語法：  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```  
  
> [!NOTE]
> 如果 SPN 已存在，必須先將它刪除之後才可以重新註冊。 您可以搭配 `setspn` 參數使用 `-D` 命令來進行這項處理。 下列範例說明如何手動註冊以新執行個體為基礎的 SPN。 若是使用網域使用者帳戶的預設執行個體，請使用：  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
若為具名執行個體，請使用：  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com/instancename redmond\accountname  
```  
  
##  <a name="Client"></a> 用戶端連接  
 用戶端驅動程式內可支援使用者指定的 SPN。 但是，如果未提供 SPN，將會根據用戶端連接的類型來自動產生 SPN。 如果是 TCP 連接，將會針對具名和預設執行個體使用 *MSSQLSvc*/*FQDN*:[*port*] 格式的 SPN。  
  
如果是具名管道和共用記憶體的連線，將會針對具名執行個體使用 *MSSQLSvc/\<FQDN>:\<執行個體名稱>* 格式的 SPN，並針對預設執行個體使用 *MSSQLSvc/\<FQDN>* 格式的 SPN。  
  
 **將服務帳戶當做 SPN 使用**  
  
服務帳戶可以當做 SPN 使用， 它們是透過 Kerberos 驗證的連接屬性所指定，而且會使用以下的格式：  
  
-   適用於網域使用者帳戶的 **username@domain** 或 **domain\username**  
  
-   適用於電腦網域帳戶 (如本機系統或 NETWORK SERVICES) 的 **machine$@domain** 或 **host\FQDN**。  
  
若要判斷連接的驗證方法，請執行下列查詢。  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
##  <a name="Defaults"></a> 驗證預設值  
 下表說明根據 SPN 註冊狀況所使用的驗證預設值。  
  
|狀況|驗證方法|  
|--------------|---------------------------|  
|SPN 會對應到正確的網域帳戶、虛擬帳戶、MSA 或內建帳戶。 例如，Local System 或 NETWORK SERVICE。|本機連接會使用 NTLM，遠端連接則使用 Kerberos。|  
|SPN 是正確的網域帳戶、虛擬帳戶、MSA 或內建帳戶。|本機連接會使用 NTLM，遠端連接則使用 Kerberos。|  
|SPN 對應到不正確的網域帳戶、虛擬帳戶、MSA 或內建帳戶。|驗證失敗。|  
|SPN 查閱失敗或是未對應到正確的網域帳戶、虛擬帳戶、MSA 或內建帳戶，或者不是正確的網域帳戶、虛擬帳戶、MSA 或內建帳戶。|本機和遠端連接都會使用 NTLM。|  
  
> [!NOTE]  
> 「正確」表示已註冊之 SPN 對應的帳戶就是執行 SQL Server 服務所使用的帳戶。  
  
##  <a name="Comments"></a> 註解  
 專用管理員連接 (DAC) 使用以執行個體名稱為基礎的 SPN。 如果該 SPN 註冊成功的話，Kerberos 驗證便可搭配 DAC 使用。 另外，使用者也可將此帳戶名稱指定為 SPN。  
  
 如果 SPN 註冊在啟動期間失敗，則此失敗會記錄在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中，而啟動會繼續進行。  
  
 如果 SPN 取消註冊在關閉期間失敗，則此失敗會記錄在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中，而關閉作業會繼續進行。  
  
## <a name="see-also"></a>另請參閱  
 [用戶端連接中的服務主要名稱 &#40;SPN&#41; 支援](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)   
 [用戶端連接 &#40;OLE DB&#41; 中的服務主體名稱 &#40;SPN&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)   
 [用戶端連接 &#40;ODBC&#41; 中的服務主體名稱 &#40;SPN&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)   
 [SQL Server Native Client 功能](../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [管理 Reporting Services 環境中的 Kerberos 驗證問題](http://technet.microsoft.com/library/ff679930.aspx)  
  
  
