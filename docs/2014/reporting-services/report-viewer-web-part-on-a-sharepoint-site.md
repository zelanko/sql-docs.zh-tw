---
title: 在 SharePoint 網站上的報表檢視器 Web 組件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: b6341a73-172f-4632-a9e9-cc79fed3f36b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 80baae6ca56757c8723934102341352f34cb0709
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905229"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>SharePoint 網站上的報表檢視器 Web 組件
  報表檢視器網頁組件是由適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集所安裝的自訂網頁組件。 您可以在設定為以 SharePoint 整合模式執行的報表伺服器上，使用 Web 組件來檢視、導覽、列印與匯出報表。 報表檢視器網頁組件與 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器所處理的報表定義 (.rdl) 檔相關聯。 您無法使用該組件搭配以其他軟體產品建立的其他報表文件。  
  
 若要安裝此 Web 組件，您必須執行 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集的安裝程式。 您不應該獨立安裝或解除安裝此 Web 組件。 這是增益集的一部分，而且僅能透過增益集安裝套件安裝。 報表檢視器 Web 組件的檔案名稱為 ReportViewer.dwp。 它位於 Program Files\Common Files\Microsoft Shared\web server extensions\12\template\features\reportserver 資料夾中，而且不得移到其他資料夾中。  
  
 若要使用此 Web 組件，您必須已安裝並設定 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 增益集，並將報表伺服器設定為 SharePoint 整合。 此外，您也必須備妥要在檢視器中顯示的報表。 您只能開啟位於文件庫、文件庫資料夾及報表記錄中的報表，或是從文件庫 Web 組件連結至報表檢視器 Web 組件的報表。 您無法開啟在自訂清單中儲存成項目之附加檔案的報表。  
  
 您可以在報表檢視器網頁組件上設定屬性，以便控制工具列和檢視區域的外觀，以及將此網頁組件連結至特定報表。 報表檢視器會顯示您明確連結的目標報表，或顯示您所開啟的任何 .rdl 檔。  
  
 您無法將多個報表連結至單一的報表檢視器執行個體，但是如果您想要將報表群組在一起，您可以在單一頁面上，建立內嵌多個報表檢視器 Web 組件執行個體的儀表板或 Web 組件頁面。  
  
 Web 組件包含檢視區域、工具列、設定認證和參數的可摺疊區域以及屬性。 下列影像顯示具有 Company Sales 範例報表的 Web 組件，以及您可以從工具列選取的匯出選項。  
  
 ![報表檢視器網頁組件](media/rs-sharepointrvwebpart.gif "報表檢視器網頁組件")  
  
## <a name="web-part-components"></a>Web 組件元件  
 檢視區域會以 HTML 顯示報表。 根據此 Web 組件的設定方式，檢視區域可能會最大化以便以整頁模式顯示報表，或者可能會與相鄰的窗格和工具列共用可用空間。  
  
 工具列會提供頁面導覽、搜尋、顯示比例以及匯出功能，讓您可以用另一種應用程式格式檢視報表。 此外，它也會提供選用的列印功能，可提供 HTML 報表的分頁列印輸出以及變更頁面配置和邊界設定的功能。 **開啟報表產生器中，訂閱**，**匯出**，以及**列印**中所提供**動作**工具列上的功能表。 頁面導覽及顯示比例控制項直接位於工具列上。  
  
> [!NOTE]  
>  除非您有撰寫相關的程式碼，否則無法自訂工具列，但是您可以設定屬性，以便隱藏所有或部分控制項。  
  
### <a name="export-action-on-the-report-toolbar"></a>報表工具列上的匯出動作  
 **匯出**上**動作**功能表會顯示與報表伺服器上部署的轉譯延伸模組相關聯的應用程式格式。 若要決定特定格式的可用性，您可以在報表伺服器上加入或移除轉譯延伸模組，也可以修改組態設定，以便從清單中移除特定匯出格式。 此外，您也可以在報表伺服器上指定組態設定，以便控制可用的格式。 您可以透過加入並修改該轉譯延伸模組的組態設定，修改特定格式的預設行為。  
  
### <a name="print-action-on-the-report-toolbar"></a>報表工具列上的列印動作  
 **列印**上**動作** 功能表是透過提供自訂列印功能[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。 當您按一下 **列印**，ActiveX 用戶端列印控制項就會下載到用戶端電腦。 在大部分情況下，使用者按下的使用者**列印**必須在本機電腦上具有系統管理員權限。 常見的作法是將 ActiveX 控制項下載限制為僅擁有「管理員」權限的使用者。 您可以使用 SharePoint 管理中心來啟用或停用用戶端列印控制項下載。  
  
### <a name="find-action-on-the-report-toolbar"></a>報表工具列上的尋找動作  
 **尋找**上**動作**功能表可用來將移至報表中的目標位置。 您可以輸入您要尋找的單字或片語來搜尋報表的內容。 搜尋詞彙的最大值為 256 個字元。 當您的搜尋在報表中找到相符的值時，焦點就會移到報表中，包含該值的部分。  
  
 輸入要搜尋的值時，請輸入您預期會顯示在報表中的值。 除非您預期句子中的每個字都會出現在報表中，否則請勿提出疑問句 (例如，「本月份的平均收益有多少」)。  
  
 您一次只能搜尋一個詞彙或值， 您不能使用搜尋運算子 (例如 `AND` 或 `OR`)，或是符號和萬用字元， 也不能執行資料的交叉搜尋 (例如，搜尋特定產品在特定月份的淨銷售額)。 如需該分析類型，請使用報表產生器來建立點選連結報表。  
  
 限制存取報表資料的資料庫和模型安全性設定會套用至搜尋作業。 如果您要在使用模型做為資料來源的點選連結報表中搜尋某個值，而您無法存取該模型部分，則搜尋作業將會排除該模型部分所代表的資料。  
  
### <a name="panes-for-specifying-credentials-and-parameters"></a>指定認證與參數的窗格  
 **認證**並**參數**會出現在檢視區域旁的窗格。 **認證**報表的資料來源連接設定為提示使用者輸入的帳戶和密碼具有權限可存取資料來源時，會出現。 **參數**報表接受報表中定義參數的使用者輸入時，會出現。  
  
### <a name="setting-properties-on-the-report-viewer-web-part"></a>設定報表檢視器 Web 組件上的屬性  
 Web 組件上的屬性包括報表檢視器特定的自訂屬性，以及您可以為任何 Web 組件設定的一般屬性。 如需詳細資訊，請參閱 [自訂報表檢視器網頁組件](../../2014/reporting-services/customize-the-report-viewer-web-part.md)。  
  
 根據預設，報表會以整頁模式開啟。 整頁模式會顯示提供頁面導覽、搜尋及其他功能的工具列。 您可以自訂網頁組件，以便變更外觀或預設行為。  
  
## <a name="see-also"></a>另請參閱  
 [安裝或解除安裝 Reporting Services 增益集，適用於 SharePoint &#40;SharePoint 2010 和 SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [將報表檢視器網頁組件加入至網頁 &#40;SharePoint 整合模式的 Reporting Services&#41;](report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
  
