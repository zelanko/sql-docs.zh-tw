---
title: 設定多重主目錄電腦進行 SQL Server 存取 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multi-homed computer
- multi-homed computer [SQL Server] configuring ports
- firewall systems [Database Engine], multi-homed computer
ms.assetid: ba369e5b-7d1f-4544-b7f1-9b098a1e75bc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3e20ed69a9fdff95914dd0d5086e3c0774421d44
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47599946"
---
# <a name="configure-a-multi-homed-computer-for-sql-server-access"></a>設定多重主目錄電腦進行 SQL Server 存取
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  當伺服器必須提供兩個或多個網路或子網路的連接時，一般會使用多重主目錄電腦。 這部電腦通常位於周邊網路 (也稱為 DMZ 或篩選的子網路) 中。 本文描述如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和具有進階安全性的 Windows 防火牆，以便在多重主目錄環境中提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路連線。  
  
> [!NOTE]  
>  多重主目錄電腦具有多張網路介面卡，或者已經設定成針對單一網路介面卡使用多個 IP 位址。 雙重主目錄電腦具有兩張網路介面卡，或者已經設定成針對單一網路介面卡使用兩個 IP 位址。  
  
 繼續本文之前，您應該先熟悉[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)一文中提供的資訊。 本文包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件如何使用防火牆的基本資訊。  
  
 **這個範例假設：**  
  
-   電腦中安裝了兩張網路介面卡。 其中一或多張網路介面卡可能是無線的。 您可以使用某張網路介面卡的 IP 位址，然後使用回送 IP 位址 (127.0.0.1) 當做第二張網路介面卡，藉以模擬擁有兩張網路介面卡。  
  
-   為了簡化，這個範例會使用 IPv4 位址。 您可以使用 IPv6 位址來執行相同的程序。  
  
    > [!NOTE]  
    >  IPv4 位址是一連串稱為八位元資料組的四個數字。 每個數字都小於 255，並以句號隔開，例如 127.0.0.1。 IPv6 位址是一連串八個十六進位數字 (以冒號隔開)，例如 fe80:4898:23:3:49a6:f5c1:2452:b994。  
  
-   防火牆規則可能會允許透過特定通訊埠存取，例如通訊埠 1433。 或者，防火牆規則可能會允許存取 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 程式 (sqlservr.exe)。 這兩種方法各有優點。 由於周邊網路的伺服器比內部網路的伺服器更容易遭受攻擊，因此本文假設您想要擁有更精確的控制權，並分別選取您所開啟的通訊埠。 基於上述原因，本文假設您要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接聽固定通訊埠。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所用連接埠的詳細資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
-   這則範例會使用 TCP 通訊埠 1433 來設定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的存取權。 您可以使用相同的一般步驟來設定不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件所使用的其他通訊埠。  
  
 **這則範例中的一般步驟如下所示：**  
  
-   判斷電腦的 IP 位址。  
  
-   將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為接聽特定的 TCP 通訊埠。  
  
-   設定具有進階安全性的 Windows 防火牆。  
  
## <a name="optional-procedures"></a>選擇性程序  
 如果您已經知道電腦可用的 IP 位址，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的 IP 位址，就可以略過下列程序。  
  
#### <a name="to-determine-the-ip-addresses-available-on-the-computer"></a>若要判斷電腦可用的 IP 位址  
  
1.  在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上，依序按一下 [開始] 和 [執行]、輸入 **cmd**，然後 [!INCLUDE[clickOK](../../includes/clickok-md.md)]。  
  
2.  在 [命令提示字元] 視窗中，輸入 **ipconfig**，然後按下 ENTER，即可列出這部電腦可用的 IP 位址。  
  
    > [!NOTE]  
    >  **ipconfig** 命令有時會列出許多可能的連結，包含已中斷連線的連結。 **ipconfig** 命令可以同時列出 IPv4 及 IPv6 的位址。  
  
3.  請記下所使用的 IPv4 位址和 IPv6 位址。 清單中的其他資訊 (例如暫時位址、子網路遮罩和預設閘道器) 都是設定 TCP/IP 網路的重要資訊。 不過，這則範例不會使用這項資訊。  
  
#### <a name="to-determine-the-ip-addresses-and-ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>判斷使用的 IP 位址和連接埠 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  按一下 [開始] 並依序指向 [所有程式]、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 [組態工具]，然後按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員]。  
  
2.  在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員] 的主控台窗格中，展開 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路組態]，再展開 [\<執行個體名稱> 的通訊協定]，然後按兩下 [TCP/IP]。  
  
3.  在 [TCP/IP 內容] 對話方塊的 [IP 位址] 索引標籤上會出現數個 IP 位址，這些 IP 位址的格式是 **IP1**、**IP2** 到 **IPAll**。 其中一個是供回送介面卡的 IP 位址 127.0.0.1 使用。 此時會出現額外的 IP 位址，代表電腦上設定的每個 IP 位址。  
  
4.  對於任何 IP 位址而言，如果 [TCP 動態通訊埠] 對話方塊包含 **0**，這就表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在接聽動態連接埠。 這則範例會使用固定通訊埠來取代可能會在重新啟動時變更的動態通訊埠。 因此，如果 [TCP 動態通訊埠] 對話方塊包含 **0**，請刪除 0。  
  
