---
title: 第 2 課：從另一部電腦連接 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
caps.latest.revision: 22
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0498eda438389648df868c34da088500a0e3710c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948383"
---
# <a name="lesson-2-connecting-from-another-computer"></a>第 2 課：從另一部電腦連接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
為了加強安全性，初始安裝時，您不能從另一部電腦存取 [!INCLUDE[ssDE](../includes/ssde-md.md)] Developer Edition、Express Edition 和 Evaluation Edition 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。 這一課教您如何啟用通訊協定、設定通訊埠以及設定 Windows 防火牆，以便從其他電腦連接。  
  
這一課包含下列工作：  
  
-   [啟用通訊協定](#protocols)  
  
-   [設定固定通訊埠](#port)  
  
-   [在防火牆中開啟通訊埠](#firewall)  
  
-   [從另一部電腦連接到 Database Engine](#otherComp)  
  
-   [使用 SQL Server Browser 服務來連接](#browser)  
  
## <a name="protocols"></a>啟用通訊協定  
為了加強安全性， [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]、Developer 和 Evaluation 的安裝只包含有限的網路連線功能。 同一部電腦上執行的工具可以建立 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的連接，但無法從其他電腦中建立。 如果您打算在 [!INCLUDE[ssDE](../includes/ssde-md.md)]所在的同一部電腦上進行開發工作，便不需要另外啟用其他通訊協定。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 將會使用 Shared Memory 通訊協定連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] 。 這個通訊協定已經啟用。  
  
如果您打算從其他電腦連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)] ，您必須啟用通訊協定，例如 TCP/IP。  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>如何從其他電腦啟用 TCP/IP 連接  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
    > [!NOTE]  
    > 您必須同時能夠使用 32 位元和 64 位元選項。  
  
    > [!NOTE]  
    > 由於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console 程式的嵌入式管理單元，而不是獨立的程式，因此 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。 檔案名稱中包含代表 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本號碼的數字。 若要從執行命令開啟組態管理員，以下是 Windows 安裝於 C 磁碟機時的最後四個版本路徑。  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
2.  在 [SQL Server 組態管理員] 中，展開 [SQL Server 網路組態]，然後按一下 [*<InstanceName>* 的通訊協定]。  
  
    預設執行個體 (未命名的執行個體) 是以 **MSSQLSERVER** 列出。 如果您安裝了具名執行個體，則會列出您所提供的名稱。 [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] 會安裝成 **SQLEXPRESS**，除非您在安裝期間變更其名稱。  
  
3.  在通訊協定清單中，以滑鼠右鍵按一下要啟用的通訊協定 ([TCP/IP])，然後按一下 [啟用]。  
  
    > [!NOTE]  
    > 變更網路通訊協定之後，您必須重新啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務。不過，此步驟會在下一項工作中完成。  
  
## <a name="port"></a>設定固定通訊埠  
為了加強安全性，Windows Server 2008、 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]和 Windows 7 都會開啟 Windows 防火牆。 若要從另一部電腦連接到這個執行個體，您必須在防火牆中開啟通訊埠。 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的預設執行個體會接聽通訊埠 1433，因此，您不需要設定固定通訊埠。 但是，包括 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 在內的具名執行個體則會接聽動態通訊埠。 在防火牆中開啟通訊埠之前，您必須先設定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 接聽特定的通訊埠 (稱為固定通訊埠或靜態通訊埠)，否則每次 [!INCLUDE[ssDE](../includes/ssde-md.md)] 啟動時可能會接聽不同的通訊埠。 如需防火牆、預設 Windows 防火牆設定的詳細資訊以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
> [!NOTE]  
> 通訊埠編號指派是由 Internet Assigned Numbers Authority 所管理，而且列於 [http://www.iana.org](http://go.microsoft.com/fwlink/?LinkId=48844)。您應該從 49152 到 65535 指派通訊埠編號。  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>設定 SQL Server 在特定通訊埠接聽  
  
1.  在 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員] 中，展開 [SQL Server 網路組態]，然後按一下您要設定的伺服器執行個體。  
  
2.  在右窗格中，按兩下 [TCP/IP]。  
  
3.  在 [TCP/IP 屬性] 對話方塊中，按一下 [IP 位址] 索引標籤。  
  
4.  在 [IPAll] 區段的 [TCP 通訊埠] 方塊中，輸入可用的通訊埠號碼。 在此教學課程中，我們將使用 **49172**。  
  
5.  按一下 [確定] 關閉對話方塊，再於提示您必須重新啟動服務的警告中按一下 [確定]。  
  
6.  在左窗格中，按一下 **[SQL Server 服務]**。  
  
7.  在右窗格中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，然後按一下 [重新啟動]。 當 [!INCLUDE[ssDE](../includes/ssde-md.md)] 重新啟動時，它將在通訊埠 **49172**上接聽。  
  
## <a name="firewall"></a>在防火牆中開啟通訊埠  
防火牆系統有助於預防未經授權存取電腦資源。 若要在防火牆開啟時從另一部電腦連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，您必須在防火牆中開啟通訊埠。  
  
> [!IMPORTANT]  
> 在防火牆中開啟通訊埠可能會讓您的伺服器面臨惡意攻擊的威脅。 在開啟通訊埠之前，請先確定您已經了解防火牆系統。 如需詳細資訊，請參閱＜ [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md)＞。  
  
在設定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 使用固定通訊埠之後，請遵循下列指示，在「Windows 防火牆」中開啟該通訊埠 (您不需要為預設執行個體設定固定通訊埠，因為它已經固定在 TCP 通訊埠 1433)。  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>若要在 Windows 防火牆中開啟通訊埠供 TCP 存取 (Windows 7)  
  
1.  在 **[開始]** 功能表上、按一下 **[執行]**，輸入 **WF.msc**，然後按一下 **[確定]**。  
  
2.  在 [具有進階安全性的 Windows 防火牆] 的左窗格中，以滑鼠右鍵按一下 [輸入規則]，再從動作窗格按一下 [新增規則]。  
  
3.  在 **[規則類型]** 對話方塊中，選取 **[通訊埠]**，然後按 **[下一步]**。  
  
4.  在 **[通訊協定及連接埠]** 對話方塊中，選取 **[TCP]**。 選取 [特定本機連接埠]，然後輸入 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體的通訊埠編號。 輸入 1433 表示預設執行個體。 如果您要設定具名執行個體，而且在上一項工作中已設定固定通訊埠，請輸入 **49172** 。 按 [下一步] 。  
  
5.  在 **[執行動作]** 對話方塊中，選取 **[允許連線]**，然後按 **[下一步]**。  
  
6.  在 **[設定檔]** 對話方塊中，選取您想要連線至 [!INCLUDE[ssDE](../includes/ssde-md.md)]時，描述電腦連線環境的設定檔，然後按 **[下一步]**。  
  
7.  在 **[名稱]** 對話方塊中，輸入此規則的名稱和描述，然後按一下 **[完成]**。  
  
如需防火牆設定 (包括 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]的指示) 的詳細資訊，請參閱 [設定用於 Database Engine 存取的 Windows 防火牆](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)。 如需預設 Windows 防火牆設定的詳細資訊以及影響 Database Engine、Analysis Services、Reporting Services 和 Integration Services 之 TCP 通訊埠的描述，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
## <a name="otherComp"></a>從另一部電腦連接到 Database Engine  
既然您已經設定 [!INCLUDE[ssDE](../includes/ssde-md.md)] 在固定通訊埠接聽，而且已在防火牆開啟該通訊埠，您就可以從另一部電腦連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服務在伺服器電腦上執行，而且防火牆已開啟 UDP 通訊埠 1434 時，可以使用電腦名稱和執行個體名稱來建立連接。 為了加強安全性，此範例不使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服務。  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>若要從另一部電腦連接到 Database Engine  
  
