---
title: 在 SharePoint 伺服器上安裝 Analysis Services OLE DB Provider |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2c62daf9-1f2d-4508-a497-af62360ee859
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f8dcec71f8b9c90df9f30aa5bfb972fef28fbcd7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74200441"
---
# <a name="install-the-analysis-services-ole-db-provider-on-sharepoint-servers"></a>在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者
  Microsoft OLE DB Provider for Analysis Services (MSOLAP) 是用戶端應用程式用來與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料互動的介面。 在包含 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]的 SharePoint 環境中，提供者會處理 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的連接要求。  
  
 資料提供者內含在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝套件 (spPowerPivot.msi) 中，但是可能需要手動安裝。 在兩種情況下您可能必須在 SharePoint 伺服器上手動安裝用戶端程式庫或資料提供者。  
  
-   **啟用回溯相容性**。 
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 活頁簿會在其連接字串中指定 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的 Analysis Services OLE DB 提供者。 如此一來，此提供者版本必須存在電腦上，要求才能成功。  
  
-   **在專用 Excel Services 實例上啟用資料存取**。 如果您的 SharePoint 伺服器陣列在同樣沒有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]的伺服器上包含 Excel Services，則使用 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 安裝套件來安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 版的提供者和其他用戶端連接性元件。  
  
    > [!NOTE]  
    >  這些案例不會互斥。 若您在包含執行 Excel Services 但沒有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 執行個體之應用程式伺服器的伺服器陣列上裝載多個活頁簿版本，則需要在每一部 Excel Services 電腦上同時安裝舊版和新版資料提供者。  
  
  
##  <a name="bkmk_vers"></a>支援 PowerPivot 資料存取的 OLE DB 提供者版本  
 SharePoint 伺服器陣列可能包含多個 Analysis Services OLE DB 提供者版本，包括不支援 PowerPivot 資料存取的舊版。  
  
 根據預設，SharePoint 2010 會安裝提供者的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本。 此版本雖然識別為 MSOLAP.4 (與用於 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]的版本號碼相同)，但是不適用於 PowerPivot 資料存取。 您必須具有 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版的提供者，才能成功連接。  
  
 OLE DB 提供者在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之後的版本中，包含適用於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料結構的傳輸和連接支援。 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿會使用這個提供者的新版，向伺服器陣列中的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器要求查詢處理。 若要取得已更新的版本，可以透過 [SQL Server 功能套件] 頁面下載並安裝。  
  
 下表描述有效的版本：  
  
|產品版本|檔案版本|有效：|  
|---------------------|------------------|----------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|檔案系統中的 MSOLAP100.dll<br /><br /> Excel 連接字串中的 MSOLAP.4<br /><br /> 檔案版本詳細資料中的 10.50.1600 或更新版本|使用以 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的 PowerPivot for Excel 建立的資料模型。|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|檔案系統中的 MSOLAP110.dll<br /><br /> Excel 連接字串中的 MSOLAP.5<br /><br /> 檔案版本詳細資料中的 11.0.0000 或更新版本|用於以 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 建立的資料模型。|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|檔案系統中的 MSOLAP120.dll<br /><br /> 檔案版本詳細資料中的 12.0.20000 或更新版本|用於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型之外的資料模型。|  
  
  
##  <a name="bkmk_why"></a>為何需要安裝 OLE DB 提供者  
 下列兩種情況需要在伺服器陣列中的伺服器上手動安裝 OLE DB 提供者。  
  
 **最常見的情況**是當您在伺服器陣列的文件庫[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]中儲存舊版和較新版本的活頁簿時。 如果組織的分析師使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel，並將活頁簿儲存至 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝，則舊版活頁簿將無法運作。 其連接字串會參考較舊版本的提供者，除非您安裝它，否則不會在伺服器上。 同時安裝兩個版本，即可存取在新舊版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中建立之 PowerPivot 活頁簿的資料。 
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安裝程式不會安裝提供者的 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本，因此若要使用舊版活頁簿，您必須手動安裝該版本。  
  
 **第二個案例**是當您的伺服器在執行 Excel Services 的 SharePoint 伺服器陣列中，但[!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]卻不是。 在此情況下，執行 Excel Services 的應用程式伺服器必須手動更新，才能使用新版的提供者。 連接至 PowerPivot for SharePoint 執行個體需要此元件。 如果 Excel Services 正在使用舊版的提供者，則連接要求將會失敗。 請注意，必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式或 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝套件 (spPowerPivot.msi) 來安裝提供者，以確保安裝支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 所需的所有元件。  
  
  