5.  請記下針對您想要設定之每個 IP 位址所列出的 TCP 通訊埠。 在這則範例中，請假設兩個 IP 位址都在接聽預設通訊埠 1433。  
  
6.  如果您不想要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用某些可用的連接埠，請在 [通訊協定] 索引標籤中，將 [全部接聽] 值變更為 [否]。然後，在 [IP 位址] 索引標籤中，針對您不想要使用的 IP 位址，將 [使用中] 值變更為 [否]。  
  
## <a name="configuring-windows-firewall-with-advanced-security"></a>設定具有進階安全性的 Windows 防火牆  
 在您知道電腦所使用的 IP 位址以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的通訊埠之後，就可以建立防火牆規則，然後針對特定的 IP 位址設定這些規則。  
  
#### <a name="to-create-a-firewall-rule"></a>若要建立防火牆規則  
  
1.  在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦上，以管理員身分登入。  
  
2.  依序按一下 [開始] 和 [執行]、輸入 **wf.msc**，然後按一下 [確定]。  
  
3.  在 [使用者帳戶控制] 對話方塊中，按一下 [繼續]，即可使用管理員認證來開啟 [具有進階安全性的 Windows 防火牆] 嵌入式管理單元。  
  
4.  在 [概觀] 頁面上，確認 Windows 防火牆已啟用。  
  
5.  在左窗格中，按一下 [輸入規則]。  
  
6.  以滑鼠右鍵按一下 [輸入規則]，然後按一下 [新增規則] 以開啟 [新增輸入規則精靈]。  
  
7.  您可以針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式建立規則。 不過，因為這則範例使用固定通訊埠，所以請選取 [連接埠]，然後按 [下一步]。  
  
8.  在 [通訊協定及連接埠] 頁面上，選取 [TCP]。  
  
9. 選取 [特定本機連接埠]。 輸入以逗號隔開的通訊埠編號，然後按 [下一步]。 在這則範例中，您將設定預設通訊埠。因此，請輸入 **1433**。  
  
10. 在 [動作] 頁面上，檢閱這些選項。 在這則範例中，您不會使用防火牆來強制執行安全連接。 因此，請按一下 [允許該連線]，然後按 [下一步]。  
  
    > [!NOTE]  
    >  您的環境可能需要使用安全連接。 如果您選取其中一個安全連接選項，可能必須設定憑證和 [強制加密] 選項。 如需安全連線的詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md) 和[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
11. 在 [設定檔] 頁面上，針對此規則選取一個或多個設定檔。 如果您不熟悉防火牆設定檔，請按一下防火牆程式中的 [深入了解設定檔] 連結。  
  
    -   如果此電腦是伺服器，而且只有在連接至網域時才能使用，請選取 [網域]，然後按 [下一步]。  
  
    -   如果此電腦是行動式電腦 (例如，筆記型電腦)，當它連接至不同的網路時，可能會使用多個設定檔。 若為行動式電腦，您可以針對不同的設定檔設定不同的存取功能。 例如，您可能會在電腦使用網域設定檔時允許存取，但在它使用公用設定檔時拒絕存取。  
  
12. 在 [名稱] 頁面上，針對此規則提供名稱和描述，然後按一下 [完成]。  
  
13. 重複這項程序，以便針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 即將使用的每個 IP 位址建立其他規則。  
  
 在您已經建立一項或多項規則之後，請執行下列步驟，將電腦上的每個 IP 位址都設定成使用規則。  
  
#### <a name="to-configure-the-firewall-rule-for-a-specific-ip-addresses"></a>若要針對特定的 IP 位址設定防火牆規則  
  
1.  在 [具有進階安全性的 Windows 防火牆] 的 [輸入規則] 頁面上，以滑鼠右鍵按一下您剛建立的規則，然後按一下 [內容]。  
  
2.  在 [規則內容] 對話方塊中，選取 [範圍] 索引標籤。  
  
3.  在 [本機 IP 位址] 區域中，選取 [這些 IP 位址]，然後按一下 [新增]。  
  
4.  在 [IP 位址] 對話方塊中，選取 [此 IP 位址或子網路]，然後輸入您想要設定的其中一個 IP 位址。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  在 [遠端 IP 位址] 區域中，選取 [這些 IP 位址]，然後按一下 [新增]。  
  
7.  您可以使用 [IP 位址] 對話方塊，針對電腦上選取的 IP 位址設定連接性。 您可以啟用來自指定之 IP 位址、IP 位址範圍、整個子網路或特定電腦的連接。 若要正確設定這個選項，您必須充分了解網路。 如需有關網路的詳細資訊，請洽詢網路管理員。  
  
8.  若要關閉 [IP 位址] 對話方塊，請按一下 [確定]。然後，按一下 [確定] 關閉 [規則內容] 對話方塊。  
  
9. 若要在多重主目錄電腦上設定其他 IP 位址，請使用其他 IP 位址和其他規則來重複這項程序。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Browser 服務 &#40;Database Engine 和 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [經由 Proxy 伺服器連接至 SQL Server &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager.md)  
  
  
