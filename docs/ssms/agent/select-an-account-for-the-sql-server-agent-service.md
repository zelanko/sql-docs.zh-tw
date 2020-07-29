---
title: 選取 SQL Server Agent 服務的帳戶
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, accounts
- startup accounts [SQL Server]
- SQL Server Agent service, accounts
- accounts [SQL Server], SQL Server Agent
- Windows groups [SQL Server Agent]
- SQL Server Agent, permissions
- members [SQL Server], SQL Server Agent service
- Windows domain accounts [SQL Server]
- security [SQL Server], SQL Server Agent
ms.assetid: fe658e32-9e6b-4147-a189-7adc3bd28fe7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 05/04/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4356764f50b816a05e9bcfbfb294c65cdc8080fe
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85644683"
---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>選取 SQL Server Agent 服務的帳戶

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

服務啟動帳戶會定義 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Agent 用來執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 帳戶及其網路權限。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會以指定的使用者帳戶執行。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員選擇下列選項，藉此選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的帳戶：  
  
-   **內建帳戶**。 您可從下列內建 Windows 服務帳戶的清單中進行選擇：  
  
    -   **本機系統** 帳戶。 這個帳戶的名稱是 NT AUTHORITY\System。 它是功能強大的帳戶，可不受限制地存取所有本機系統資源。 這個帳戶是本機電腦上的 Windows **Administrators** 群組成員，因此也是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **系統管理員**固定伺服器角色的成員  
  
        > [!IMPORTANT]  
        > [本機系統帳戶]  選項僅用於回溯相容性。 本機系統帳戶具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 不需要的權限。 避免以本機系統帳戶身分執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。 為了改善安全性，請搭配使用 Windows 網域帳戶與下節「Windows 網域帳戶權限」所列的權限。  
  
-   **這個帳戶**。 可讓您指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務用來執行的 Windows 網域帳戶。 我們建議您選擇非 Windows **Administrators** 群組成員的 Windows 使用者帳戶。 然而， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶不是本機 **Administrators** 群組的成員時，則會限制多伺服器管理的使用。 如需詳細資訊，請參閱本主題稍後的＜支援的服務帳戶類型＞。  
  
## <a name="windows-domain-account-permissions"></a>Windows 網域帳戶權限  
為了改善安全性，請選取 [這個帳戶]  ，以指定 Windows 網域帳戶。 您指定的 Windows 網域帳戶必須具有下列權限：  
  
-   在所有 Windows 版本中，以服務方式登入的權限 (SeServiceLogonRight)  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是網域控制站上 Pre-Windows 2000 Compatible Access 群組的一部分，否則，非 Windows Administrators 群組成員之網域使用者所擁有的作業會失敗。  
  
-   在 Windows 伺服器中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務用以執行的帳戶需要下列權限，才能支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy。  
  
    -   略過周遊檢查的權限 (SeChangeNotifyPrivilege)  
  
    -   取代處理序層級 Token 的權限 (SeAssignPrimaryTokenPrivilege)  
  
    -   調整處理序之記憶體配額的權限 (SeIncreaseQuotaPrivilege)  
  
    -   從網路存取這台電腦的權限 (SeNetworkLogonRight)  
  
> [!NOTE]  
> 如果帳戶沒有支援 Proxy 所需的權限，則只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以建立作業。  
  
> [!NOTE]  
> 若要接收 WMI 警示通知，必須授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的服務帳戶對於包含 WMI 事件之命名空間的權限，以及 ALTER ANY EVENT NOTIFICATION 的權限。  
  
## <a name="sql-server-role-membership"></a>SQL Server 角色成員資格  
用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的帳戶必須是下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色的成員：  
  
-   帳戶必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
-   若要使用多伺服器作業處理，帳戶必須是主要伺服器上 **msdb** 資料庫角色 **TargetServersRole** 的成員。  
  
## <a name="supported-service-account-types"></a>支援的服務帳戶類型  
下表列出可用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的 Windows 帳戶類型。  
  
|服務帳戶類型|非叢集伺服器|叢集伺服器|網域控制站 (非叢集)|  
|------------------------|-------------------------|--------------------|--------------------------------------|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 網域帳戶 (Windows Administrators 群組的成員)|支援|支援|支援|  
|Windows 網域帳戶 (非管理)|支援<br /><br />請參閱下列限制 1。|支援<br /><br />請參閱下列限制 1。|支援<br /><br />請參閱下列限制 1。|  
|網路服務帳戶 (NT AUTHORITY\NetworkService)|支援<br /><br />請參閱下列限制 1、3 和 4。|不支援|不支援|  
|本機使用者帳戶 (非管理)|支援<br /><br />請參閱下列限制 1。|不支援|不適用|  
|本機系統帳戶 (NT AUTHORITY\System)|支援<br /><br />請參閱下列限制 2。|不支援|支援<br /><br />請參閱下列限制 2。|  
|本機服務帳戶 (NT AUTHORITY\LocalService)|不支援|不支援|不支援|  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>限制 1：針對多伺服器管理使用非管理帳戶  
將目標伺服器登錄到主要伺服器可能失敗，並出現下列錯誤訊息：「登錄作業失敗。」  
  
若要解決此錯誤，請重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 如需詳細資訊，請參閱 [启动、停止、暂停、继续、重启 SQL Server 服务](https://msdn.microsoft.com/32660a02-e5a1-411a-9e57-7066ca459df6)。  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>限制 2：針對多伺服器管理使用本機系統帳戶  
當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務在本機系統帳戶下執行時支援多伺服器管理，但前提是主要伺服器和目標伺服器都必須位於相同電腦上。 如果您使用此組態，則當您在主要伺服器上編列目標伺服器時會傳回下列訊息：  
  
「請確定 <目標伺服器電腦名稱>  的代理程式啟動帳戶有權限以 targetServer 的身分登入」。  
  
您可以忽略此參考訊息。 編列作業應該順利完成。 如需詳細資訊，請參閱 [建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)。  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>限制 3：在網路服務帳戶為 SQL Server 使用者時使用它  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果您是在網路服務帳戶之下執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務，而且已明確授與網路服務帳戶存取權限，以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的身分登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，則 Agent 可能無法啟動。  
  
若要解決此問題，請將執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦重新開機。 這個動作只需要做一次。  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>限制 4：當 SQL Server Reporting Services 在相同電腦上執行時，使用網路服務帳戶  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果您是在網路服務帳戶之下執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務，且 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 也在相同電腦上執行，則 Agent 可能無法啟動。  
  
若要解決此問題，請將執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦重新開機，然後重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 這個動作只需要做一次。  
  
## <a name="common-tasks"></a>一般工作  
**若要指定 SQL Server Agent 服務的啟動帳戶**  
  
-   [設定 SQL Server Agent 的服務啟動帳戶 &#40;SQL Server 組態管理員&#41;](../../ssms/agent/set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
**若要指定 SQL Server Agent 的郵件設定檔**  
  
-   [操作說明：設定 SQL Server Agent Mail 使用 Database Mail](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
> [!NOTE]  
> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 必須在啟動作業系統時啟動。  
  
## <a name="see-also"></a>另請參閱  
[設定 Windows 服務帳戶](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
[使用 SQL 電腦管理員管理服務](https://msdn.microsoft.com/78dee169-df0c-4c95-9af7-bf033bc9fdc6)  
[實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)  
  