##  <a name="bkmk_sql11"></a>使用 SQL Server 安裝程式，在 Excel Services 伺服器上安裝 SQL Server 2012 OLE DB 提供者  
 使用下列指示，將 OLE DB 提供者和其他用戶端連接性元件加入至未安裝這些元件的 SharePoint 伺服器，例如執行 Excel Services 但未在相同硬體上安裝 PowerPivot for SharePoint 的應用程式伺服器。  
  
 使用以下指示來安裝目前的 Analysis Services OLE DB 提供者，並將 **Microsoft.AnalysisServices.Xmla.dll** 加入至全域組件。  
  
#### <a name="run-sql-server-setup-and-install-the-client-connectivity-tools"></a>執行 SQL Server 安裝程式及安裝用戶端連接工具  
  
1.  在主控 Excel Services 的應用程式伺服器上，執行 SQL Server 安裝程式。  
  
2.  在 [安裝] 頁面上，選擇 **[新增 SQL Server 獨立安裝或將功能加入至現有安裝]**。  
  
3.  在 [安裝類型] 頁面上，選擇 **[執行 SQL Server 2012 的新安裝]**。  
  
4.  在 [安裝程式角色] 頁面上，選擇 **[SQL Server 功能安裝]**。  
  
5.  在 **[特徵選取]** 頁面上，按一下 **[用戶端工具連接性]**。 此選項會安裝 **Microsoft.AnalysisServices.Xmla.dll**。  
  
     請勿選取其他任何功能。  
  
6.  按 **[下一步]** 完成精靈，然後按一下 **[安裝]** 執行安裝程式。  
  
7.  如果您有其他伺服器執行 Excel Services 但是並未在相同的伺服器上安裝 PowerPivot for SharePoint，請重複上述步驟。  
  
#### <a name="verify-msolap5-is-a-trusted-provider"></a>確認 MSOLAP.5 是受信任的提供者  
  
1.  在 [管理中心]，按一下 **[管理服務應用程式]**，然後按一下 Excel Services 服務應用程式。  
  
2.  按一下 **[信任的資料提供者]**。  
  
3.  確認 MSOLAP.5 出現在清單中。 根據您設定 PowerPivot for SharePoint 的方式，MSOLAP.5 可能已經是受信任的提供者。 如果您使用 PowerPivot 組態工具，但之後將此動作排除在工作清單之外，則 Excel Services 將不會信任 MSOLAP.5，且現在必須手動加入 MSOLAP.5。  
  
4.  如果未列出 MSOLAP，請按一下 **[新增信任的資料提供者]**。  
  
5.  在 [提供者識別碼] 中，輸入 `MSOLAP.5`。  
  
6.  對於 [提供者類型]，請確認已選取 OLE DB。  
  
7.  在 [提供者描述] 中，輸入 **Microsoft OLE DB Provider for OLAP Services 11.0**。  
  
#### <a name="verify-installation"></a>確認安裝  
  
1.  移至 Program files\Microsoft Analysis Services\AS OLEDB\110。  
  
2.  以滑鼠右鍵按一下 msolap110.dll，然後選取 **[內容]**。  
  
3.  按一下 [詳細資料]****。  
  
4.  檢視檔案版本資訊。 版本應包含11.00。\<buildnumber>。  
  
5.  在 Windows\assembly 資料夾中，確認已列出 Microsoft.AnalysisServices.Xmla.dll 版本 11.0.0.0。  
  
  
##  <a name="bkmk_install2012_from_sppowerpivot_msi"></a>使用 PowerPivot for SharePoint 安裝套件（Sppowerpivot.msi .msi）來安裝 SQL Server 2012 OLE DB 提供者  
 使用 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 安裝套件 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] (spPowerPivot.msi) **來將**OLE DB 提供者安裝於 Excel Services 伺服器上。  
  
