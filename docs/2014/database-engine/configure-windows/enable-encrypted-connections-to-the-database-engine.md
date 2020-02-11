---
title: 啟用資料庫引擎的加密連接（SQL Server 組態管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a872057f354b289d65a6a3a730e3a63afd7af0d4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782312"
---
# <a name="enable-encrypted-connections-to-the-database-engine-sql-server-configuration-manager"></a>啟用 Database Engine 的加密連接 (SQL Server 組態管理員)
  此主題描述如何使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 組態管理員指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的憑證，以啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的加密連接。 伺服器電腦必須提供憑證，且用戶端機器必須設定為信任該憑證的根授權單位。 提供是安裝憑證的處理序，方法是將它匯入 Windows。  
  
 您必須針對 **伺服器驗證**發出此憑證。 憑證的名稱必須是電腦的完整網域名稱 (FQDN)。  
  
 電腦上之使用者的憑證會儲存在本機中。 若要安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所使用的憑證，則除非服務是以 LocalSystem、NetworkService 或 LocalService 執行，否則您必須使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務相同的使用者帳戶來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，而在此情況下，您可以使用管理帳戶。  
  
 用戶端必須可確認伺服器所使用之憑證的擁有權。 如果用戶端具有已簽署伺服器憑證之憑證授權單位的公開金鑰憑證，則不需要進一步進行組態設定。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 包含許多憑證授權單位的公開金鑰憑證。 如果伺服器憑證是由用戶端沒有公開金鑰憑證的公開或私人憑證授權單位所簽署，則您必須安裝已簽署伺服器憑證之憑證授權單位的公開金鑰憑證。  
  
> [!NOTE]  
>  若要在容錯移轉叢集中使用加密功能，請務必在容錯移轉叢集中的所有節點上，對於虛擬伺服器使用完整的 DNS 名稱來安裝伺服器憑證。 例如，如果您有兩個節點的叢集，且節點名為 test1。您的公司>.com 和 test2。 * \< *您的公司>.com，而且您有名為 virtsql 的虛擬伺服器，您必須安裝 virtsql 的憑證。 * \< *您的公司在這兩個節點上>.com。 * \< * 您可以將 [[ForceEncryption]] **[ForceEncryption]** 選項的值設為 [是] **[是]**。  
  
 **本主題內容**  
  
-   **若要啟用加密連接：**  
  
     [在伺服器上提供 (安裝) 憑證](#Provision)  
  
     [匯出伺服器憑證](#Export)  
  
     [設定伺服器接受加密連接](#ConfigureServerConnections)  
  
     [設定用戶端要求加密連接](#ConfigureClientConnections)  
  
     [從 SQL Server Management Studio 加密連接](#EncryptConnection)  
  
##  <a name="SSMSProcedure"></a>  
  
###  <a name="Provision"></a>在伺服器上提供（安裝）憑證  
  
1.  在 [**開始**] 功能表上，按一下 [**執行**]，然後在 [ `MMC` **開啟**] 方塊中輸入，然後按一下 **[確定]**。  
  
2.  在 MMC 主控台的 [檔案]  功能表上，按一下 [新增/移除嵌入式管理單元]  。  
  
3.  在 [新增/移除嵌入式管理單元]  對話方塊中，按一下 [新增]  。  
  
4.  在 [新增獨立嵌入式管理單元]  對話方塊中，按一下 [憑證]  ，然後按 [新增]  。  
  
5.  在 [憑證嵌入式管理單元]  對話方塊中，按一下 [電腦帳戶]  ，然後按 [完成]  。  
  
6.  在 [新增獨立嵌入式管理單元]  對話方塊中，按一下 [關閉]  。  
  
7.  在 [新增/移除嵌入式管理單元]  對話方塊中，按一下 [確定]  。  
  
8.  在 [憑證]  嵌入式管理單元中，展開 [憑證]  後再展開 [個人]  ，然後以滑鼠右鍵按一下 [憑證]  ，接著指向 [所有工作]  ，再按 [匯入]  。  
  
9. 完成 **[憑證匯入精靈]** 以加入憑證至電腦中，然後關閉 MMC 主控台。 如需新增憑證至電腦的詳細資訊，請參閱 Windows 文件集。  
  
###  <a name="Export"></a>若要匯出伺服器憑證  
  
1.  從 [憑證]  嵌入式管理單元的 [憑證]   / [個人]  資料夾中找到憑證，以滑鼠右鍵按一下 [憑證]  ，並指向 [所有工作]  ，然後按一下 [匯出]  。  
  
2.  完成 **[憑證匯出精靈]** ，並將憑證檔儲存在方便取得的位置。  
  
###  <a name="ConfigureServerConnections"></a>若要將伺服器設定為接受加密的連接  
  
1.  在 [SQL Server 組態管理員]  中，展開 [SQL Server 網路組態]  ，並以滑鼠右鍵按一下 [**伺服器執行個體>** _的通訊協定]\<_ ，然後選取 [屬性]  。  
  
2.  在 [_\<實例名稱_的**通訊協定**>**屬性**] 對話方塊的 [**憑證**] 索引標籤上，從 [**憑證**] 方塊的下拉式方塊中選取所需的憑證，然後按一下 **[確定]**。  
  
3.  在 **[旗標]** 索引標籤的 **[ForceEncryption]** 方塊中選取 **[是]** ，然後按一下 **[確定]** 以關閉對話方塊。  
  
4.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
###  <a name="ConfigureClientConnections"></a>設定用戶端要求加密的連接  
  
1.  將原始憑證或匯出的憑證檔複製到用戶端電腦。  
  
2.  在用戶端電腦上，使用 [憑證]  嵌入式管理單元安裝根憑證或匯出的憑證檔。  
  
3.  在主控台窗格中，以滑鼠右鍵按一下 [SQL Server Native Client 組態]****，然後按一下 [屬性]****。  
  
4.  在 **[旗標]** 頁面的 **[強制通訊協定加密]** 方塊中，按一下 **[是]** 。  
  
###  <a name="EncryptConnection"></a>若要從 SQL Server Management Studio 加密連接  
  
1.  在 [物件總管] 工具列上，按一下 **[連接]** ，再按一下 **[Database Engine]** 。  
  
2.  在 **[連接到伺服器]** 對話方塊中，完成連接資訊，然後按一下 **[選項]** 。  
  
3.  在 **[連接屬性]** 索引標籤上，按一下 **[加密連接]** 。  
  
  
