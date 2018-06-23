---
title: 安裝 Distributed 的 Replay （安裝程式） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64479cdc-661a-4e32-a381-8f8b5a238337
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ea29de67ee3e94089c63d5310e38a050be614ce3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145294"
---
# <a name="install-distributed-replay-setup"></a>安裝 Distributed Replay (安裝程式)
  您可以使用 [ [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈] 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Distributed Replay 功能。 規劃要安裝這些功能的位置時，請考慮下列事項：  
  
-   您可以選擇將管理工具與 Distributed Replay Controller 安裝在同一部電腦上，也可以選擇安裝在不同的電腦上。  
  
-   每個 Distributed Replay 環境只可有一個控制器。  
  
-   您最多可以在 16 部 (實體或虛擬) 電腦上安裝 Client 服務。  
  
-   Distributed Replay Controller 電腦上只可安裝一個用戶端服務執行個體。 您的 Distributed Replay 環境中如有多個用戶端，即不建議您將用戶端服務與控制器安裝在同一部電腦上。 這樣做可能會降低 Distributed Replay 的整體速度。  
  
-   在效能測試案例中，我們不建議您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的目標執行個體上安裝管理工具、Distributed Replay Controller 服務或 Client 服務。 在目標伺服器上安裝這些所有功能應限於應用程式相容性的功能測試。  
  
-   安裝之後，必須先執行控制器服務 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller)，然後再啟動用戶端上的 Distributed Replay Client 服務。  
  
> [!NOTE]  
>  如果要移除或變更 Distributed Replay 功能，請使用 Windows [控制台] 中的 [程式和功能] 視窗。 在 [解除安裝或變更程式] 視窗中，選取 [[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]]，然後按一下 [移除] 開啟 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈。 在 [選取功能] 頁面上，核取您想要移除的 Distributed Replay 功能。  
  
 **必要條件：**  
  
-   請確定您想要使用的電腦符合 [Distributed Replay 需求](../../tools/sql-server-profiler/replay-requirements.md)主題中所描述的需求。  
  
-   開始進行此程序之前，請建立將用來執行 Controller 和 Client 服務的網域使用者帳戶。 建議您不要將這些帳戶設定為 Windows Administrators 群組的成員。 如需詳細資訊，請參閱 [Distributed Replay 安全性](../../tools/distributed-replay/distributed-replay-security.md) 主題中的＜使用者和服務帳戶＞一節。  
  
    > [!NOTE]  
    >  如果您要在同一部電腦上執行管理工具、Controller 服務和 Client 服務，可以使用本機使用者帳戶。  
  
 **安裝位置：**  
  
 假設您使用預設檔案位置和標準安裝，則基底目錄便位於 C:\Program Files\Microsoft SQL Server。 在該目錄中，二進位編碼檔案與組件的安裝位置如下：  
  
-   在 32 位元系統上：  
  
     [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]工具  
  
     \- 或 -  
  
     \<共用功能目錄>\Tools\\(使用者提供的替代共用功能目錄)  
  
-   在 64 位元系統上：  
  
     C:\Program Files\\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (x86) \120\Tools  
  
     \- 或 -  
  
     \<共用功能目錄 (x86)>\Tools\\(使用者提供的替代共用功能 (x86) 目錄)  
  
### <a name="to-install-distributed-replay-features"></a>安裝 Distributed Replay 功能  
  
1.  如果要開始安裝 Distributed Replay 功能，請啟動 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈。  
  
2.  [安裝程式支援規則] 頁面會識別安裝 SQL Server 安裝程式支援檔案時可能會發生的問題。 您必須先更正任何安裝程式支援失敗，然後再繼續進行安裝。  
  
3.  在 **[產品金鑰]** 頁面上，選取選項按鈕，指出您要安裝免費的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本，或具有 PID 金鑰之產品的實際執行版本。 如需詳細資訊，請參閱[版本和 SQL Server 2014 元件](../editions-and-components-of-sql-server-2016.md)。  
  
4.  在 **[授權條款]** 頁面上，閱讀授權條款，然後選取要接受授權條款和條件的核取方塊。 若要協助提升 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您也可以啟用功能使用方式選項，並傳送報告給 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。  
  
5.  在 [安裝程式支援檔案] 頁面上，按一下 [安裝]，即可安裝或更新 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的安裝程式支援檔案。  
  
6.  在 [安裝程式角色] 頁面上，選取 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能安裝]，然後按一下 [下一步] 繼續前往 [特徵選取] 頁面。  
  
7.  在 [特徵選取] 頁面上，設定您想要安裝的功能。  
  
    -   若要安裝管理工具，請選取 [管理工具 - 基本]。  
  
    -   如果要安裝控制器服務，請選取 [Distributed Replay Controller]。  
  
    -   如果要安裝用戶端服務，請選取 [Distributed Replay Client]。  
  
     **重要事項**：當您設定 Distributed Replay Controller 時，可以指定將用來執行 Distributed Replay Client 服務的一個或多個使用者帳戶。 下列是支援帳戶的清單：  
  
    -   網域使用者帳戶  
  
    -   使用者建立的本機使用者帳戶  
  
    -   系統管理員  
  
    -   虛擬帳戶和 MSA (受管理的服務帳戶)  
  
    -   網路服務、本機系統和系統  
  
     不接受群組帳戶 (本機或網域) 和其他內建帳戶 (例如 Everyone)。  
  
8.  (選擇性) 按一下省略符號 (…) 按鈕，即可變更共用功能目錄路徑。  
  
    1.  在 32 位元電腦上，預設安裝路徑為 **C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
    2.  在 64 位元電腦上，預設安裝路徑為 **C:\Program Files (x86)\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\**  
  
9. 完成後，請按一下 [下一步]。  
  
10. 在 [安裝規則] 頁面上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會驗證您的電腦組態。 當驗證程序完成之後，請按一下 [下一步]。  
  
11. **[磁碟空間需求]** 頁面會計算您所指定之功能的所需磁碟空間。 然後，它會比較所需的空間與可用的磁碟空間。  
  
12. 在 [錯誤報告] 頁面上，指定您想要傳送給 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的資訊，以便協助改善 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 錯誤報告選項預設為啟用。  
  
13. 系統組態檢查會在 [安裝組態規則] 頁面上另外執行一組規則，藉此向您所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能驗證電腦組態。  
  
14. 在 [已完成安裝程式的準備工作] 頁面上，按一下 [安裝]。  
  
    > [!IMPORTANT]  
    >  安裝 Distributed Replay 之後，您必須在控制器電腦與用戶端電腦上建立防火牆規則，並為目標伺服器上的每個用戶端電腦授與權限。 如需詳細資訊，請參閱 [完成安裝後步驟](../../tools/distributed-replay/complete-the-post-installation-steps.md)。  
  
 下列其他主題詳述了 Distributed Replay 的其他安裝方式：  
  
-   [從命令提示字元安裝 Distributed 的 Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
-   [使用組態檔安裝 Distributed 的 Replay](../../../2014/sql-server/install/install-distributed-replay-using-a-configuration-file.md)  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 您必須具備管理權限，才可安裝各種 Distributed Replay 功能。 只有擁有系統管理員權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入能夠將用戶端服務帳戶加入測試伺服器的系統管理員伺服器角色。 如需 Distributed Replay 安全性考量的詳細資訊，請參閱 [Distributed Replay 安全性](../../tools/distributed-replay/distributed-replay-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Distributed 的 Replay 需求](../../tools/sql-server-profiler/replay-requirements.md)   
 [管理工具命令列選項 &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)   
 [設定 Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  