---
title: "針對 Web 同步處理設定 IIS 7 | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IIS 7 server configuration [SQL Server replication]
- Web synchronization, IIS 7 servers
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: ecc4752f5bf52931df9c7af62b5828b92f8f0123
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="configure-iis-7-for-web-synchronization"></a>針對 Web 同步處理設定 IIS 7
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  本主題中的程序將逐步引導您完成手動設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 7 及更新版本的程序，以搭配使用 Web 同步處理，並進行合併式複寫。 
  
 啟用 Web 同步處理需要三個步驟，第一個步驟是設定 IIS 7 或更新版本。  
  
 如需完整組態處理序的概觀，請參閱[設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)。  
  
> [!IMPORTANT]  
>  確定您的應用程式只使用 [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] 或更新版本，而且 IIS 伺服器上未安裝較早版本的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。 舊版 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 可能會導致錯誤，例如：「Web 同步處理期間，訊息的格式無效。 請確認已在 Web 伺服器正確地設定複寫元件」。  
  
 若要使用 Web 同步處理，您必須完成下列步驟來設定 IIS。 本主題中有每個步驟的詳細描述。  
  
1.  在執行 IIS 的電腦上安裝並設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener。  
  
2.  設定安全通訊端層 (SSL)。 IIS 與所有訂閱者之間的通訊都需要 SSL。  
  
3.  設定 IIS 驗證。  
  
4.  設定帳戶並設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener 的權限。  
  
## <a name="installing-the-sql-server-replication-listener"></a>安裝 SQL Server Replication Listener  

IIS 5.0 版開始支援 Web 同步處理。 IIS 7.0 版或更新版本不提供 IIS 5 和 IIS 6 版的 [設定 Web 同步處理精靈]。 **從 SQL Server 2012 開始，若要在 IIS 伺服器上使用 Web 同步處理元件，您應該安裝具有複寫功能的 SQL Server。例如，免費的 SQL Server Express Edition。**
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>若要安裝和設定 SQL Server Replication Listener  
  
1.  在 IIS 電腦上安裝 SQL Server 複寫。

2. 在執行 IIS 的電腦上，針對 replisapi.dll 建立新的檔案目錄。 您可以在任何位置建立該目錄，不過，建議您在 \<*磁碟機*>:\Inetpub 目錄底下建立該目錄。 例如，您可以建立 \<*磁碟機*>:\Inetpub\SQLReplication\\ 目錄。  
  
3.  將 replisapi.dll 從目錄 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ 複製到步驟 1 中建立的檔案目錄。  
  
4.  註冊 replisapi.dll：  
  
    1.  按一下 **[開始]**，然後按一下 **[執行]**。 在 [開啟]  方塊中，輸入 **cmd**，然後按一下 [確定] 。  
  
    2.  在步驟 1 中建立的目錄中，執行下列命令：  
  
         **regsvr32 replisapi.dll**  
  
5.  為複寫建立新網站，或使用現有的網站。 這個網站將在同步處理期間由複寫元件存取。 本主題中的程序將採用預設的網站。 如需有關如何建立網站的詳細資訊，請參閱 IIS 文件集。  
  
6.  在 IIS 中建立虛擬目錄。 虛擬目錄應該在步驟 4 所建立的網站之下建立，而且應該對應至步驟 1 所建立的目錄。 在指派此目錄的權限時愈嚴格愈好。 您至少必須選取 **[讀取]** 和 **[執行]** 權限。  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**的 **[連線]** 窗格中，以滑鼠右鍵按一下 **[預設的網站]**，然後選取 **[新增虛擬目錄]**。  
  
    2.  針對 [別名] ，輸入 **SQLReplication**。  
  
    3.  針對 [實體路徑]，輸入 **\<磁碟機>:\Inetpub\SQLReplication\\**，然後按一下 [確定]。  
  
