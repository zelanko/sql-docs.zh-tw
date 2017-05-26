---
title: "SQL Server 2012 SP1 版本資訊 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72171357-28de-4edd-bdfd-194f97225a6f
caps.latest.revision: 49
author: byham
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 47cba5e99626a7b378c29a9dde4923963fae09da
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-2012-sp1-release-notes"></a>SQL Server 2012 SP1 Release Notes
這份版本資訊文件說明您在安裝或對 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 進行疑難排解之前應該閱讀的已知問題。 這份版本資訊文件僅於線上提供，安裝媒體中並不提供，而且會定期更新。  
  
## <a name="bkmk_top"></a>目錄  
[1.0 安裝之前](#bmk_Install)  
  
[2.0 Analysis Services 和 PowerPivot](#bkmk_AS)  
  
[3.0 Reporting Services](#bkmk_RS)  
  
[4.0 Data Quality Services](#bkmk_DQS)  
  
[5.0 SQL Server Express](#bkmk_Express)  
  
[6.0 Attunity Oracle 異動資料擷取 (CDC) 服務和設計工具](#bkmk_CDC)  
  
[7.0 SQL Server 資料層應用程式架構 (DACFx)](#DACFx)  
  
[8.0 此 Service Pack 中修正的已知問題](#bkmk_known_issues_fixed)  
  
## <a name="bmk_Install"></a>1.0 安裝之前  
在安裝 SQL Server 2012 SP1 之前，請考量以下資訊。  
  
### <a name="11-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.1 如果您使用相同的 IP 位址，重新安裝 SQL Server 容錯移轉叢集的執行個體會失敗  
**問題：** 如果您在安裝 SQL Server 容錯移轉叢集執行個體期間指定不正確的 IP 位址，安裝就會失敗。 解除安裝失敗的執行個體之後，如果您嘗試使用相同的執行個體名稱和正確的 IP 位址來重新安裝 SQL Server 容錯移轉叢集執行個體，安裝仍會失敗。 發生失敗的原因是先前的安裝遺留了重複的資源群組。  
  
**因應措施** ：若要解決此問題，請在重新安裝期間使用不同的執行個體名稱，或在重新安裝之前手動刪除資源群組。 如需詳細資訊，請參閱 [在 SQL Server 容錯移轉叢集中加入或移除節點](http://msdn.microsoft.com/library/ms191545)。  
  
### <a name="12-choose-the-correct-file-to-download-and-install"></a>1.2 選擇要下載並安裝的正確檔案  
您可以使用下表來決定要下載並安裝的檔案。 在安裝 Service Pack 之前，請先確認您擁有正確的系統需求。 系統需求會列在資料表中所連結的下載頁面。  
  
|如果您目前安裝的版本是...|而您要...|請下載並安裝...|  
|-------------------------------------------|----------------------|---------------------------|  
|**32 位元安裝：**|||  
|任何 SQL Server 2012 版本的 32 位元版本|升級為 32 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|32 位元版本的 SQL Server 2012 RTM Express|升級為 32 位元版本的 SQL Server 2012 Express SP1|SQLServer2012SP1-KB2674319-x86-CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|32 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 32 位元版本的 SQL Server 2012 SP1|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|32 位元版本的 SQL Server 2012 Management Studio Express|升級為 32 位元版本的 SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|32 位元版本的任何 SQL Server 2012 版本， **以及** 32 位元版本的用戶端和管理能力工具 (包括 SQL Server 2012 RTM Management Studio)|將所有產品升級為 32 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|[Microsoft SQL Server 2012 RTM 功能套件](http://www.microsoft.com/download/details.aspx?id=16978)中一個或多個 32 位元版本的工具|將工具升級為 32 位元版本的 Microsoft SQL Server 2012 SP1 功能套件|[Microsoft SQL Server 2012 SP1 功能套件](http://go.microsoft.com/fwlink/p/?LinkID=268266)中的一個或多個檔案|  
|無 32 位元的 SQL Server 2012 安裝|安裝包括 SP1 的 32 位元 Server 2012 (已預先安裝 SP1 的新執行個體)|SQLServer2012SP1-FullSlipstream-x86-CHT.exe **以及** SQLServer2012SP1-FullSlipstream-x86-CHT.box 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|無 32 位元的 SQL Server 2012 Management Studio 安裝|安裝包括 SP1 的 32 位元 SQL Server 2012 Management Studio|SQLManagementStudio_x86_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|無 32 位元版本的 SQL Server 2012 RTM Express|安裝包括 SP1 的 32 位元 SQL Server 2012 Express|SQLEXPR32_x86_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|32 位元的 **SQL Server 2008** 或 **SQL Server 2008 R2**安裝|**就地升級** 為包括 SP1 的 32 位元 SQL Server 2012|SQLServer2012SP1-FullSlipstream-x86-CHT.exe **以及** SQLServer2012SP1-FullSlipstream-x86-CHT.box 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|**64 位元安裝：**|||  
|任何 SQL Server 2012 版本的 64 位元版本|升級為 64 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64 位元版本的 SQL Server 2012 RTM Express|升級為 64 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64 位元版本的 SQL Server 2012 用戶端和管理能力工具 (包括 SQL Server 2012 Management Studio)|將用戶端和管理能力工具升級為 64 位元版本的 SQL Server 2012 SP1|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64 位元版本的 SQL Server 2012 Management Studio Express|升級為 64 位元版本的 SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64 位元版本的任何 SQL Server 2012 版本， **以及** 64 位元版本的用戶端和管理能力工具 (包括 SQL Server 2012 RTM Management Studio)|將所有產品升級為 64 位元版本的 SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|[Microsoft SQL Server 2012 RTM 功能套件](http://www.microsoft.com/download/en/details.aspx?id=16978)中一個或多個 64 位元版本的工具|將工具升級為 64 位元版本的 Microsoft SQL Server 2012 SP1 功能套件|[Microsoft SQL Server 2012 SP1 功能套件](http://go.microsoft.com/fwlink/p/?LinkID=268266)中的一個或多個檔案|  
|無 64 位元的 SQL Server 2012 安裝|安裝包括 SP1 的 64 位元 Server 2012 (已預先安裝 SP1 的新執行個體)|SQLServer2012SP1-FullSlipstream-x64-CHT.exe， **以及** SQLServer2012SP1-FullSlipstream-x64-CHT.box 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|無 64 位元的 SQL Server 2012 Management Studio 安裝|安裝 64 位元的 SQL Server 2012 Management Studio，包括 SP1|SQLManagementStudio_x64_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|無 64 位元版本的 SQL Server 2012 RTM Express|安裝 64 位元的 SQL Server 2012 Express，包括 SP1|SQLEXPR_x64_CHT.exe 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64 位元的 **SQL Server 2008** 或 **SQL Server 2008 R2**安裝|**就地升級** 為包括 SP1 的 64 位元 SQL Server 2012|SQLServer2012SP1-FullSlipstream-x64-CHT.exe， **以及** SQLServer2012SP1-FullSlipstream-x64-CHT.box 的下載位置在 [這裡](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../release-notes/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[內容](#bkmk_top)  
  
## <a name="bkmk_AS"></a>2.0 Analysis Services 和 PowerPivot  
  
### <a name="21-powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>2.1 PowerPivot 組態工具不會建立 PowerPivot 圖庫  
**問題** ：PowerPivot 組態工具會佈建小組網站，因此不會建立 PowerPivot 圖庫。  
  
**因應措施** ：建立新的應用程式 (程式庫)。  
  
1.  確認網站集合功能 **[網站集合的 PowerPivot 功能整合]** 為 [使用中]。  
  
2.  在現有網站的 [網站內容] **** 頁面中，按一下 [加入應用程式] ****。  
  
3.  按一下 [PowerPivot 圖庫] ****。  
  
### <a name="22-to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>2.2 若要使用 PowerPivot for Excel 搭配 Excel 2013，您必須使用與 Excel 一起安裝的增益集  
**問題** ：在 Office 2010 中，PowerPivot for Excel 是可從 [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx)下載的獨立增益集。 或者，您也可以從 [Microsoft 下載中心](http://www.microsoft.com/download/details.aspx?id=29074)下載此增益集。 請注意，目前可供下載的 PowerPivot 增益集有兩種版本：第一種版本隨附於 SQL Server 2008 R2，而另一種版本則隨附於 SQL Server 2012。 不過，如果是 Office 2013，PowerPivot for Excel 隨附於 Office，而且會在您安裝 Excel 時一併安裝。 雖然 SQL Server 2008 R2 和 SQL Server 2012 版本的 PowerPivot for Excel 2010 與 Excel 2013 不相容，不過如果您想要讓 Excel 2010 與 Excel 2013 並存執行，仍然可以在用戶端電腦上安裝 PowerPivot for Excel 2010。 換言之，這兩種 Excel 版本可以共存，因此對應的 PowerPivot 增益集也可以。  
  
**因應措施**：若要使用 PowerPivot for Excel 2013，您必須啟用 COM 增益集。 在 Excel 2013 中，選取 [檔案]**** | [選項]**** | [增益集]****。 在 [管理]**** 下拉式方塊中，選取 [COM 增益集]****，然後按一下 [執行]****。 在 [COM 增益集] ****中，選取 [Microsoft Office PowerPivot for Excel 2013] **** ，然後按一下 [確定] ****。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../release-notes/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[內容](#bkmk_top)  
  
## <a name="bkmk_RS"></a>3.0 Reporting Services  
  
### <a name="31-install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>3.1 在安裝 Reporting Services 之前，安裝並設定 SharePoint Server 2013  
**問題** ：安裝 SQL Server Reporting Services (SSRS) **之前** ，請先完成下列需求。  
  
1.  執行 SharePoint 2013 產品準備工具。  
  
2.  安裝 SharePoint Server 2013。  
  
3.  執行 SharePoint 2013 產品設定精靈，或完成對等的設定步驟來設定 SharePoint 伺服器陣列。  
  
**因應措施**  ：如果您在設定 SharePoint 伺服器陣列之前已安裝 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式，必要的因應措施就會取決於其他已安裝的元件而定。  
  
### <a name="32-power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>3.2 SharePoint Server 2013 中的 Power View 需要使用 Microsoft.AnalysisServices.SPClient.dll  
**問題**：[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 不會安裝必要的元件：**Microsoft.AnalysisServices.SPClient.dll**。 如果您在 SharePoint 模式下安裝 SharePoint Server 2013 Preview 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，但並未下載及安裝 PowerPivot for SharePoint 2013 安裝程式套件 **spPowerPivot.msi**，則 Power View 將無法運作且會出現下列徵兆。  
  
**徵兆** ：當您嘗試建立 Power View 報表時，將會看見類似下面的錯誤訊息：  
  
-   「無法與資料來源建立連接...」  
  
內部錯誤詳細資料將會包含類似下面的訊息：  
  
-   「連接字串屬性 'User Identity' 不支援值 'SharePoint Principal'。」  
  
**因應措施** ：在 SharePoint Server 2013 上安裝 PowerPivot for SharePoint 2013 安裝程式套件 (**spPowerPivot.msi**)。 此安裝程式套件屬於 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 功能套件的一部分。 您可以從 [!INCLUDE[msCoName](../includes/msconame-md.md)] 下載中心的 [SQL Server 2012 SP1 功能套件](http://go.microsoft.com/fwlink/p/?LinkID=268266)下載此功能套件。  
  
### <a name="33-power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>3.3 執行排程的資料重新整理之後，PowerPivot 活頁簿中的 Power View 工作表遭到刪除  
**問題**：在 PowerPivot for SharePoint 增益集中，如果對含有 Power View 的活頁簿使用 [排定的資料重新整理] **** ，將會刪除所有 Power View 工作表。  
  
**因應措施**：若要搭配含有 Power View 的活頁簿使用 **Scheduled Data Refresh** ，請建立正好是資料模型的 PowerPivot 活頁簿。 建立含有 Excel 工作表及 Power View 工作表的不同活頁簿，讓這個活頁簿透過資料模型連結至 PowerPivot 活頁簿。 只要針對含有資料模型的 PowerPivot 活頁簿來排程資料重新整理即可。  
  
## <a name="bkmk_DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>4.1 不正確的 SQL Server 2012 版本提供了 DQS  
**問題** ：在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM 版本中，Enterprise、Business Intelligence 和 Developer Edition 以外的 SQL Server 版本都有提供 Data Quality Services (DQS) 功能。 安裝 SQL Server 2012 SP1 之後，除了 Enterprise、Business Intelligence 和 Developer Edition 以外，所有版本都不再提供 DQS。  
  
**因應措施**：如果您在不支援的版本中使用 DQS，請升級為支援的版本，或從您的應用程式中移除這項功能的相依性。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../release-notes/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[內容](#bkmk_top)  
  
## <a name="bkmk_Express"></a>5.0 SQL Server Express  
  
### <a name="51-full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>5.1 SQL Server 2012 Express SP1 提供了完整版本的 SQL Server Management Studio  
SQL Server 2012 Express Service Pack 1 (SP1) 版本包含完整版本的 SQL Server 2012 Management Studio (先前只有 SQL Server 2012 DVD 才提供) 而非 SQL Server 2012 Management Studio Express。 若要下載和安裝 SQL Server 2012 Express SP1，請參閱 [SQL Server 2012 Express Service Pack 1](http://go.microsoft.com/fwlink/p/?linkid=267905)。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../release-notes/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[內容](#bkmk_top)  
  
## <a name="bkmk_CDC"></a>6.0 Attunity Oracle 異動資料擷取 (CDC) 服務和設計工具  
  
### <a name="61-upgrading-the-cdc-service-and-designer"></a>6.1 升級 CDC 服務和設計工具  
**問題** ：在您安裝 SQL Server 2012 SP1 時，如果電腦上已安裝 Attunity Oracle Change Data Capture (CDC) 設計工具和 Change Data Capture (CDC) 服務，這些元件不會透過安裝 SP1 而升級。  
  
**因應措施** ：若要將 CDC 元件升級為最新版本：  
  
1.  從 [SQL Server 2012 SP1 功能套件下載頁面](http://go.microsoft.com/fwlink/p/?LinkID=268266)下載 Attunity Oracle Change Data Capture (CDC) 服務的 .msi 檔案。  
  
2.  執行 .msi 檔案。  
  
![搭配 [回到頁首] 連結使用的箭號圖示](../release-notes/media/uparrow16x16.gif "搭配 [回到頁首] 連結使用的箭號圖示")[內容](#bkmk_top)  
  
## <a name="DACFx"></a>7.0 SQL Server 資料層應用程式架構 (DACFx)  
**就地升級支援**  
  
此版本的資料層應用程式架構 (DACFx) 支援從舊版就地升級，因此不需要在升級至此版本之前移除舊版 DACFx 安裝。 您可以在 [此處](https://msdn.microsoft.com/library/dn702988.aspx)尋找未來的 DACFx 版本。  
  
**支援選擇性 XML 索引**  
  
SQL Server 2012 SP1 加入對 [選擇性 XML 索引 (SXI)](http://msdn.microsoft.com/en-us/598ecdcd-084b-4032-81b2-eed6ae9f5d44)的支援，這個新的 SQL Server 功能會提供新的方式來建立提升效能及效率的 XML 資料行資料索引。  
  
DACFx 現在對所有的 DAC 案例及用戶端工具都支援 SXI 索引。 只有在 SSDT 的最新版本才支援 SXI。 SSDT RTM 和 2012 年 9 月版不支援 SXI。  
  
**支援原生 BCP 資料格式**  
  
先前在 DACPAC 及 BACPAC 封裝內部用來儲存資料表資料的資料格式為 JSON。 安裝此更新後，原生 BCP 就會是目前的資料保存格式。 這項變更可將提升的 SQL Server 資料類型精確度引入 DACFx，包括支援 SQL_Variant 類型，以及增強大規模資料庫的資料部署效能。  
  
**在整個套件建立/部署中保留 CHECK 條件約束狀態**  
  
DACFx 先前並不能將資料表上定義的檢查條件約束狀態 (WITH CHECK/NOCHECK) 保留在資料庫結構描述中，也無法將此資訊儲存在 DACPAC 內部。 當有違反檢查條件約束的資料表資料存在時，此行為可能會在封裝部署上產生潛在問題。 安裝此更新後，DACFx 現在從資料庫中擷取檢查條件約束的目前狀態時，就會將此狀態儲存在 DACPAC 中，並於部署封裝時適當還原該狀態。  
  
**SqlPackage.exe (DACFx 命令列工具) 的更新**  
  
-   擷取包含資料的 DACPAC – 從即時 SQL Server 或 Windows Azure SQL 資料庫建立資料庫快照集檔案 (.dacpac)，不僅包含資料庫結構描述，還有使用者資料表中的資料。 您可以使用 SqlPackage.exe 發佈動作將這些封裝發行至新的或現有 SQL Server 或 Windows Azure SQL 資料庫。 封裝中的資料將會取代目標資料庫中的現有資料。  
  
-   匯出 BACPAC - 建立即時 SQL Server 或 Windows Azure SQL 資料庫邏輯的備份檔案 (.bacpac)，內含資料庫結構描述，以及可用於將資料庫從內部部署 SQL Server 移轉至 Windows Azure SQL 資料庫的使用者資料。 您可以匯出與 Azure 相容的資料庫，稍後再於支援的 SQL Server 版本之間將其匯入。  
  
-   匯入 BACPAC – 匯入 .bacpac 檔案以全新建立或填入空的 SQL Server 或 Windows Azure SQL 資料庫。  
  
MSDN 上的完整 SqlPackage.exe 文件可以在 [此處](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx)找到。  
  
**套件相容性**  
  
此版本導入數個適用於 DAC 封裝的向前相容性。  
  
-   此版本所建立未包含 SXI 元素或資料表資料的 DAC 封裝可供舊版 DACFx (SQL Server 2012 RTM、SQL Server 2012 CU1 和 DACFx 2012 年 9 月版) 取用。  
  
-   此版本可以使用舊版 DACFx 建立的所有 DAC 封裝。  
  
## <a name="bkmk_known_issues_fixed"></a>8.0 此 Service Pack 中修正的已知問題  
如需這個 Service Pack 所修正之錯誤和已知問題的完整清單，請參閱 [這份知識庫文件](http://support.microsoft.com/kb/2674319)。  
  
[目錄](#bkmk_top)  
  
## <a name="see-also"></a>另請參閱  
[如何判斷 SQL Server 的版本](http://support.microsoft.com/kb/321185)  
[SQL Server 2014 各版本所支援的功能](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  
  

