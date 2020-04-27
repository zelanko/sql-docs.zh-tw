---
title: 連接至遠端 Integration Services 伺服器（SSIS 服務） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], remote instance
- Integration Services service, connecting
- Integration Services service, remote instance
- service [Integration Services], connecting
ms.assetid: 9487aff1-44d8-42c1-8176-bb9891d4632d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e0e7e62510338b9dd47d59ce50626ecffebfcf85
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060418"
---
# <a name="connect-to-a-remote-integration-services-server-ssis-service"></a>連接到遠端 Integration Services 伺服器 (SSIS 服務)
    
> [!IMPORTANT] 
> 本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 從 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 或其他管理應用程式連接到遠端伺服器上的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行個體時，應用程式的使用者必須具備一組特定的伺服器權限。  
  
> [!IMPORTANT] 
> 若要管理儲存在遠端伺服器上的封裝，您不必連接到該遠端伺服器上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務執行個體， 而是要編輯 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的組態檔，好讓 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 顯示儲存在遠端伺服器上的封裝。 如需詳細資訊，請參閱 [設定 Integration Services 服務 &#40;SSIS 服務&#41;](service/integration-services-service-ssis-service.md)回溯相容。  
  
## <a name="connecting-to-integration-services-on-a-remote-server"></a>連接到遠端伺服器上的 Integration Services  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>連接到遠端伺服器上的 Integration Services  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  依序選取 [檔案]****、[連接物件總管]****，以顯示 [連接到伺服器]**** 對話方塊。  
  
3.  選取 [伺服器類型]**** 清單中的 [Integration Services]****。  
  
4.  在 [伺服器名稱]**** 文字方塊中鍵入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器的名稱。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務不是執行個體特定的。 您可以使用 Integration Services 服務執行所在的電腦名稱來連接此服務。  
  
5.  按一下 [ **連接**]。  
  
> [!NOTE]  
>  [瀏覽伺服器]**** 對話方塊不會顯示 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的遠端執行個體。 此外，[連接到伺服器]**** 對話方塊的 [連接選項]**** 索引標籤 (按一下 [選項]**** 按鈕即可顯示) 上的可用選項不適用於 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 連接。  
  
## <a name="eliminating-the-access-is-denied-error"></a>排除「存取遭到拒絕」的錯誤  
 如果不具備足夠權限的使用者試圖連接到遠端伺服器上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 執行個體，伺服器便會回應「存取遭到拒絕」的錯誤訊息。 只要確保使用者具有 DCOM 權限，就可以避免產生這個錯誤訊息。  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>設定 Windows Server 2003 或 Windows XP 遠端使用者的權限  
  
1.  如果使用者不是本機 Administrators 群組的成員，請將使用者加入「分散式 COM 使用者」群組。 您可以從 [系統管理工具]**** 功能表中的 [電腦管理] MMC 嵌入式管理單元進行這項作業。  
  
2.  開啟 [控制台]，依序按兩下 [系統管理工具]****、[元件服務]**** 啟動 [元件服務] MMC 嵌入式管理單元。  
  
3.  展開控制台左邊窗格中的 [元件服務]**** 節點。 依序展開 [電腦]**** 節點和 [我的電腦]****，然後按一下 [DCOM 設定]**** 節點。  
  
4.  選取 [DCOM 設定]**** 節點，然後選取可以設定之應用程式清單中的 SQL Server Integration Services 11.0。  
  
5.  以滑鼠右鍵按一下 SQL Server Integration Services 11.0，然後選取 [內容]****。  
  
6.  在 [SQL Server Integration Services 11.0 內容]**** 對話方塊中，選取 [安全性]**** 索引標籤。  
  
7.  選取 [啟動和啟用權限]**** 底下的 [自訂]****，然後按一下 [編輯]**** 開啟 [啟動權限]**** 對話方塊。  
  
8.  在 [啟動權限]**** 對話方塊中，新增或刪除使用者，並指派適當權限給適當的使用者與群組。 可用的權限有本機啟動、遠端啟動、本機啟用以及遠端啟用。 啟動權限可授與或拒絕啟動及停止服務的權限；啟用權限則可以授與或拒絕連接到服務的權限。  
  
9. 按一下 [確定] 關閉對話方塊。  
  
10. 在 [存取權限]**** 底下，重複步驟 7 和 8，為適當的使用者和群組指派適當的權限。  
  
11. 關閉 MMC 嵌入式管理單元。  
  
12. 重新啟動 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>設定具有最新 Service Pack 版本的 Windows 2000 遠端使用者權限  
  
1.  在命令提示字元執行 **dcomcnfg.exe** 。  
  
2.  在 [分散式 COM 組態內容]**** 對話方塊的 [應用程式]**** 頁面上，選取 SQL Server Integration Services 11.0，然後按一下 [內容]****。  
  
3.  選取 [安全性] 頁面 **** 。  
  
4.  使用兩個分開的對話方塊設定 [存取權限]**** 與 [啟動權限]****。 您無法區分遠端與本機存取，存取權限包含了本機與遠端存取，而啟動權限則包含了本機與遠端啟動。  
  
5.  關閉對話方塊和 **dcomcnfg.exe**。  
  
6.  重新啟動 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。  
  
## <a name="connecting-by-using-a-local-account"></a>使用本機帳戶進行連接  
 如果您是在用戶端電腦上使用本機 Windows 帳戶工作，那麼只有當遠端電腦上存在和本機帳戶相同名稱與密碼以及適當權限的帳戶，您才能連接到遠端電腦上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。  
  
## <a name="by-default-the-ssis-service-does-not-support-delegation"></a>SSIS 服務預設不支援委派  
根據預設[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，服務不支援認證的委派，或有時稱為雙躍點。 在這種情況中，您是在用戶端電腦上工作、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務是在第二部電腦上執行， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 則是在第三部電腦上執行。 首先， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 已順利將認證從用戶端電腦傳遞至正在其上執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的第二部電腦。 接著，不過， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務無法將認證從第二部電腦委派至正在其上執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的第三部電腦。

將 [信任這個使用者，可委派任何服務 (只限 Kerberos)]**** 權限授與 SQL Server 服務帳戶 (可將 Integration Services 服務 (ISServerExec.exe) 啟動為子處理序)，即可啟用認證委派。 在授與此權限之前，請考慮它是否符合您組織的安全性需求。

如需詳細資訊，請參閱 [取得使用 SSIS 封裝的跨網域 Kerberos 和委派](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)。
  
## <a name="see-also"></a>另請參閱  
 [針對 SSIS 服務的存取設定 Windows 防火牆](../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)  
  
  