7.  設定 IIS，使 replisapi.dll 能夠執行。  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**中，按一下 **[預設的網站]**。  
  
    2.  在中央窗格中，按一下 **[處理常式對應]**。  
  
    3.  在 **[動作]** 窗格中，按一下 **[新增模組對應]**。  
  
    4.  針對 [要求路徑]  ，輸入 **replisapi.dll**。  
  
    5.  從 **[模組]** 下拉式清單中選取 **[IsapiModule]**。  
  
    6.  針對 [可執行檔]，輸入 **\<磁碟機>:\Inetpub\SQLReplication\replisapi.dll**。  
  
    7.  針對 [名稱] ，輸入 **Replisapi**。  
  
    8.  按一下 **[要求限制]** 按鈕、按一下 **[存取]** 索引標籤，然後按一下 **[執行]**。  
  
    9. 按一下 **[確定]** 關閉 **[要求限制]** 對話方塊，然後再次按一下 **[確定]** 關閉 **[新增模組對應]** 對話方塊。 當系統提示您允許 ISAPI 延伸模組時，請按一下 **[是]** 加入此延伸模組。  
  
    10. 確認 Replisapi.dll 是否列於 **[已啟用]** 處理常式對應底下。 如果它位於 **[已停用]** 清單中，請以滑鼠右鍵按一下 Replisapi 項目，然後按一下 **[編輯功能權限]**。 核取 **[執行]** 方塊，然後按一下 **[確定]**。  
  
## <a name="configuring-iis-authentication"></a>設定 IIS 驗證  
 當訂閱者電腦連接到 IIS 時，訂閱者必須經過 IIS 驗證才能存取資源和處理序。 驗證可套用至整個網站或您建立的虛擬目錄。  
  
 我們建議您搭配 SSL 使用基本驗證。 不論採用哪一種驗證類型，都需要 SSL。  
  
 我們建議您搭配 SSL 使用基本驗證。 不論採用哪一種驗證類型，都需要 SSL。  
  
#### <a name="to-configure-iis-authentication"></a>若要設定 IIS 驗證  
  
1.  在 **[Internet Information Services (IIS) 管理員]**中，按一下 **[預設的網站]**。  
  
2.  在中間窗格中，按兩下 **[驗證]**。  
  
3.  以滑鼠右鍵按一下 [匿名驗證]，然後選擇 [停用]。  
  
4.  以滑鼠右鍵按一下 [基本驗證]，然後選擇 [啟用]。  
  
## <a name="configuring-secure-sockets-layer"></a>設定安全通訊端層  
 若要設定 SSL，請指定要由執行 IIS 之電腦使用的憑證。 合併式複寫的 Web 同步處理支援使用伺服器憑證，但不支援用戶端憑證。 若要設定 IIS 以進行部署，必須先從憑證授權中心 (CA) 獲得憑證。 如需有關憑證的詳細資訊，請參閱 IIS 文件集。  
  
 在您安裝憑證之後，必須將憑證與 Web 同步處理所使用的網站相關聯。 如果是為了開發和測試，您可以指定自我簽署憑證。 IIS 7 可以為您建立憑證並在電腦上註冊此憑證。  
  
 針對實際執行部署與此處所提供程序之間的差異在於，進行實際執行和實際執行前測試時，您會使用 CA 所核發的憑證而非自我簽署憑證。  
  
> [!IMPORTANT]  
>  若為實際執行安裝，則不建議使用自我簽署憑證。 自我簽署憑證並不安全。 如果只是為了開發和測試，請使用自我簽署憑證。  
  
 若要設定 SSL，您將執行下列步驟：  
  
1.  將網站設定為要求 SSL 並忽略用戶端憑證。  
  
2.  從 CA 取得憑證，或建立自我簽署憑證。  
  
3.  將憑證繫結至複寫網站。  
  
#### <a name="to-require-ssl-security-for-a-web-site"></a>若要要求網站的 SSL 安全性  
  
1.  在 **[Internet Information Services (IIS) 管理員]**中，展開本機伺服器節點，然後按一下 **[預設的網站]** (或是您的 Web 同步處理網站，如果它與預設的網站不同的話)。  
  
2.  在中間窗格中，按兩下 **[SSL 設定]**。  
  
3.  核取 **[必須使用 SSL]** 選項。 在 **[用戶端憑證]**底下，確認已選取 **[略過]** 按鈕。  
  
#### <a name="to-create-a-self-signed-certificate-for-testing"></a>若要針對測試建立自我簽署憑證  
  
1.  在 **[Internet Information Services (IIS) 管理員]**中，按一下本機伺服器節點，然後在中央窗格中，按兩下 **[伺服器憑證]**。  
  
