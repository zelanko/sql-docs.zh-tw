---
title: SQL Server Browser 服務 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- services [SQL Server], security
- SQL Browser service (See SQL Server Browser Service)
- Browser Service
- SQL Server Browser service
ms.assetid: 3cc00d3a-487c-4cd9-a155-655f02485fa0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4e06fe371602956b6b43714038f41d8486cf2ae0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253635"
---
# <a name="sql-server-browser-service"></a>SQL Server Browser 服務
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser 程式會以 Windows 服務的方式執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會接聽 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的內送要求，並提供有關電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 完成下列動作：  
  
-   瀏覽可用伺服器的清單  
  
-   連接到正確的伺服器執行個體  
  
-   連接到專用管理員連接 (DAC) 端點  
  
 對於 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 與 [!INCLUDE[ssAS](../../includes/ssas-md.md)]的每個執行個體， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務 (sqlbrowser) 會提供執行個體名稱與版本號碼。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一起安裝。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務會在下列情況中自動啟動：  
  
-   升級安裝時。  
  
-   在叢集上安裝時。  
  
-   安裝 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的具名執行個體並包括 SQL Server Express 的所有執行個體時。  
  
-   安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的具名執行個體時。  
  
## <a name="background"></a>背景  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]之前，電腦上只可以安裝一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽通訊埠 1433 內送的要求，該通訊埠是由 Internet Assigned Numbers Authority (IANA) 官方指派給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的。 只有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體可以使用通訊埠，因此當 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 推出支援多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的功能時，發展了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) 來接聽 UDP 通訊埠 1434。 此接聽服務是以安裝的執行個體名稱，以及執行個體使用的通訊埠或具名管道來回應用戶端要求。 為了克服 SSRP 系統的限制， [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 引進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務來取代 SSRP。  
  
## <a name="how-sql-server-browser-works"></a>SQL Server Browser 如何運作  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體啟動時，如果已為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]啟用 TCP/IP 通訊協定，則會指派 TCP/IP 通訊埠給伺服器。 如果已啟用具名管道通訊協定，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會接聽特定的具名管道。 這個通訊埠或「管道」是由該特定執行個體使用，來與用戶端應用程式交換資料。 在安裝期間，TCP 通訊埠 1433 和管道 `\sql\query` 會指派給預設執行個體，但以後伺服器管理員可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來變更它們。 由於只有一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以使用通訊埠或管道，因此會指定不同的通訊埠編號和管道名稱給具名執行個體，包括 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 依預設，啟用之後，具名執行個體和 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 都設定為使用動態通訊埠，也就是說，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動時會指派可用的通訊埠。 如果需要，也可以將特定通訊埠指派給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 在連接時，用戶端可以指定特定的通訊埠，但如果該通訊埠是動態指定，則每當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動時，通訊埠編號可能變更，導致用戶端不知道正確的通訊埠編號。  
  
 在啟動時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會啟動並要求 UDP 通訊埠 1434。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會讀取登錄項目、識別電腦上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並記下它們使用的通訊埠與具名管道。 當伺服器擁有兩張或多張網路卡時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所遇到的第一個已啟用連接埠。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 支援 ipv6 和 ipv4。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源時，用戶端網路程式庫會使用通訊埠 1434 傳送 UDP 訊息到伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器回應要求之執行個體的 TCP/IP 通訊埠或具名管道。 於是，用戶端應用程式上的網路程式庫會使用所要的執行個體的通訊埠或具名管道，將要求傳送至伺服器來完成連接。  
  
 如需有關啟動與停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書。  
  
## <a name="using-sql-server-browser"></a>使用 SQL Server Browser  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務未執行，但您提供正確的通訊埠編號或具名管道，則仍然可以連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，您可以使用在通訊埠 1433 執行的 TCP/IP，來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。  
  
 不過，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務未執行，則下列連接沒有作用：  
  
-   任何嘗試連接到具名執行個體卻未完整指定所有參數 (例如 TCP/IP 通訊埠或具名管道) 的元件。  
  
-   任何產生或傳遞伺服器/執行個體資訊的元件，稍後要重新連接的其他元件可使用此資訊。  
  
-   連接到具名執行個體但未提供通訊埠編號或管道。  
  
-   具名執行個體或預設執行個體 (若未使用 TCP/IP 通訊埠 1433) 的 DAC。  
  
-   OLAP 重新導向程式服務。  
  
-   列舉 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、Enterprise Manager 或 Query Analyzer 中的伺服器。  
  
 如果您在主從式架構狀況中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (例如，當應用程式透過網路上存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時)，且如果您停止或停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務，則必須指派特定通訊埠編號給每一個執行個體，並將用戶端應用程式碼撰寫為永遠使用此通訊埠編號。 此方式有下列問題：  
  
-   您必須更新或維護用戶端應用程式碼，才能確保它是連接到正確的通訊埠。  
  
-   您為每個執行個體選取的通訊埠可能正由該伺服器上的其他服務或應用程式使用中，導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體無法使用。  
  
## <a name="clustering"></a>群集  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 不是群集資源，不支援一個叢集節點容錯移轉到另一個叢集節點。 因此，以群集的情況而言，應該要為群集的每一個節點安裝及開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser。 在群集上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會接聽 IP_ANY。  
  
> [!NOTE]  
>  接聽 IP_ANY 時，若您啟用的是接聽特定 IP，則使用者必須在每一個 IP 上設定相同的 TCP 通訊埠，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會傳回它發現的第一個 IP/通訊埠組合。  
  
## <a name="installing-uninstalling-and-running-from-the-command-line"></a>從命令列安裝、解除安裝和執行  
 依預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 程式會安裝在 C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe。  
  
 移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最後一個執行個體之後，就會解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 利用 **-c** 參數，可從命令提示字元啟動瀏覽器來進行疑難排解：  
  
```  
<drive>\<path>\sqlbrowser.exe -c  
```  
  
## <a name="security"></a>安全性  
  
### <a name="account-privileges"></a>帳戶權限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器會接聽 UDP 通訊埠，並接受使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) 的未驗證要求。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser，以降低遭受惡意攻擊的機會。 可利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來變更登入帳戶。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 所需的最低使用者權限如下：  
  
-   拒絕從網路存取這部電腦  
  
-   拒絕本機登入  
  
-   拒絕以批次作業登入  
  
-   拒絕透過終端機服務登入  
  
-   登入為服務  
  
-   讀寫與網路通訊 (通訊埠和管道) 有關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登錄機碼。  
  
### <a name="default-account"></a>預設帳戶  
 在安裝過程中，安裝程式會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 使用此帳戶來啟動服務。 其他可能的帳戶包括下列各項：  
  
-   任何 **網域\本機** 帳戶  
  
-   **[本機服務]** 帳戶  
  
-   **本機系統** 帳戶 (不建議使用，因為有不必要的權限)  
  
### <a name="hiding-sql-server"></a>隱藏 SQL Server  
 隱藏的執行個體是只支援共用記憶體連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請設定 `HideInstance` 旗標以指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 不應使用關於此伺服器執行個體的資訊來回應。  
  
### <a name="using-a-firewall"></a>使用防火牆  
 若要與位於防火牆後面之伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務進行通訊，除了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的 TCP 通訊埠 (例如 1433) 之外，請開啟 UDP 通訊埠 1434。 如需有關使用防火牆的資訊，請參閱 「 如何：設定防火牆供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]存取 」 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
## <a name="see-also"></a>另請參閱  
 [網路通訊協定和網路程式庫](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)  
  
  