#### <a name="download-the-msolap5-provider-from-the-includesssql11sp1includessssql11sp1-mdmd-feature-pack"></a>從 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 功能套件下載 MSOLAP.5 提供者。  
  
1.  瀏覽至 [Microsoft® SQL Server® 2012 SP1 功能套件](https://www.microsoft.com/download/details.aspx?id=35580)  
  
2.  按一下 **[安裝指示]**。  
  
3.  請參閱 "Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1" 一節。 下載檔案並開始安裝。  
  
4.  在 **[特徵選取]** 頁面上，選取 **[Analysis Services OLE DB Provider for SQL Server]**。 取消選取其他元件，並完成安裝。 如需 Sppowerpivot.msi 的詳細資訊，請參閱[&#40;SharePoint 2013&#41;安裝或卸載 PowerPivot for SharePoint 增益集](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)。  
  
5.  向 SharePoint Excel Services 註冊 MSOLAP.5 當做信任的提供者。 如需詳細資訊，請參閱 [加入 MSOLAP.5 做為 Excel Services 中受信任的資料提供者](https://technet.microsoft.com/library/hh758436.aspx)。  
  
  
##  <a name="bkmk_kj"></a>安裝 SQL Server 2008 R2 OLE DB 提供者以裝載舊版活頁簿  
 請依照下列指示安裝 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的 MSOLAP.4 提供者，並且登錄 Microsoft.AnalysisServices.ChannelTransport.dll 檔。 ChannelTransport 是 Analysis Services OLE DB 提供者的子元件。 
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版的提供者會在使用 ChannelTransport 建立連接時讀取登錄。 登錄此檔案是一個後續安裝步驟，只需要針對 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 伺服器上 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 提供者處理的連接執行。  
  
#### <a name="step-1-download-and-install-the-client-library"></a>步驟 1：下載和安裝用戶端文件庫  
  
1.  在 [SQL Server 2008 R2 功能套件頁面](https://www.microsoft.com/download/details.aspx?id=16978)上，尋找 Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2008 R2。  
  
2.  下載 `SQLServer2008_ASOLEDB10.msi` 安裝程式的 x64 封裝。 雖然檔案名稱包含 SQLServer2008，但這是用於 SQL Server 2008 R2 版提供者的正確檔案。  
  
3.  在已安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]的電腦上，執行 .msi 安裝程式庫。  
  
4.  如果您的伺服器陣列中有其他只執行 Excel Services 的伺服器，但同一部伺服器上沒有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] ，請重複上述步驟，在 Excel Services 電腦上安裝 2008 R2 版的提供者。  
  
#### <a name="step-2-register-the-microsoftanalysisserviceschanneltransportdll-file"></a>步驟 2：登錄 Microsoft.AnalysisServices.ChannelTransport.dll 檔  
  
1.  使用 regasm.exe 公用程式登錄檔案。 如果您之前未執行 regasm，請將其父資料夾 C:\Windows\Microsoft.NET\Framework64\v4.0.30319\\新增至系統路徑變數。  
  
2.  使用管理員權限來開啟命令提示字元。  
  
3.  移至此資料夾 C:\Windows\assembly\GAC_MSIL\Microsoft.AnalysisServices.ChannelTransport\10.0.0.0__89845dcd8080cc91  
  
4.  輸入下列命令：`regasm microsoft.analysisservices.channeltransport.dll`  
  
5.  針對您手動安裝 2008 R2 版提供者的任何電腦重複上述步驟。  
  
#### <a name="verify-installation"></a>確認安裝  
  
1.  您現在應該能夠配量或篩選 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 活頁簿。 如果發生錯誤，請確認您使用的是 64 位元版的 regasm.exe 來登錄檔案。  
  
2.  此外，您可以檢查檔案版本。  
  
     移至 `C:\Program files\Microsoft Analysis Services\AS OLEDB\10`。 以滑鼠右鍵按一下 **msolap100.dll** ，然後選取 **[屬性]**。 按一下 [詳細資料]****。  
  
     檢視檔案版本資訊。 版本應包含10.50。\<buildnumber>。  
  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
