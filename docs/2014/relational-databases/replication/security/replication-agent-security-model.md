---
title: 複寫代理程式安全性模型 | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b919289d49901f64b26db0aa2d4b71eeb0e132a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62960814"
---
# <a name="replication-agent-security-model"></a>複寫代理程式安全性模型
  複寫代理程式安全性模型可允許針對複寫代理程式執行和建立連線時所使用的帳戶，進行更細微的控制：針對每個代理程式，可以指定不同的帳戶。 如需如何指定帳戶的詳細資訊，請參閱[管理複寫的登入與密碼](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)。  
  
> [!IMPORTANT]  
>  當 **系統管理員 (sysadmin)** 固定伺服器角色的成員設定複寫時，複寫代理程式可以設定為模擬 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 帳戶。 完成這項作業的方法，就是不指定複寫代理程式的登入和密碼；不過，我們不建議此方式。 反之，就安全性最佳做法而言，我們建議您為每個具有最小權限的代理程式指定帳戶；本主題稍後的＜代理程式所需的權限＞一節會描述最小權限。  
  
 跟所有可執行檔一樣，複寫代理程式也是在 Windows 帳戶的內容下執行。 代理程式會利用此帳戶來建立「Windows 整合式安全性」連接。 執行代理程式所使用的帳戶取決於代理程式的啟動方式：  
  
-   從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業啟動代理程式 (預設值)：使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業來啟動複寫代理程式時，代理程式會在您設定複寫時指定的帳戶內容下執行。 如需有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 和複寫的詳細資訊，請參閱本主題稍後的＜SQL Server Agent 下的代理程式安全性＞一節。 如需用來執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 之帳戶所需權限的資訊，請參閱[設定 SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md)。  
  
-   從 MS-DOS 命令列直接或透過指令碼啟動代理程式：代理程式會在於命令列執行代理程式之使用者的帳戶內容下執行。  
  
-   從使用 Replication Management Objects (RMO) 或 ActiveX 控制項的應用程式啟動代理程式：代理程式會在呼叫 RMO 或 ActiveX 控制項之應用程式的內容下執行。  
  
    > [!NOTE]  
    >  ActiveX 控制項已被取代。  
  
 我們建議您在 Windows 整合式安全性的內容下建立連接。 為了回溯相容性，您也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性。 如需最佳作法的相關資訊，請參閱 [Replication Security Best Practices](replication-security-best-practices.md)。  
  
## <a name="permissions-that-are-required-by-agents"></a>代理程式所需的權限  
 執行代理程式和建立連接所使用的帳戶需要多種權限。 下表描述這些權限。 我們建議每個代理程式均應使用不同的 Windows 帳戶執行，且帳戶應僅被授與所需權限。 如需與多個代理程式相關之發行集存取清單 (PAL) 的資訊，請參閱[保護發行者](secure-the-publisher.md)。  
  
> [!NOTE]  
>  某些 Windows 作業系統中的「使用者帳戶控制」(UAC) 可以防止以管理員權限存取快照集共用。 因此，您必須針對快照集代理程式、散發代理程式和合併代理程式所使用的 Windows 帳戶，明確地授與快照集共用權限。 即使 Windows 帳戶是管理員群組的成員，也必須這麼做。 如需詳細資訊，請參閱[保護快照集資料夾](secure-the-snapshot-folder.md)。  
  
