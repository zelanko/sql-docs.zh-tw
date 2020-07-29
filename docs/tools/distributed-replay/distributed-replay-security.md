---
title: Distributed Replay 安全性
titleSuffix: SQL Server Distributed Replay
description: 此文章說明 SQL Server Distributed Replay 的安全性設定步驟，以及資料保護與移除步驟的重要考量。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 7e2e586d-947d-4fe2-86c5-f06200ebf139
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 944fc1a9b5769c797ed9fa372e45c17931814983
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85681545"
---
# <a name="distributed-replay-security"></a>Distributed Replay 安全性

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在安裝和使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 功能之前，您應該先檢閱本主題中的重要安全性資訊。 本主題描述的是使用 Distributed Replay 之前必須進行的安裝後安全性設定步驟。 本主題亦描述與資料保護和重要移除步驟有關的重要考量。  
  
## <a name="user-and-service-accounts"></a>使用者和服務帳戶  
 下表描述用於 Distributed Replay 的帳戶。 安裝 Distributed Replay 之後，您必須指派用以執行 Controller 和 Client 服務帳戶的安全性主體。 因此，我們建議您在安裝 Distributed Replay 功能之前設定對應的網域使用者帳戶。  
  
|使用者帳戶|需求|  
|------------------|------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 服務帳戶|可以是網域使用者帳戶或本機使用者帳戶。 如果您使用本機使用者帳戶，管理工具、Controller 和 Client 都必須在同一部電腦上執行。<br /><br /> **\*\* 安全性注意事項 \*\*** 我們建議您不要將此帳戶設定為 Windows 本機 Administrators 群組的成員。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務帳戶|可以是網域使用者帳戶或本機使用者帳戶。 如果您使用本機使用者帳戶，Controller、Client 和目標 SQL Server 都必須在同一部電腦上執行。<br /><br /> **\*\* 安全性注意事項 \*\*** 我們建議您不要將此帳戶設定為 Windows 本機 Administrators 群組的成員。|  
|用來執行 Distributed Replay 管理工具的互動式使用者帳戶|可以是本機使用者或網域使用者帳戶。 若要使用本機使用者帳戶，管理工具和控制器必須在同一部電腦上執行。|  
  
 **重要**：當您設定 Distributed Replay Controller 時，可以指定將用來執行 Distributed Replay Client 服務的一或多個使用者帳戶。 下列是支援帳戶的清單：  
  
-   網域使用者帳戶  
  
-   使用者建立的本機使用者帳戶  
  
-   系統管理員  
  
-   虛擬帳戶和 MSA (受管理的服務帳戶)  
  
-   網路服務、本機系統和系統  
  
 不接受群組帳戶 (本機或網域) 和其他內建帳戶 (例如 Everyone)。  
  
 若要在安裝 Distributed Replay 之後設定服務帳戶或其密碼，您可以使用 Windows 服務工具。 若要變更與 Distributed Replay Controller 或 Client 服務相關聯的服務帳戶，請遵循下列步驟進行：  
  
1.  請根據作業系統執行下列其中一項作業：  
  
    -   按一下 [開始]、在 [搜尋] 方塊中輸入 **services.msc**，然後按下 ENTER。  
  
    -   按一下 [開始]、按一下 [執行]、輸入 **services.msc**，然後按下 ENTER。  
  
2.  在 [服務] 對話方塊中，以滑鼠右鍵按一下您想要設定的服務，然後按一下 [內容]。  
  
3.  在 [登入] 索引標籤上，按一下 [This account (這個帳戶)]。  
  
4.  設定您想要使用的使用者帳戶。  
  
## <a name="file-and-folder-permissions"></a>檔案和資料夾權限  
 指定了服務帳戶之後，您必須將必要的檔案和資料夾權限授與這些服務帳戶。 請根據下表設定檔案和資料夾權限：  
  
|帳戶|資料夾權限|  
|-------------|------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 服務帳戶|`<Controller_Installation_Path>\DReplayController` (讀取、寫入、刪除)<br /><br /> `DReplayServer.xml` 檔案 (讀取、寫入)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務帳戶|`<Client_Installation_Path>\DReplayClient` (讀取、寫入、刪除)<br /><br /> `DReplayClient.xml` 檔案 (讀取、寫入)<br /><br /> 工作和結果目錄，分別由 `WorkingDirectory` 和 `ResultDirectory` 元素指定於 Client 組態檔中 (讀取、寫入)。|  
  
## <a name="dcom-permissions"></a>DCOM 權限  
 DCOM 是用於 Controller 與管理工具以及 Controller 與所有 Client 之間的遠端程序呼叫 (RPC) 通訊。 安裝了 Distributed Replay 功能之後，您必須在 Controller 上設定整部電腦和應用程式特定的 DCOM 權限。  
  
 若要設定 Controller DCOM 權限，請遵循下列步驟進行：  
  
