---
title: "Enable Encrypted Connections to the Database Engine (SQL Server Configuration Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "連線 [SQL Server], 已加密"
  - "SSL [SQL Server]"
  - "安全通訊端層 (SSL) (Secure Sockets Layer (SSL))"
  - "加密 [SQL Server], 連線"
  - "加密 [SQL Server], 連線"
  - "憑證 [SQL Server], 安裝"
  - "要求加密的連接"
  - "安裝憑證"
  - "security [SQL Server], encryption"
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Enable Encrypted Connections to the Database Engine (SQL Server Configuration Manager)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 組態管理員指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的憑證，以啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的加密連接。 伺服器電腦必須提供憑證，且用戶端機器必須設定為信任該憑證的根授權單位。 提供是安裝憑證的處理序，方法是將它匯入 Windows。  
  
 您必須針對 **伺服器驗證**發出此憑證。 憑證的名稱必須是電腦的完整網域名稱 (FQDN)。  
  
 電腦上之使用者的憑證會儲存在本機中。 若要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的憑證，則除非服務是以 LocalSystem、NetworkService 或 LocalService 執行，否則您必須使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務相同的使用者帳戶來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，而在此情況下，您可以使用管理帳戶。  
  
 用戶端必須可確認伺服器所使用之憑證的擁有權。 如果用戶端具有已簽署伺服器憑證之憑證授權單位的公開金鑰憑證，則不需要進一步進行組態設定。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 包含許多憑證授權單位的公開金鑰憑證。 如果伺服器憑證是由用戶端沒有公開金鑰憑證的公開或私人憑證授權單位所簽署，則您必須安裝已簽署伺服器憑證之憑證授權單位的公開金鑰憑證。  
  
> [!NOTE]  
>  若要在容錯移轉叢集中使用加密功能，請務必在容錯移轉叢集中的所有節點上，對於虛擬伺服器使用完整的 DNS 名稱來安裝伺服器憑證。 例如，假設您有一個雙節點的叢集，節點的名稱分別為 test1.*\<您的公司>*.com 與 test2.*\<您的公司>*.com，而且您有一個名為 virtsql 的虛擬伺服器，則兩個節點上都需要安裝 virtsql.*\<您的公司>*.com 的憑證。 您可以將 [[ForceEncryption]] **[ForceEncryption]**選項的值設為 [是] **[是]**。  

> [!NOTE]
> 在 Azure VM 上建立 Azure 搜尋服務索引子到 SQL Server 的加密連線時，請參閱[在 Azure VM 上設定從 Azure 搜尋服務索引子到 SQL Server 的連線](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/)。 
  
 
##  <a name="SSMSProcedure"></a>  
  
###  <a name="Provision"></a> 若要在伺服器上提供 (安裝) 憑證  
  
1.  在 [開始]  功能表中按一下 [執行] ，然後在 [開啟]  方塊中輸入 **MMC** ，然後按一下 [確定] 。  
  
2.  在 MMC 主控台的 [檔案] 功能表上，按一下 [新增/移除嵌入式管理單元]。  
  
3.  在 [新增/移除嵌入式管理單元] 對話方塊中，按一下 [新增]。  
  
4.  在 [新增獨立嵌入式管理單元] 對話方塊中，按一下 [憑證]，然後按 [新增]。  
  
5.  在 [憑證嵌入式管理單元] 對話方塊中，按一下 [電腦帳戶]，然後按 [完成]。  
  
6.  在 [新增獨立嵌入式管理單元] 對話方塊中，按一下 [關閉]。  
  
7.  在 [新增/移除嵌入式管理單元] 對話方塊中，按一下 [確定]。  
  
8.  在 [憑證] 嵌入式管理單元中，展開 [憑證] 後再展開 [個人]，然後以滑鼠右鍵按一下 [憑證]，接著指向 [所有工作]，再按 [匯入]。  

9. 以滑鼠右鍵按一下匯入的憑證，並指向 [所有工作]，然後按一下 [管理私密金鑰]。 在 [安全性] 對話方塊中，新增 SQL Server 服務帳戶所使用之使用者帳戶的讀取權限。  
  
10. 完成 **[憑證匯入精靈]**以加入憑證至電腦中，然後關閉 MMC 主控台。 如需新增憑證至電腦的詳細資訊，請參閱 Windows 文件集。  
  
###  <a name="Export"></a> 若要匯出伺服器憑證  
  
1.  從 [憑證] 嵌入式管理單元的 [憑證] / [個人] 資料夾中找到憑證，以滑鼠右鍵按一下 [憑證]，並指向 [所有工作]，然後按一下 [匯出]。  
  
2.  完成 **[憑證匯出精靈]**，並將憑證檔儲存在方便取得的位置。  
  
###  <a name="ConfigureServerConnections"></a> 若要設定伺服器接受加密的連接  
  
1.  在 [SQL Server 組態管理員] 中，展開 [SQL Server 網路組態]，並以滑鼠右鍵按一下 [*\<伺服器執行個體>* 的通訊協定]，然後選取 [屬性]。  
  
2.  在 [*\<執行個體名稱>* 屬性的通訊協定] 對話方塊的 [憑證] 索引標籤上，從 [憑證] 方塊的下拉式清單中選取所需的憑證，然後按一下 [確定]。  
  
3.  在 **[旗標]** 索引標籤的 **[ForceEncryption]** 方塊中選取 **[是]**，然後按一下 **[確定]** 以關閉對話方塊。  
  
4.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
###  <a name="ConfigureClientConnections"></a> 若要設定用戶端要求加密的連接  
  
1.  將原始憑證或匯出的憑證檔複製到用戶端電腦。  
  
2.  在用戶端電腦上，使用 [憑證] 嵌入式管理單元安裝根憑證或匯出的憑證檔。  
  
3.  在主控台窗格中，以滑鼠右鍵按一下 [SQL Server Native Client 組態]，然後按一下 [屬性]。  
  
4.  在 **[旗標]** 頁面的 **[強制通訊協定加密]** 方塊中，按一下 **[是]**。  
  
###  <a name="EncryptConnection"></a> 若要從 SQL Server Management Studio 加密連接  
  
1.  在 [物件總管] 工具列上，按一下 **[連接]**，再按一下 **[Database Engine]**。  
  
2.  在 **[連接到伺服器]** 對話方塊中，完成連接資訊，然後按一下 **[選項]**。  
  
3.  在 **[連接屬性]** 索引標籤上，按一下 **[加密連接]**。  
  
## 另請參閱

[Microsoft SQL Server 的 TLS 1.2 支援](https://support.microsoft.com/kb/3135244)  