2.  在 **[動作]** 窗格中，按一下 **[建立自我簽署憑證]**。  
  
3.  在 **[建立自我簽署憑證]** 對話方塊中，輸入憑證的名稱，然後按一下 **[確定]**。  
  
###### <a name="to-bind-a-certificate-to-a-web-site"></a>若要將憑證繫結至網站  
  
1.  在 **[連線]** 窗格中，按一下 **[預設的網站]** (或是您的 Web 同步處理網站，如果它與預設的網站不同的話)。  
  
2.  在 **[動作]** 窗格中，按一下 **[繫結]**，然後按一下 **[新增]**。 **[新增站台繫結]** 對話方塊將會出現。  
  
3.  從 **[類型]** 下拉式清單中選取 **[https]**。 保留 **[IP 位址]** 和 **[連接埠]**的預設設定。  
  
4.  從 **[SSL 憑證]** 下拉式清單中，選取您在＜若要針對測試建立自我簽署憑證＞中建立的憑證、按一下 **[確定]**，然後按一下 **[關閉]**。  
  
###### <a name="to-test-the-certificate"></a>若要測試憑證  
  
1.  在 **在ternet 在formation Services (IIS) Manager**中，按一下 **[預設的網站].**  
  
2.  在 [動作] 窗格中，按一下 [瀏覽 \*:443(https)]。  
  
3.  Internet Explorer 將開啟並顯示一則訊息：「此網站的安全性憑證有問題」。 這則警告是要告知您，相關聯的憑證是由無法辨識的 CA 所核發，而且可能不值得信任。 這是預期的警告，因此請按一下 **[繼續瀏覽此網站 (不建議)]**。  
  