|Agent|Permissions|  
|-----------|-----------------|  
|快照集代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須：<br /><br /> -至少是散發資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> -具備快照集共用的讀取、寫入及修改權限。<br /><br /> <br /><br /> 用來連接發行者的帳戶必須至少是發行集資料庫中 **db_owner** 固定資料庫角色的成員。|  
|記錄讀取器代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須至少是散發資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> 用來連接發行者的帳戶必須至少是發行集資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> 選取時`sync_type`選項*replication support only&lt*，*使用的備份初始化*，或*從 lsn 初始化*之後, 必須執行 「 記錄讀取器代理程式執行`sp_addsubscription`，讓設定指令碼會寫入至散發資料庫。 記錄讀取器代理程式必須在屬於 **系統管理員 (sysadmin)** 固定伺服器角色成員的 Windows 帳戶底下執行。 當`sync_type`選項設為*自動*，不需要任何特殊的記錄讀取器代理程式動作。|  
|發送訂閱的散發代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須：<br /><br /> -至少是散發資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> -為 PAL 的成員。<br /><br /> -擁有快照集共用的讀取權限。<br /><br /> -如果訂閱是針對非 SQL Server 訂閱者，訂閱者之 OLE DB 提供者的安裝目錄上，就要擁有讀取權限。<br /><br /> -在複寫 LOB 資料時，散發代理程式必須擁有複寫 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 的寫入權限，其中 XX 代表執行個體識別碼。<br /><br /> <br /><br /> 用於連接訂閱者的帳戶必須至少為訂閱資料庫中 **db_owner** 固定資料庫角色的成員，或者，如果訂閱為非 SQL Server 訂閱者的訂閱，則應擁有相等權限。<br /><br /> 注意:使用時`-subscriptionstreams >= 2`您也必須授與 「 散發代理程式上`View Server State`訂閱者的權限，以偵測死結。|  
|提取訂閱的散發代理程式|在連接到訂閱者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須至少是訂閱資料庫中 **db_owner** 固定資料庫角色的成員。 用於連接散發者的帳戶必須：<br /><br /> -為 PAL 的成員。<br /><br /> -擁有快照集共用的讀取權限。<br /><br /> -在複寫 LOB 資料時，散發代理程式必須擁有複寫 **C:\Program Files\Microsoft SQL Server\XX\COMfolder** 的寫入權限，其中 XX 代表執行個體識別碼。<br /><br /> <br /><br /> 注意:使用時`-subscriptionstreams >= 2`您也必須授與 「 散發代理程式上`View Server State`訂閱者的權限，以偵測死結。|  
|發送訂閱的合併代理程式|與發行者和散發者建立連接時，需使用代理程式執行時所用的 Windows 帳戶。 這個帳戶必須：<br /><br /> -至少是散發資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> -為 PAL 的成員。<br /><br /> -為與發行集資料庫中使用者相關聯的登入。<br /><br /> -擁有快照集共用的讀取權限。<br /><br /> <br /><br /> 用來連接訂閱者的帳戶必須至少是訂閱資料庫中 **db_owner** 固定資料庫角色的成員。|  
|提取訂閱的合併代理程式|在連接到訂閱者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須至少是訂閱資料庫中 **db_owner** 固定資料庫角色的成員。 用於連接發行者和散發者的帳戶必須：<br /><br /> -為 PAL 的成員。<br /><br /> -為與發行集資料庫中使用者相關聯的登入。<br /><br /> -為與散發資料庫中使用者相關聯的登入。 使用者可以是 `Guest` 使用者。<br /><br /> -擁有快照集共用的讀取權限。|  
|佇列讀取器代理程式|在連接到散發者時，需使用執行代理程式的 Windows 帳戶。 這個帳戶必須至少是散發資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> 用來連接發行者的帳戶必須至少是發行集資料庫中 **db_owner** 固定資料庫角色的成員。<br /><br /> 用來連接訂閱者的帳戶必須至少是訂閱資料庫中 **db_owner** 固定資料庫角色的成員。|  
  
## <a name="agent-security-under-sql-server-agent"></a>SQL Server Agent 下的代理程式安全性  
 利用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 程序或 RMO 設定複寫時，依預設，會為每個代理程式建立 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 作業。 然後，代理程式將在作業步驟內容下執行，無論是連續執行、按排程執行，或者在需要時執行。 您可以在 **中的** [作業] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾下檢視這些作業。 下表列出各個作業名稱。  
  
|Agent|作業名稱|  
|-----------|--------------|  
|快照集代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<整數>**|  
|合併式發行集分割區的快照集代理程式|**Dyn_\<發行者>-\<發行集資料庫>-\<發行集>-\<GUID>**|  
|記錄讀取器代理程式|**\<發行者>-\<發行集資料庫>-\<整數>**|  
|提取訂閱的合併代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<訂閱資料庫>-\<整數>**|  
|發送訂閱的合併代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>**|  
|發送訂閱的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>** <sup>1</sup>|  
|提取訂閱的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<訂閱資料庫>-\<GUID>** <sup>2</sup>|  
|發送訂閱至非 SQL Server 訂閱者的散發代理程式|**\<發行者>-\<發行集資料庫>-\<發行集>-\<訂閱者>-\<整數>**|  
|佇列讀取器代理程式|**[\<散發者>].\<整數>**|  
  
 <sup>1</sup>對於 Oracle 發行集的發送訂閱，作業名稱是**\<發行者 >-\<發行者**> 而非**\<發行者 >-\<發行集資料庫 >**。  
  
 <sup>2</sup>對於 Oracle 發行集的提取訂閱，作業名稱是**\<發行者 >-\<散發**> 而非**\<發行者 >-\<發行集資料庫 >**。  
  
 在複寫設定期間，指定代理程式應在其下執行的帳戶。 但是，所有作業步驟均在 *Proxy*安全性內容下執行，因此複寫將為您指定的代理程式帳戶在內部執行下列對應：  
  
-   先利用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql) 陳述式將帳戶對應至認證。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Proxy 使用認證來儲存 Windows 使用者帳戶的相關資訊。  
  
-   呼叫預存程序 [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) ，並利用認證建立 Proxy。  
  
> [!NOTE]  
>  提供此資訊的目的，是為了協助您了解，利用適當的安全性內容執行代理程式時會涉及哪些項目。 您不應該直接與已建立的認證或 Proxy 互動。  
  
## <a name="see-also"></a>另請參閱  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [SQL Server 複寫安全性](view-and-modify-replication-security-settings.md)   
 [保護快照集資料夾](secure-the-snapshot-folder.md)  
  
  
