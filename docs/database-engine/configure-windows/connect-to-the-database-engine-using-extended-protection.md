---
title: 使用擴充保護連接至資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5216b324477f1af7fb727af3462ccce8d64e6a64
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012105"
---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>使用擴充保護連接至 Database Engine
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 開始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就支援 [擴充保護]。 **驗證擴充保護** 是作業系統實作的網路元件功能。 Windows 7 和 Windows Server 2008 R2 上可支援 **[擴充保護]** 。 Service Pack 中內含**擴充保護** ，可供舊版 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 作業系統使用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在使用 **擴充保護**進行連接時較安全。  
  
> [!IMPORTANT]  
> Windows 預設不會啟用 **[擴充保護]** 。 如需有關如何在 Windows 中啟用 **[擴充保護]** 的詳細資訊，請參閱 [驗證擴充保護](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)。
  
## <a name="description-of-extended-protection"></a>擴充保護的描述  
 **[擴充保護]** 會使用服務繫結與通道繫結來避免驗證轉送攻擊。 在驗證轉送攻擊中，可以執行 NTLM 驗證的用戶端 (如 Windows 檔案總管、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook、.NET SqlClient 應用程式等) 會連接到攻擊者 (如惡意 CIFS 檔案伺服器)。 攻擊者會使用用戶端的認證來偽裝成用戶端，並向服務驗證 (例如，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務的執行個體)。  
  
 這種攻擊有兩種變化：  
  
-   在引誘攻擊中引誘用戶端自願連接到攻擊者。  
  
-   在詐騙攻擊中，用戶端打算連接到有效的服務，但沒有注意到 DNS 和 IP 路由的其中一個或兩者已被侵害，所以連接會重新導向攻擊者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援服務繫結與通道繫結，以減少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的這些攻擊。  
  
### <a name="service-binding"></a>服務繫結  
 服務繫結位址引誘攻擊的方式，是要求用戶端傳送用戶端打算連接之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的已簽署服務主要名稱 (SPN)。 在驗證回應的過程中，該服務會驗證封包中收到的 SPN 與它自己的 SPN 相符。 如果用戶端被引誘連接到攻擊者，用戶端將會包含攻擊者的已簽署 SPN。 攻擊者無法轉送封包來向真正的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務驗證為用戶端，因為其中包含攻擊者的 SPN。 服務繫結會產生單次可忽略的成本，但是並不會處理詐騙攻擊。 當用戶端應用程式沒有使用加密來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，系統就會進行服務繫結。  
  
### <a name="channel-binding"></a>通道繫結  
 通道繫結會在用戶端與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的執行個體之間建立安全通道 (Schannel)。 此服務會驗證用戶端的真實性，其方式是比較該通道特定用戶端通道繫結權杖 (CBT) 與它自己的 CBT。 通道繫結會處理引誘和詐騙這兩種攻擊。 但是，它會發生較大的執行階段成本，因為它需要所有工作階段流量的傳輸層安全性 (TLS) 加密。 用戶端應用程式使用加密連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時會發生通道繫結，與加密由用戶端還是伺服器強制無關。  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 資料提供者支援 TLS 1.0 和 SSL 3.0。 如果您以在作業系統 SChannel 層級中進行變更的方式，強制執行不同的通訊協定 (例如 TLS 1.1 或 TLS 1.2)，您與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線可能會失敗。  
  
### <a name="operating-system-support"></a>作業系統支援  
 下列連結提供有關 Windows 如何支援 **[擴充保護]** 的詳細資訊：  
  
