---
title: 安裝、 解除安裝與報表產生器支援 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Report Builder
ms.assetid: 2c9a5814-17bf-4947-8fb3-6269e7caa416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d35f6c7d77a43fe35ba78a88824309ffd72a5a44
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454604"
---
# <a name="install-uninstall-and-report-builder-support"></a>安裝、解除安裝和報表產生器支援
  報表產生器是一項報表撰寫工具，可用來建立、更新和共用報表、報表組件和共用資料集。 報表產生器有提供兩個版本：單機版和 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]。 單機版是由您或系統管理員安裝在電腦上。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本是隨 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 自動安裝，而且從報表管理員或與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]整合的 SharePoint 網站下載到電腦。  
  
 單機版的報表產生器不會與 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]一起安裝， 您必須從 [Microsoft® SQL Server® 2012 報表產生器](https://go.microsoft.com/fwlink/?LinkId=401502)分別下載它們並加以安裝。  
  
> [!NOTE]  
>  報表產生器無法安裝在 Itanium 型電腦上。 這同樣適用於 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 和單機版本的報表產生器。  
  
 系統管理員通常會安裝及設定 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]、授與使用 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本報表產生器的權限，以及管理儲存到報表伺服器之報表、報表組件和共用資料集的資料夾和權限。 如需詳細資訊[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]管理，請參閱 < [Reporting Services 報表伺服器&#40;原生模式&#41;](report-server/reporting-services-report-server-native-mode.md)中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][線上叢書 》](https://go.microsoft.com/fwlink/?LinkId=154888) msdn.microsoft.com 上。  
  
##  <a name="Installing"></a> 安裝報表產生器  
 報表產生器有單機版和 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本。 您或系統管理員可在電腦上下載及安裝單機版本，而 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本則會隨著 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]一起安裝。 您也可以從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?LinkID=186083)下載報表產生器。  
  
> [!NOTE]  
>  報表產生器無法安裝在 Itanium 64 型電腦上。 這同樣適用於 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 和單機版本的報表產生器。  
  
 安裝任一版本的報表產生器之前，請先確認系統需求並安裝任何必要條件。  
  
### <a name="system-requirements"></a>系統需求  
 報表產生器會要求本機電腦上必須已經安裝 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 3.5 版。 當您安裝報表產生器時，如果 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 沒有安裝在本機電腦上，系統就會提示您進行安裝，然後才能繼續和完成安裝。  
  
 .NET Framework 3.5 是免費的。 您可以從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?LinkID=110520)下載 .NET Framework 3.5。  
  
 您可以將報表產生器安裝在任何支援 [!INCLUDE[msCoName](../includes/msconame-md.md)] 3.5 的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Windows 作業系統上。 例如，您可以將報表產生器安裝在 Windows Vista 或 Windows 7 上。  
  
 建議執行報表產生器的電腦應該具有 512 MB 的 RAM。 不過，根據您所執行之報表的複雜度，可能需要更少或更多 RAM。  
  