1.  在包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端工具的第二部電腦上，使用經授權連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的帳戶登入，並開啟 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
2.  在 [連接到伺服器] 對話方塊中，確認 [伺服器類型] 方塊中的 [Database Engine]。  
  
3.  在 [伺服器名稱] 方塊中，輸入 **tcp:** 以指定通訊協定，後面接著電腦名稱、逗號和通訊埠編號。 若要連線到預設執行個體，通訊埠 1433 為隱含 且可省略的通訊埠，因此只要鍵入 *tcp:***<電腦名稱> 即可。 在我們的具名執行個體範例中，請鍵入 **tcp:<電腦名稱>,49172**。  
  
    > [!NOTE]  
    > 如果 [伺服器名稱] 方塊中省略了 **tcp:**，用戶端將依照用戶端設定中指定的順序，嘗試所有啟用的通訊協定。  
  
4.  在 [驗證] 方塊中，確認 [Window 驗證]，然後按一下 [連接]。  
  
## <a name="browser"></a>使用 SQL Server Browser 服務來連接  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服務會接聽 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資源的內容要求，並提供有關電腦上所安裝之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的資訊。 當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 服務執行時，使用者可以提供電腦名稱和執行個體名稱 (而非電腦名稱和通訊埠編號) 來連接到具名執行個體。 因為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser 接收未驗證的 UDP 要求，所以在安裝期間不一定都開啟著。 如需服務的描述及其何時開啟的說明，請參閱 [SQL Server Browser 服務 &#40;Database Engine 和 SSAS&#41;](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)。  
  
若要使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser，您必須遵循與上述相同的步驟，並開啟防火牆中的 UDP 通訊埠 1434。  
  
以上總結這個簡短的基本連接教學課程。  
  
## <a name="return-to-tutorials-portal"></a>返回教學課程入口網站  
[教學課程：Database Engine 使用者入門](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