-   [具有擴充保護的整合式 Windows 驗證](https://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Microsoft 安全性摘要報告 (973811)，驗證擴充保護](/security-updates/SecurityAdvisories/2009/973811)
  
## <a name="settings"></a>設定  
 有三個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接設定會影響服務繫結與通道繫結。 這些設定可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員或 WMI 加以設定，而且可以使用原則型式管理中的 **[伺服器通訊協定設定]** Facet 加以檢視。  
  
-   **強制加密**  
  
     可能的值是 **[開啟]** 和 **[關閉]** 。 若要使用通道繫結，[ **強制加密** ] 必須設定為 [ **開啟**]，而所有用戶端將會強制加密。 如果設定為 **[關閉]** ，則只會保證服務繫結。 **[強制加密]** 位於 **組態管理員的** [MSSQLSERVER 的通訊協定屬性] ([旗標] 索引標籤) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。  
  
-   **擴充保護**  
  
     可能的值是 **[關閉]** 、 **[允許]** 和 **[必要]** 。 **[擴充保護]** 變數可讓使用者設定每個 **執行個體的** 擴充保護層級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **[擴充保護]** 位於 **組態管理員的** [MSSQLSERVER 的通訊協定屬性] ([進階] 索引標籤) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。  
  
    -   當設定為 **[關閉]** 時，便會停用 **[擴充保護]** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體將會接受來自任何用戶端的連接，不論用戶端是否受到保護。 **[關閉]** 與舊版及未修補的作業系統相容，但是比較不安全。 當您知道用戶端作業系統不支援擴充保護時，請使用這個設定。  
  
    -   當設定為 **[允許]** 時，支援 **[擴充保護]** 之作業系統的連接便需要 **[擴充保護]** 。 如果是不支援 **[擴充保護]** 之作業系統所做的連接，便會忽略 **[擴充保護]** 。 如果未受保護的用戶端應用程式在受保護的用戶端作業系統上執行，則會拒絕來自該應用程式的連接。 這個設定要比 **[關閉]** 安全，但不是最安全的設定。 請在某些作業系統支援 **[擴充保護]** 但某些不支援的混合式環境中使用這個設定。  
  
    -   當設定為 **[必要]** 時，只會接受來自受保護之作業系統上的受保護應用程式的連接。 這個設定最安全，但是不支援 **[擴充保護]** 之作業系統或應用程式的連接將無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   **接受的 NTLM SPN**  
  
     當一個以上的 SPN 知道伺服器時，便需要 **[接受的 NTLM SPN]** 變數。 當用戶端嘗試使用伺服器不知道的有效 SPN 連接到伺服器時，服務繫結將會失敗。 若要避免這個問題，使用者可以使用 **[接受的 NTLM SPN]** 來指定代表伺服器的數個 SPN。 **[接受的 NTLM SPN]** 是以分號分隔的一系列 SPN。 例如，若要允許 SPN **MSSQLSvc/ HostName1.Contoso.com** 和 **MSSQLSvc/ HostName2.Contoso.com**，請在 **[接受的 NTLM SPN]** 方塊中輸入 **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** 。 此變數的最大長度為 2,048 個字元。 **[接受的 NTLM SPN]** 位於 **組態管理員的** [MSSQLSERVER 的通訊協定屬性] ([進階] 索引標籤) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上。  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>啟用 Database Engine 的擴充保護  
 若要使用 **[擴充保護]** ，伺服器和用戶端都必須擁有支援 **[擴充保護]** 的作業系統，而且必須在作業系統上啟用 **[擴充保護]** 。 如需有關如何針對作業系統啟用 **[擴充保護]** 的詳細資訊，請參閱 [驗證擴充保護](/dotnet/framework/wcf/feature-details/extended-protection-for-authentication-overview)。  
  
 從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 開始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就支援 [擴充保護]。 某些舊版**的未來更新中將可以使用** [擴充保護] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在伺服器電腦上啟用 **[擴充保護]** 之後，請使用下列步驟來啟用 **[擴充保護]** ：  
  
1.  在 **[開始]** 功能表上，選擇 **[所有程式]** ，指向 **[Microsoft SQL Server]** ，然後按一下 **[SQL Server 組態管理員]** 。  
  
2.  展開 [SQL Server 網路組態]，然後在 [_\<_執行個體名稱*>* 的通訊協定] 上按一下滑鼠右鍵，再按一下 [屬性]。  
  
3.  針對通道繫結和服務繫結，在 **[進階]** 索引標籤上將 **[擴充保護]** 設定為適當的設定值。  
  
4.  當一個以上的 SPN 知道伺服器時，您也可以選擇在 **[進階]** 索引標籤上設定 **[接受的 NTLM SPN]** 欄位，如＜設定＞一節所述。  
  
5.  如果是通道繫結，請在 **[旗標]** 索引標籤上將 **[強制加密]** 設定為 **[開啟]** 。  
  
6.  重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務。  
  
## <a name="configuring-other-sql-server-components"></a>設定其他 SQL Server 元件  
 如需如何設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的詳細資訊，請參閱 [含有 Reporting Services 的驗證擴充保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)。  
  
 當使用 IIS 來透過 HTTP 或 HTTPs 連接存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以充分利用 IIS 所提供的擴充保護。 如需有關如何設定 IIS 使用擴充保護的詳細資訊，請參閱 [在 IIS 7.5 中設定擴充保護](https://go.microsoft.com/fwlink/?LinkId=181105)。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器網路組態](../../database-engine/configure-windows/server-network-configuration.md)   
 [用戶端網路組態](../../database-engine/configure-windows/client-network-configuration.md)   
 [驗證擴充保護概觀](https://go.microsoft.com/fwlink/?LinkID=177943)   
 [具有擴充保護的整合式 Windows 驗證](https://go.microsoft.com/fwlink/?LinkId=179922)  
  
  