### <a name="installing-the-stand-alone-version-of-report-builder-directly-on-your-computer"></a>直接在電腦上安裝單機版本的報表產生器  
 您可以從下載網址 ( [Microsoft 下載中心](https://go.microsoft.com/fwlink/?LinkID=186083)) 安裝報表產生器，或是由系統管理員將 ReportBuilder3.msi 檔 (報表產生器的 Windows 安裝程式套件) 放在可下載的共用上。  
  
 您也可以執行命令列安裝並加入一些選項，例如進行無訊息安裝和寫入安裝的記錄檔。 執行此 .msi 檔之 Windows Installer 的文件集會提供可用選項的相關資訊。  
  
 如需詳細資訊，請參閱 <<c0> [ 安裝獨立版本的報表產生器&#40;報表產生器&#41;](install-windows/install-report-builder.md)。</c0>  
  
 系統管理員也可以使用 Microsoft Systems Manager Server (SMS) 等軟體，將此程式發送至您的電腦。 若要了解如何使用特定軟體來安裝報表產生器，請參閱軟體的文件集。   
  
### <a name="installing-the-clickonce-version-of-report-builder-on-your-computer"></a>在電腦上安裝報表產生器的 ClickOnce 版本  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本的報表產生器會隨著 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]一起安裝。 這會由 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]的原生和 SharePoint 整合安裝進行安裝。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 是一種 Microsoft 技術，用於部署 Windows 應用程式。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 可讓使用者按一下網頁上的連結，即可安裝及執行 Windows 應用程式，例如報表產生器。 如需有關部署[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]應用程式、 套用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]應用程式的安全性或執行[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)][網際網路] 區域中的應用程式，請參閱 [ClickOnce 部署的 Windows Forms 應用程式] 中的 < 安全性Windows Forms 概觀 > 或 「 受信任的應用程式部署概觀 > 文章[!INCLUDE[msCoName](../includes/msconame-md.md)]開發人員網路網站，網址[ https://developer.microsoft.com/ ](https://developer.microsoft.com/)。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本的報表產生器位於報表伺服器上，當您按一下報表管理員中的 **[報表產生器]** 按鈕，或是在 SharePoint 文件庫中按一下 **[新增文件]** 功能表上的 **[報表產生器報表]** 選項時，就會安裝在您的電腦上。  
  
> [!NOTE]  
>  如果 **[新增文件]** 功能表未列出 **[報表產生器報表]** 、 **[報表產生器模型]** 和 **[報表資料來源]** 選項，則必須將其內容類型加入至 SharePoint 文件庫。   
  
 您可以從報表管理員或 SharePoint 文件庫開啟報表產生器。 如需有關如何開啟報表產生器的詳細資訊，請參閱 <<c0> [ 啟動報表產生器&#40;報表產生器&#41;](report-builder/start-report-builder.md)。</c0>  
  
### <a name="report-builder-languages"></a>報表產生器語言  
 除了英文版以外，報表產生器還提供了 21 種語言版本。 當您下載報表產生器的單機版時，請選取想要安裝的語言版本。 您必須針對想要使用的每種語言版本，重複進行下載步驟。  
  
 如果是 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本，當您安裝 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]時，所有語言版本都會安裝在報表伺服器上。 使用者電腦的文化特性會決定安裝在電腦的語言版本。 如果文化特性與可用的報表產生器語言不相符，則會安裝英文版本。  
  
 下表具有可用語言版本的相關資訊。  
  
|LCID|語言|Culture|  
|----------|--------------|-------------|  
|1028|中文 (繁體)|zh-TW|  
|1029|捷克文|cs-CZ|  
|1030|丹麥文|da-DK|  
|1031|德文|de-DE|  
|1032|希臘文|el-GR|  
|1033|英文|zh-TW|  
|1035|芬蘭文|fi-FI|  
|1036|法文|fr-FR|  
|1038|匈牙利文|hu-HU|  
|1040|義大利文|it-IT|  
|1041|日文|ja-JP|  
|1042|韓文|ko-KR|  
|1043|荷蘭文|nl-NL|  
|1044|挪威文 (巴克摩)|nb-NO|  
|1045|波蘭文|pl-PLl|  
|1046|葡萄牙文 (巴西)|pt-BR|  
|1049|俄文|ru-RU|  
|1053|瑞典文|sv-SE|  
|1055|土耳其文|tr-TR|  
|2052|中文 (簡體)|zh-CN|  
|2070|葡萄牙文 (葡萄牙)|pt-PT|  
|3082|西班牙文 (西班牙)|es-ES|  
  
  
##  <a name="Uninstalling"></a> 解除安裝報表產生器  
 您可以從控制台或命令列解除安裝單機版本的報表產生器。 這只適用於單機版本的報表產生器。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 版本的報表產生器不能個別解除安裝， 它必須隨 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]一起安裝和解除安裝。  
  
 如需詳細資訊，請參閱 <<c0> [ 解除安裝獨立版本的報表產生器&#40;報表產生器&#41;](install-windows/uninstall-report-builder.md)。</c0>  
  
  
##  <a name="Supporting"></a> 支援報表產生器  
 為支援報表作者，系統管理員必須負責管理報表伺服器上的資料夾、報表以及報表相關項目、授與報表伺服器上資源的權限，以及設定報表伺服器以供存取。  
  
### <a name="folders-reports-and-report-related-items"></a>資料夾、報表和報表相關項目  
 下列資料夾、報表和報表相關項目是在報表伺服器上管理的：  
  
-   儲存報表、共用資料來源、模型等的資料夾。  
  
-   [我的報表]，這是儲存您的報表和報表相關項目的私人資料夾。  
  
-   共用資料來源，可讓報表作者使用儲存在報表外部的資料來源。  
  
-   共用資料集，可將現成可用的查詢資料提供給多個使用者的多份報表。  
  
-   如資料表和圖表等報表組件，可讓使用者在共同作業環境下加強和重複使用其他人建立的報表組件。  
  
-   報表模型，可讓報表更簡單方便從複雜的資料來源取得資料。  
  
-   如背景影像和標誌等影像，可用於多份報表並儲存在報表外部以便維護。  
  
 如需詳細資訊，請參閱 <<c0> [ 報表伺服器內容管理&#40;SSRS 原生模式&#41;](report-server/report-server-content-management-ssrs-native-mode.md)中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][線上叢書 》](https://go.microsoft.com/fwlink/?LinkId=154888) msdn.microsoft.com 上。</c0>  
  
### <a name="permissions"></a>Permissions  
 系統管理員會授與報表伺服器的權限。 報表產生器使用者需要報表伺服器的權限，才能存取報表伺服器的內容和功能。 例如，您可能想要使用儲存在報表伺服器上的報表組件、更新報表並再儲存到報表伺服器，以及在報表管理員中執行報表。 授與權限的高低會視您的需求和執行的工作而定。 例如，為只需開啟共用報表的使用者授與較低的權限 (相較於需要修改共用報表的使用者)。  
  
 當 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 是以原生模式安裝時，系統管理員可以：  
  
-   啟用 [我的報表] 功能，為您提供私人資料夾來建立和儲存您自己的報表。  
  
-   在公用資料夾上使用 [報表產生器] 角色，讓您可以開啟共用報表的副本，然後將修改過的版本儲存到私人資料夾。  
  
-   使用 [發行者] 角色，讓您管理公用資料夾中的報表和共用資料來源。 此角色會授與較有經驗的使用者。  
  
 當 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 是以 SharePoint 整合模式安裝時，系統管理員可以：  
  
-   使用依預設授與「訪客」群組的「讀取」權限等級，讓您可以開啟公用資料夾中報表的副本，然後將修改過的報表版本儲存到私人資料夾或電腦。  
  
-   使用依預設授與「成員」群組的「參與」權限等級，讓您管理公用資料夾中的報表和共用資料來源。 此權限等級會授與較有經驗的使用者。  
  
 如需有關權限和建立及使用角色的一般資訊，請參閱 msdn.microsoft.com 上《 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 線上叢書 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [》中的＜](https://go.microsoft.com/fwlink/?LinkId=154888) ＞。  
  
### <a name="configuration-of-report-server"></a>設定報表伺服器  
 當您在報表產生器中撰寫報表，並連接到安裝在 Windows Vista、Windows Server 2008 或 Windows 7 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，如果您嘗試存取報表伺服器來開啟或儲存報表，可能會遇到拒絕存取的錯誤。 發生這個情況是因為 Windows Vista、Windows Server 2008 和 Windows 7 中的安全性功能「使用者帳戶控制」(UAC) 會透過移除管理員權限來限制存取應用程式時過度使用更高的權限。  
  
 不過，透過額外的設定，您可以將報表伺服器提供給報表產生器的使用者使用。 您可以將 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] URL 加入至信任的網站。 根據預設，Windows Vista、Windows Server 2008 和 Windows 7 上的 Internet Explorer 7.0 或更新版本會在「受保護模式」下執行。 「受保護模式」功能會封鎖瀏覽器要求，使其無法到達相同電腦上執行的高層級處理序。 您可以為報表伺服器應用程式停用受保護模式，只要將這些應用程式加入為信任的網站即可。 您必須具有管理員權限才能進行此變更。  
  
 如需設定的詳細資訊[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]，請參閱 < [Reporting Services 組態管理員&#40;del&#41; ](https://docs.microsoft.com/sql/sql-server/install/reporting-services-configuration-manager-native-mode)中[Reporting Services 文件](https://go.microsoft.com/fwlink/?linkid=121312)msdn.microsoft.com 上。  
  
  
##  <a name="SampleDatabases"></a> SQL Server 範例資料庫  
 Adventure Works 系列範例資料庫提供了一些資料，可讓您用來了解報表撰寫和撰寫範例報表。  
  
 資料庫有下列版本：  
  
-   Adventure Works OLTP 資料庫支援一家虛構自行車製造商 (Adventure Works Cycles) 的標準線上交易處理案例。 案例包括製造、銷售、採購、產品管理、連絡人管理以及人力資源。  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫示範如何建立資料倉儲。  
  
-   [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 專案可用來為商業智慧案例建立 AS 資料庫。  
  
 這些範例資料庫未隨附於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ，而且也不會隨您安裝 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 或單機版本報表產生器一起安裝。 不過，您可以從 [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843)下載範例資料庫。 所有版本的範例資料庫都會一起下載。 您也可以下載隨 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]發行的舊版資料庫。  
  
 如需有關下載和安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 範例資料庫的必要條件和指示，請參閱 CodePlex 上的＜ [SQL Server 2008 範例資料庫的安裝必要條件](https://go.microsoft.com/fwlink/?LinkId=166648) ＞和＜ [安裝範例資料庫](https://go.microsoft.com/fwlink/?LinkId=166649) ＞。  
  
  
##  <a name="HowTo"></a> 如何主題  
 本節列出如何安裝和解除安裝報表產生器的程序。  
  
 [安裝單機版本報表產生器的&#40;報表產生器&#41;](install-windows/install-report-builder.md)  
  
 [解除安裝單機版本報表產生器的&#40;報表產生器&#41;](install-windows/uninstall-report-builder.md)  
  
 [啟動報表產生器&#40;報表產生器&#41;](report-builder/start-report-builder.md)  
  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中的報表產生器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