1.  **開啟 dcomcnfg.exe，[元件服務] 嵌入式管理單元**：此為用來設定 DCOM 權限的工具。  
  
    1.  在 Controller 電腦上，按一下 [開始]。  
  
    2.  在 [搜尋] 方塊中，輸入 **dcomcnfg.exe**。  
  
    3.  按 ENTER 鍵。  
  
2.  **設定整部電腦的 DCOM 權限**：針對下表所列的每個帳戶授與對應的整部電腦 DCOM 權限。 如需如何設定整部電腦權限的詳細資訊，請參閱 [檢查清單：管理 DCOM 應用程式](https://go.microsoft.com/fwlink/?LinkId=185842)。  
  
3.  **設定應用程式限定的 DCOM 權限**：針對下表所列的每個帳戶授與對應的應用程式限定的 DCOM 權限。 控制器服務的 DCOM 應用程式名稱是 **DReplayController**。 如需如何設定應用程式特定權限的詳細資訊，請參閱 [檢查清單：管理 DCOM 應用程式](https://go.microsoft.com/fwlink/?LinkId=185842)。  
  
 下表描述哪些 DCOM 權限是管理工具互動式使用者帳戶和 Client 服務帳戶所需的權限：  
  
|功能|帳戶|Controller 的必要 DCOM 權限|  
|-------------|-------------|---------------------------------------------|  
|Distributed Replay 管理工具|互動式使用者帳戶|本機存取<br /><br /> 遠端存取<br /><br /> 本機啟動<br /><br /> 遠端啟動<br /><br /> 本機啟用<br /><br /> 遠端啟用|  
|Distributed Replay Client|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務帳戶|本機存取<br /><br /> 遠端存取<br /><br /> 本機啟動<br /><br /> 遠端啟動<br /><br /> 本機啟用<br /><br /> 遠端啟用|  
  
> [!IMPORTANT]  
>  為了有效抵禦惡意查詢或阻斷服務攻擊，請務必只將信任的使用者帳戶用於 Client 服務帳戶。 此帳戶將能夠針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目標執行個體連接並重新執行工作負載。  
  
## <a name="sql-server-permissions"></a>SQL Server 權限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務帳戶是用來連接到工作負載的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目標執行個體。 這些連接僅支援 Windows 驗證模式。  
  
 當您在一組電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 服務之後，用於這些服務帳戶的安全性主體必須被授與您要重新執行追蹤工作負載之目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的系統管理員伺服器角色。 在 Distributed Replay 安裝期間，不會自動執行此步驟。  
  
## <a name="data-protection"></a>資料保護  
 在 Distributed Replay 環境中，下列使用者帳戶會被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之目標伺服器執行個體、輸入追蹤資料和結果追蹤檔案的完整存取權：  
  
-   用來執行管理工具的互動式使用者帳戶。  
  
-   Controller 服務帳戶。  
  
-   Client 服務帳戶。  
  
-   Controller 上本機 Administrators 群組的成員。  
  
-   Client 上本機 Administrators 群組的成員。  
  
    > [!IMPORTANT]  
    >  這些帳戶對於 Distributed Replay 所使用之追蹤、中繼、分派或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔案中包含的任何個人識別資訊 (PII) 或機密資訊擁有完整存取權。  
  
 我們建議您採取下列安全性預防措施：  
  
-   將輸入追蹤資料、輸出追蹤結果和資料庫檔案儲存在使用 NTFS 檔案系統 (NTFS) 的位置，並且套用適當的存取控制清單 (ACL)。 必要時，請加密儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上的資料。 請注意，ACL 不會套用至追蹤檔案，因此沒有任何資料遮罩或模糊化。 您應該在使用後盡快刪除這些檔案。  
  
-   將適當的 ACL 和保留原則套用至 Distributed Replay 所產生的所有中繼和分派檔案。  
  
-   使用「傳輸層安全性」(TLS) (先前稱為「安全通訊端層」(SSL)) 來協助保護網路傳輸。  
  
## <a name="important-removal-steps"></a>重要移除步驟  
 我們建議您僅在測試環境中使用 Distributed Replay。 在您完成測試之後，針對不同的工作佈建這些電腦之前，請務必執行下列作業：  
  
-   解除安裝 Distributed Replay 功能並且從 Controller 和所有 Client 中移除相關的組態檔。  
  
-   刪除用於測試的任何追蹤、中繼、分派和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫檔案。 中繼和分派檔案會分別儲存在 Controller 和 Client 的工作目錄中。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [安裝 Distributed Replay - 概觀](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
  
