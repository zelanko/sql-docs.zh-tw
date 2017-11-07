---
title: "設定 Analysis Services 及 Kerberos 限制委派 (KCD) |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0006e143-d3ba-4d10-a415-e42c45e2bb0a
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c13b9095224d1c33e09c9513121e46483da05c0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="configure-analysis-services-and-kerberos-constrained-delegation-kcd"></a>設定 Analysis Services 及 Kerberos 限制委派 (KCD)
  Kerberos 限制委派 (KCD) 是驗證通訊協定，您可使用 Windows 驗證對其進行設定，在整個環境的服務間委派用戶端認證。 KCD 需要其他基礎結構 (例如網域控制站)，以及您環境的其他組態。 某些在 SharePoint 2016 使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 資料的案例會需要 KCD。 在 SharePoint 2016 中，Excel Services 已從 SharePoint 伺服器陣列外移到不同的新伺服器： **Office Online Server**。 因為 Office Online Server 是獨立的，所以對於在典型雙躍點案例中委派用戶端認證的方法，其需求漸增。  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016|  
  
## <a name="overview"></a>概觀  
 KCD 可讓帳戶模擬另一個帳戶，以提供資源的存取權。 進行模擬的帳戶可以是指派給 Web 應用程式的服務帳戶或網頁伺服器的電腦帳戶，而受模擬的帳戶必須是要求資源存取權的使用者帳戶。 KCD 會在服務層級運作，讓模擬的帳戶可將存取權授與伺服器上選取的服務，同時拒絕讓相同伺服器上的其他服務或其他伺服器上的服務進行存取。  
  
 本主題中的章節將檢閱需要 KCD 的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 及 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 常見案例，還有範例伺服器部署可讓您大致了解需要安裝及設定的項目。 如需其中涉及的技術 (例如網域控制站及 KCD) 詳細資訊，請參閱 [其他資訊及社群內容](#bkmk_moreinfo) 一節中的連結。  
  
## <a name="scenario-1-workbook-as-data-source-wds"></a>案例 1︰以活頁簿作為資料來源 (WDS)。  
 ![請參閱 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "看到 1") Office Online Server 會開啟 Excel 活頁簿和![請參閱 2](../../../analysis-services/instances/install-windows/media/ssas-callout2.png "請參閱 2")偵測到另一個活頁簿的資料連接。 Office Online Server 傳送要求以[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]重新導向程式服務![看到 3](../../../analysis-services/instances/install-windows/media/ssas-callout3.png "看到 3")開啟第二個活頁簿和資料![請參閱 4](../../../analysis-services/instances/install-windows/media/ssas-callout4.png "請參閱 4").  
  
 在此案例中，必須將使用者認證從 Office Online Server 委派給 SharePoint 中的 SharePoint [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 重新導向程式服務。  
  
 ![做為資料來源的活頁簿](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-wds.png "做為資料來源的活頁簿")  
  
## <a name="scenario-2-an-analysis-services-tabular-model-links-to-an-excel-workbook"></a>案例 2：連結至 Excel 活頁簿的 Analysis Services 表格式模型  
 Analysis Services 表格式模型![看到 1](../../../analysis-services/instances/install-windows/media/ssas-callout1.png "看到 1")連結到包含 Power Pivot 模型的 Excel 活頁簿。 在此案例中，當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 載入表格式模型時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會偵測到活頁簿的連結。 處理模型時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會將查詢要求傳送至 SharePoint，以載入活頁簿。 在此案例中，「不」  需要將用戶端認證從 Analysis Services 委派給 SharePoint，不過用戶端應用程式可能會覆寫非正規繫結中的資料來源資訊。 如果非正規繫結要求指定要模擬目前的使用者，就必須委派使用者認證，而這會需要在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 與 SharePoint 之間設定 KCD。  
  
 ![office online server](../../../analysis-services/instances/install-windows/media/ssas-kcd-wtih-oos.png "office online server")  
  
## <a name="example-deployment-of-kcd-with-office-online-server-and-analysis-services"></a>使用 Office Online Server 及 Analysis Services 的 KCD 範例部署  
 本章節描述使用四部電腦進行的範例部署。 下列章節則摘要說明每部電腦上主要的安裝及設定步驟。 在開始部署之前，建議您先使用作業系統修補將電腦處於最新狀態，並請記得電腦名稱，因為有些組態步驟將會用到。  
  
-   網域控制站  
  
-   SQL Server 資料庫引擎和 Power Pivot 模式的 Analysis Services。 資料庫引擎的執行個體將用於 SharePoint 內容資料庫。  
  
-   SharePoint server 2016  
  
-   Office Online Server  
  
 ![domain controller](../../../analysis-services/instances/install-windows/media/ssas-kcd-domainserver-icon.png "domain controller")  
  
### <a name="domain-controller"></a>網域控制站  
 以下摘要說明要為網域控制站 (DC) 安裝的項目。  
  
-   **角色** ︰Active Directory 網域服務。 如需概觀，請參閱 [Configuring Active Directory (AD DS) in Windows Server 2012](http://sharepointgeorge.com/2012/configuring-active-directory-ad-ds-in-windows-server-2012/)(在 Windows Server 2012 中設定 Active Directory (AD DS))。  
  
-   **角色** ︰DNS 伺服器  
  
-   **功能** ︰.NET Framework 3.5 功能/.NET Framework 3.5  
  
-   **功能** ：遠端伺服器管理工具/角色管理工具  
  
-   設定 Active Directory 以建立新的樹系，並將電腦聯結至網域。 您必須先將用戶端電腦 DNS 設為 DC 的 IP 位址，然後再嘗試將其他電腦加入私人網域中。 在 DC 電腦上，執行 `ipconfig /all` 為下個步驟取得 IPv4 及 IPv6 位址。  
  
-   建議您同時設定 IPv4 及 IPv6 位址。 您可在 Windows 控制台執行此動作︰  
  
    1.  按一下 [網路和共用中心]   
  
    2.  按一下您的乙太網路連線  
  
    3.  按一下 [屬性]   
  
    4.  按一下 [網際網路通訊協定第 6 版 (TCP/IPv6)]   
  
    5.  按一下 [屬性]   
  
    6.  按一下 [使用下列的 DNS 伺服器位址]   
  
    7.  輸入來自 ipconfig 命令的 IP 位址。  
  
    8.  按一下 [進階]  按鈕，再按一下 [DNS]  索引標籤，並確認 DNS 尾碼是否正確。  
  
    9. 按一下 [附加這些 DNS 尾碼]   
  
    10. 為 IPv4 重複以上步驟。  
  
-   **注意︰** 您可從 Windows [控制台] 的 [系統] 設定，將電腦加入網域。 如需詳細資訊，請參閱 [How To Join Windows Server 2012 to a Domain](http://social.technet.microsoft.com/wiki/contents/articles/20260.how-to-join-windows-server-2012-to-a-domain.aspx)(如何將 Windows Server 2012 加入網域)。  
  
 ![powerpivot 模式中的 ssas 伺服器](../../../analysis-services/instances/install-windows/media/ssas-kcd-powerpivotserver-icon.png "ssas powerpivot 模式伺服器")  
  
### <a name="2016-sql-server-database-engine-and-analysis-services-in-power-pivot-mode"></a>2016 SQL Server 資料庫引擎和 Power Pivot 模式的 Analysis services  
 以下摘要說明要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 電腦上安裝的項目。  
  
 ![請注意](../../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")中[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]安裝精靈[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中 Power Pivot 模式安裝做為特徵選取工作流程的一部分。  
  
1.  執行 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 安裝精靈，然後從特徵選取頁面依序按一下資料庫引擎、 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]及管理工具。 您可在安裝精靈稍後的安裝中，對 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 指定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]模式。  
  
2.  為執行個體組態設定具名執行個體 "POWERPIVOT"。  
  
3.  在 [Analysis Services 組態] 頁面上，設定 **PowerPivot** 模式的 Analysis Services 伺服器，並將 Office Online Server 的 **電腦名稱** 加入 Analysis Services 伺服器管理員清單中。 如需詳細資訊，請參閱 [以 PowerPivot 模式安裝 Analysis Services](../../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)。  
  
4.  請注意，根據預設，搜尋中不包括 “Computer” 物件類型。 按一下![按一下要新增電腦帳戶物件](../../../analysis-services/instances/install-windows/media/ss-objects-button.png "按一下要新增電腦帳戶物件")新增 Computers 物件。  
  
     ![將電腦帳戶新增為 ssas 管理員](../../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "ssas 系統管理員的身分新增電腦帳戶")  
  
5.  建立 Analysis Services 執行個體的服務主體名稱 (SPN)。  
  
     下列是實用的 SPN 命令︰  
  
    -   為執行感興趣服務的特定帳戶名稱列出 SPN： `SetSPN -l <account-name>`  
  
    -   為執行感興趣服務的帳戶名稱設定 SPN： `SetSPN -a <SPN> <account-name>`  
  
    -   從執行感興趣服務的特定帳戶名稱刪除 SPN： `SetSPN -D <SPN> <account-name>`  
  
    -   搜尋重複的 SPN： `SetSPN -X`  
  
     PowerPivot 執行個體的 SPN 格式如下︰  
  
    ```  
    MSSQLSvc.3/\<Fully Qualified Domain Name (FQDN)>:POWERPIVOT  
    MSSQLSvc.3/<NetBIOS Name>:POWERPIVOT  
    ```  
  
     其中的 FQDN 及 NetBIOS 名稱是執行個體所在的電腦名稱。 這些 SPN 會放置在服務帳戶使用的網域帳戶上。  若您使用網路服務、本機系統或服務識別碼，建議將 SPN 置於網域電腦帳戶。  若您使用網域使用者帳戶，則建議將 SPN 置於該帳戶。  
  
6.  在 Analysis Services 電腦上建立 SQL Browser 服務的 SPN。  
  
     [深入了解](https://support.microsoft.com/en-us/kb/950599)  
  
7.  請對您會在其中進行重新整理的任何外部來源 (例如 SQL Server 或 Excel 檔案)，在 Analysis Services 服務帳戶上**設定限制委派** 。 我們想確定下列項目在 Analysis Services 帳戶已完成設定  
  
     **注意** ︰若您在 [Active Directory 使用者和電腦] 中看不到帳戶的 [委派] 索引標籤，是因為該帳戶上沒有 SPN。  您可以新增假的 SPN (例如 `my/spn`) 使其出現。  
  
     **信任這個使用者，但只委派指定的服務** ，並 **使用任何驗證通訊協定**。  
  
     這稱為限制委派，而且不可或缺，因為 Windows Token 源自 Claims to Windows Token Service (C2WTS)，而其需要會轉換通訊協定的限制委派。  
  
     ![Analysis Services-限制委派](../../../analysis-services/instances/install-windows/media/analysis-services-constrained-delegation.png "Analysis Services-限制委派")  
  
     您也必須新增服務，作為您的委派目標。 這會視您的環境而有所不同。  
  
### <a name="office-online-server"></a>Office Online Server  
  
1.  安裝 Office Online Server  
  
2.  **設定 Office Online Server** 以連接至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器。 請注意，Office Online Server 電腦帳戶必須是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器上的系統管理員。 在本主題的前一節已完成安裝 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器。  
  
    1.  在 Office Online Server 上，以系統管理權限開啟 PowerShell 視窗，並執行下列命令  
  
    2.  `New-OfficeWebAppsExcelBIServer –ServerId <AS instance name>`  
  
    3.  範例： `New-OfficeWebAppsExcelBIServer –ServerId "MTGQLSERVER-13\POWERPIVOT"`  
  
3.  **設定 Active Directory** 以允許 Office Online Server 電腦帳戶模擬 SharePoint 服務帳戶的使用者。 因此，請在 Office Online Server 上為 SharePoint Web 服務執行應用程式集區的主體上設定委派內容：本章節中的 PowerShell 命令需要 Active Directory PowerShell 物件。  
  
    1.  取得 Office Online Server 的 Active Directory 身分識別  
  
        ```  
        $computer1 = Get-ADComputer -Identity [ComputerName]  
        ```  
  
         您可以在工作管理員 / 詳細資料 / w3wp.exe 的使用者名稱，找到此主體名稱。 例如 "svcSharePoint"  
  
        ```  
        Set-ADUser svcSharePoint -PrincipalsAllowedToDelegateToAccount $computer1  
  
        ```  
  
    2.  確認屬性已正確設定  
  
    3.  ```  
        Get-ADUser svcSharePoint –Properties PrincipalsAllowedToDelegateToAccount  
        ```  
  
4.  請對 Analysis Services PowerPivot 執行個體的 Office Online Server 帳戶**設定限制委派** 。 這必須是執行 Office Online Server 的電腦帳戶。 我們想確定下列項目在 Office Online Service 帳戶已完成設定。  
  
     **注意** ︰若您在 [Active Directory 使用者和電腦] 中看不到帳戶的 [委派] 索引標籤，是因為該帳戶上沒有 SPN。  您可以新增假的 SPN (例如 `my/spn`) 使其出現。  
  
     **信任這個使用者，但只委派指定的服務** ，並 **使用任何驗證通訊協定**。  
  
     這稱為限制委派，而且不可或缺，因為 Windows Token 源自 Claims to Windows Token Service (C2WTS)，而其需要會轉換通訊協定的限制委派。  接著建議您允許我們在上方建立的 MSOLAPSvc.3 及 MSOLAPDisco.3 SPN 委派。  
  
5.  設定「對 Windows Token 服務的宣告」(C2WTS)， **此為案例 1 所需**。 如需詳細資訊，請參閱 [對 Windows Token 服務的宣告 (C2WTS) 概觀](https://msdn.microsoft.com/library/ee517278.aspx)。  
  
6.  請對 C2WTS 服務帳戶**設定限制委派** 。  設定應符合您在步驟 4 中的作法。  
  
 ![sharepoint server](../../../analysis-services/instances/install-windows/media/ssas-kcd-sharepointserver-icon.png "sharepoint 伺服器")  
  
### <a name="sharepoint-server-2016"></a>SharePoint Server 2016  
 以下摘要說明 SharePoint Server 安裝。  
  
1.  執行 SharePoint 必要條件安裝程式  
  
2.  執行 SharePoint 安裝並選取 [Single Server Farm (單一伺服器陣列)]  安裝程式角色。  
  
3.  執行 PowerPivot for SharePoint 增益集 (spPowerPivot16.msi)。 如需詳細資訊，請參閱[安裝或解除安裝 Powerpivot for SharePoint 增益集 (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
4.  執行 [PowerPivot 組態精靈]。 請參閱 [PowerPivot 組態工具](../../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)。  
  
5.  將 SharePoint 連接至 Office Online Server。    ??Configure_xlwac_on_SPO.ps1 ??  
  
6.  設定 Kerberos 的 SharePoint 驗證提供者。 **此為案例 1 所需**。 如需詳細資訊，請參閱 [Plan for Kerberos authentication in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx)(規劃 SharePoint 2013 的 Kerberos 驗證)。  
  
##  <a name="bkmk_moreinfo"></a> 其他資訊及社群內容  
 [適用於忙碌管理員的 Kerberos](http://blogs.technet.com/b/askds/archive/2008/03/06/kerberos-for-the-busy-admin.aspx)  
  
 [了解 Kerberos 雙躍點](http://blogs.technet.com/b/askds/archive/2008/06/13/understanding-kerberos-double-hop.aspx)  
  
 [.Net 與 SharePoint 的一切](http://sbrickey.com/Tech/Blog/Post/Kerberos_Primer)  
  
 [以資源為基礎的 Kerberos 限制委派](http://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)  
  
 [KERBEROS PRIMER - 影片](http://blog.martinlund.it/kerberos-primer/)  
  
 [Microsoft® Kerberos Configuration Manager for Microsoft SQL Server®](http://www.microsoft.com/en-us/download/details.aspx?id=39046)  
  
  