4.  如果系統提示您 **[連線到 localhost]**，請輸入使用者名稱和密碼以繼續。 此時，您應該會看到網站的預設頁面。  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>設定 SQL Server Replication Listener 的權限  
 當訂閱者電腦連接到執行 IIS 的電腦時，系統會利用您先前設定 IIS 時所指定的驗證類型來驗證訂閱者。 IIS 驗證訂閱者之後，IIS 會檢查訂閱者是否獲授權叫用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。 您可藉由設定 replisapi.dll 的權限來控制可以叫用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫的使用者。 您必須適當地設定權限，才能避免未經授權的使用者存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。  
  
 若要設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener 執行時所用帳戶的最小權限，請完成下列程序。 下列程序中的步驟適用於執行 IIS 7.0 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 2008。  
  
 除了執行下列步驟之外，請確保所需的登入位於發行集存取清單 (PAL) 中。 如需 PAL 的詳細資訊，請參閱[保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
 **重要事項** ：在本節中建立的帳戶就是在同步處理期間連接至發行者和散發者的帳戶。 這個帳戶必須新增為散發和發行集伺服器的 SQL 登入帳戶。  
  
 用於 SQL Server Replication Listener 的帳戶必須擁有如＜合併代理程式安全性＞主題中＜連接到發行者或散發者＞一節底下所描述的權限。  
  
 總而言之，此帳戶必須：  
  
-   是發行集存取清單 (PAL) 的成員。  
  
-   對應至與發行集資料庫中之使用者相關聯的登入。  
  
-   對應至與散發資料庫中之使用者相關聯的登入。  
  
-   擁有快照集共用的讀取權限。  
  
#### <a name="to-configure-the-account-and-permissions"></a>若要設定帳戶和權限  
  
1.  在執行 IIS 的電腦上建立本機帳戶：  
  
    1.  開啟 **[伺服器管理員]**。 在 [開始] 功能表中，以滑鼠右鍵按一下 **[電腦]**，然後按一下 **[管理]**。  
  
    2.  在 **[伺服器管理員]**中，展開 **[設定]**，然後展開 **[本機使用者和群組]**。  
  
    3.  以滑鼠右鍵按一下 **[使用者]**，然後按一下 **[新增使用者]**。  
  
    4.  輸入使用者名稱與增強式密碼。 清除 **[使用者必須在下次登入時變更密碼]**。  
  
    5.  按一下 **[建立]**，然後按一下 **[關閉]**。  
  
2.  將此帳戶加入至 IIS_IUSRS 群組：  
  
    1.  在 **[伺服器管理員]**中，展開 **[設定]**、展開 **[本機使用者和群組]**，然後按一下 **[群組]**。  
  
    2.  以滑鼠右鍵按一下 **[IIS_IUSRS]**，然後按一下 **[加入群組]**。  
  
    3.  在 **[IIS_IUSRS 內容]** 對話方塊中，按一下 **[新增]**。  
  
    4.  在 **[選取使用者、電腦或群組]** 對話方塊中，加入在步驟 1 建立的帳戶。  
  
    5.  確認 **[從這個位置]** 顯示本機電腦的名稱 (而非網域)。 如果此欄位沒有顯示本機電腦名稱，請按一下 **[位置]**。 在 **[位置]** 對話方塊中，選取本機電腦，然後按一下 **[確定]**。  
  
    6.  在 [選取使用者]  對話方塊和 [IIS_IUSRS Properties] (IIS_IUSRS 屬性)  對話方塊中，按一下 [確定]。  
  
3.  將包含 replisapi.dll 之資料夾的最小權限授與帳戶：  
  
    1.  在 [Windows 檔案總管] 中，以滑鼠右鍵按一下您針對 replisapi.dll 所建立的資料夾，然後按一下 **[內容]**。  
  
    2.  在 **[安全性]** 索引標籤上，按一下 **[編輯]**。  
  
    3.  在 [\<資料夾名稱> 的權限] 對話方塊中，按一下 [新增] 以新增步驟 1 建立的帳戶。  
  
    4.  確認 **[從這個位置]** 顯示本機電腦的名稱 (而非網域)。 如果此欄位沒有顯示本機電腦名稱，請按一下 **[位置]**。 在 **[位置]** 對話方塊中，選取本機電腦，然後按一下 **[確定]**。  
  
    5.  確認只將**讀取**、**讀取與執行**和**列出資料夾內容**權限授與這個帳戶。  
  
    6.  選取任何不需要存取目錄的使用者或群組、按一下 **[移除]**，然後按一下 **[確定]**。  
  
4.  在 **[Internet Information Services (IIS) 管理員]**中建立應用程式集區：  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**的 **[連線]** 窗格中，展開本機伺服器節點。  
  
    2.  以滑鼠右鍵按一下 **[應用程式集區]**，然後按一下 **[新增應用程式集區]**。  
  
    3.  輸入應用程式集區的名稱、保留其餘欄位的預設值，然後按一下 **[確定]**。  
  
    > [!NOTE]  
    >  如果您預期有兩個以上的並行同步處理用戶端，可能會想要建立 Web 處理序區。 如需詳細資訊，請參閱[建立 Web 處理序區](../../relational-databases/replication/configure-web-synchronization.md)中的＜建立 Web 處理序區＞。  
  
5.  將帳戶與應用程式集區相關聯：  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**中，展開本機伺服器節點，然後按一下 **[應用程式集區]**。  
  
    2.  以滑鼠右鍵按一下您先前建立的應用程式集區，然後按一下 **[設定應用程式集區預設值]**。  
  
    3.  在 **[應用程式集區預設值]** 對話方塊中，向下捲動至 **[處理序模型]** 區段，然後按一下 **[識別]** 欄位。  
  
    4.  按一下位於 **[識別]** 列右側的省略符號按鈕。  
  
    5.  按一下 **[自訂帳戶]** 選項按鈕，然後按一下 **[設定]**。  
  
    6.  在 **[使用者名稱]** 和 **[密碼]** 欄位中，輸入步驟 1 中建立的帳戶和密碼，然後按一下 **[確定]**。  
  
    7.  按一下 [確定]  關閉 [應用程式集區識別]  對話方塊，然後再按一下 [確定]  關閉 [應用程式集區預設值] 對話方塊。  
  
6.  讓應用程式集區與複寫網站產生關聯：  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**中，展開本機伺服器節點，然後按一下 **[預設的網站]** (或是您的 Web 同步處理網站，如果它與預設的網站不同的話)。  
  
    2.  在 **[動作]** 窗格的 **[管理網站]**底下，按一下 **[進階設定]**。  
  
    3.  在 **[進階設定]** 對話方塊中，按一下 **[應用程式集區]**右側的省略符號按鈕。  
  
    4.  從 **[應用程式集區]** 下拉式清單中，選取您在步驟 4 中建立的應用程式集區，然後按一下 **[確定]**。  
  
    5.  再次按一下 **[確定]** 關閉 [進階設定]。  
  
## <a name="testing-the-connection-to-replisapidll"></a>測試與 replisapi.dll 的連接  
 在診斷模式下執行 Web 同步處理，以測試執行 IIS 之電腦的連接，並確定安全通訊端層 (SSL) 憑證已正確安裝。 若要在診斷模式下執行 Web 同步處理，您必須是執行 IIS 之電腦上的管理員。  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>若要測試與 replisapi.dll 的連接  
  
1.  確定訂閱者端的區域網路 (LAN) 設定正確：  
  
    1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 的 **[工具]** 功能表中，按一下 **[網際網路選項]**。  
  
    2.  在 **[連接]** 索引標籤中，按一下 **[LAN 設定]**。  
  
    3.  如果 LAN 上未使用 Proxy 伺服器，請清除 **[自動偵測設定]** 與 **[在 LAN 中使用 Proxy 伺服器]**。  
  
    4.  如果使用 Proxy 伺服器，請按一下 **[在您的區域網路使用 Proxy 伺服器]** 和 **[近端網址不使用 Proxy]**，然後按一下 **[確定]**。  
  
2.  在訂閱者端的 Internet Explorer 中，將 `?diag` 附加至 replisapi.dll 的位址，以便在診斷模式下連接伺服器。 例如： `https://server.domain.com/directory/replisapi.dll?diag`＞。  
  
    > [!NOTE]  
    >  在上述範例中，您應該將 **server.domain.com** 取代成 IIS 管理員中 **[伺服器憑證]** 區段底下所列的確切 **[發行給]** 名稱。  
  
3.  如果 Windows 作業系統無法辨識您先前為 IIS 指定的憑證，則會出現 **[安全性警示]** 對話方塊。 發生此警示的可能是因為該憑證是測試憑證，或者該憑證是由 Windows 無法辨識的憑證授權單位 (CA) 所發行。  
  
    > [!NOTE]  
    >  如果未出現此對話方塊，請確定您要存取之伺服器的憑證已做為信任憑證加入訂閱者端的憑證存放區中。 如需有關匯入憑證的詳細資訊，請參閱 IIS 文件集。  
  
    1.  在 **[安全性警示]** 對話方塊中，按一下 **[檢視憑證]**。  
  
    2.  在 **[憑證]** 對話方塊的 **[一般]** 索引標籤上，按一下 **[安裝憑證]**。  
  
    3.  完成「憑證匯入精靈」，以接受預設值。  
  
    4.  在 **[安全性警告]** 對話方塊中，按一下 **[是]**。  
  
    5.  在「憑證匯入精靈」確認對話方塊中，按一下 **[確定]**。  
  
    6.  關閉 **[憑證]** 對話方塊。  
  
    7.  在 **[安全性警示]** 對話方塊中，按一下 **[是]**。  
  
    > [!NOTE]  
    >  將為使用者安裝憑證。 這項處理序必須針對將與 IIS 同步處理的每位使用者執行。  
  
4.  在 [連接到 \<伺服器名稱>] 對話方塊中，指定合併代理程式要用來連接 IIS 的登入和密碼。 也可以在「新增訂閱精靈」中指定這些認證。  
  
5.  在稱為 **[SQL Websync 診斷資訊]**的 Internet Explorer 視窗中，確認頁面中每個 **[狀態]** 資料行中的值都是 **[SUCCESS]**。  
  
6.  確定憑證已正確安裝於訂閱者端：  
  
    1.  關閉 Internet Explorer，然後再重新開啟。  
  
    2.  在診斷模式下連接到伺服器。 如果憑證已正確安裝，就不會出現 **[安全性警示]** 對話方塊。 如果出現此對話方塊，合併代理程式將在嘗試連接到執行 IIS 的電腦時失敗。 您必須確定要存取的伺服器憑證已做為信任憑證加入訂閱者端的憑證存放區中。 如需有關匯入憑證的詳細資訊，請參閱 IIS 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的 Web 同步處理](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)  
  
  

