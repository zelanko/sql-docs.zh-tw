---
title: "使用資料摘要 (Power Pivot for SharePoint) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eb5bc547eead5e8dc2d765f56861dacbd8af64e6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="use-data-feeds-power-pivot-for-sharepoint"></a>使用資料摘要 (Power Pivot for SharePoint)
  資料摘要是從線上資料來源產生，並串流至目的地文件或應用程式的一個或多個資料流。 如果您使用的是 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel，資料摘要可以協助您從任意資料來源取得現有的公司或商務資料，送到 Excel 2010 活頁簿的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 視窗中。 將資料摘要匯入活頁簿之後，您可以在 SharePoint 伺服器上排程的任何資料重新整理作業中參考該摘要。  
  
 您使用資料摘要的方式，取決於您是使用支援 Atom 資料摘要之應用程式中的內建匯出功能，還是建立並使用自訂資料服務。 能夠發行並讀取 Atom XML 資料的應用程式提供完美的資料傳輸，隱藏資料摘要與資料服務的機制，讓使用者看不到。 對使用者來說，只是將資料從一個應用程式移到另一個。  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Microsoft SharePoint 2010 提供可用於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿的資料摘要。 您可以使用本主題中的資訊來了解如何從您已經擁有的報表與清單中存取資料摘要。  
  
 本主題包含下列幾節：  
  
 [必要條件](#prereq)  
  
 [從 SharePoint 清單建立資料摘要](#sharepointlist)  
  
 [從 Reporting Services 報表建立資料摘要](#rsreport)  
  
 [從資料服務文件建立資料摘要](#dsdoc)  
  
##  <a name="prereq"></a> 必要條件  
 您必須具有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel，才能將資料摘要匯入 Excel 2010。  
  
 您必須具有以 Atom 1.0 格式提供資料的 Web 服務或資料服務。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 SharePoint 2010 都可以用這種格式提供資料。  
  
 在您可以將 SharePoint 清單匯出為資料摘要之前，您必須在 SharePoint 伺服器上安裝 ADO.NET Data Services。 如需詳細資訊，請參閱 [安裝 ADO.NET Data Services 以支援 SharePoint 清單的資料摘要匯出](http://msdn.microsoft.com/en-us/f32527ae-f623-4e08-adfb-6d3262f5c2ac)。  
  
##  <a name="sharepointlist"></a> 從 SharePoint 清單建立資料摘要  
 在 SharePoint 2010 伺服陣列中，SharePoint 清單在清單功能區上有一個 [匯出為資料摘要] 按鈕。 您可以按一下此按鈕，將清單匯出為摘要。 為了取得最佳結果，您在工作站上應該有 Excel 2010 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 用戶端應用程式。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 用戶端應用程式將會啟動，以回應資料摘要匯出，建立包含清單的新 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料表。  
  
1.  開啟 SharePoint 網站上的清單。  
  
2.  在 [清單工具] 中，按一下 [清單]。  
  
3.  在 [連線及匯出] 中，按一下 [匯出為資料摘要]。  
  
    > [!NOTE]  
    >  [匯出為資料摘要] 按鈕會藉由 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 加入 SharePoint。 如果您沒有安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或您沒有啟動 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 功能，將無法使用此按鈕。  
  
4.  如果 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 安裝在本機上，按一下 [開啟]，或按一下 [儲存]，將 .atomsvc 文件儲存到硬碟，以供稍後的匯入作業使用。  
  
5.  如果您選擇 [開啟]，使用 [資料表匯入精靈] 將資料摘要匯入工作表中。 資料摘要將會當做新的資料表加入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 視窗。  
  
 如果 ADO.NET Data Services 3.5.1 未安裝在 SharePoint 伺服器上，則會發生錯誤。 如需錯誤及如何解決錯誤的詳細資訊，請參閱 [安裝 ADO.NET Data Services 以支援 SharePoint 清單的資料摘要匯出](http://msdn.microsoft.com/en-us/f32527ae-f623-4e08-adfb-6d3262f5c2ac)。  
  
##  <a name="rsreport"></a> 從 Reporting Services 報表建立資料摘要  
 如果您擁有 SQL Server 2008 R2 Reporting Services 的部署，您可以使用新的 Atom 轉譯延伸模組，從現有的報表中產生資料摘要。 為了取得最佳結果，您在工作站上應該有 Excel 2010 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 用戶端應用程式將會啟動，以回應資料摘要匯出，然後在進行串流時，自動加入資料表和資料行並使兩者相關。  
  
 如需如何從報表匯出資料摘要的指示，請參閱[報表產生器說明檔](http://go.microsoft.com/fwlink/?LinkId=154494)中的[從報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  若要設定週期性的資料重新整理排程，將報表資料重新匯入已發行至 SharePoint 文件庫的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿中，報表伺服器必須設定為與 SharePoint 整合。 如需一起使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 與 Reporting Services 的詳細資訊，請參閱[設定和管理報表伺服器 &#40;Reporting Services SharePoint 模式&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)。  
  
##  <a name="dsdoc"></a> 從資料服務文件建立資料摘要  
 如果您有可以產生 Atom 摘要的自訂資料服務，您可以設定資料服務文件，以便將資料提供給使用者和應用程式使用。 「資料服務文件」(.atomsvc) 檔案會指定一個或多個以 Atom 電傳格式發行資料之線上來源的連接。 資料服務文件可以在「資料摘要庫」中建立，這是一個特殊用途的文件庫，可以提供一般存取點來瀏覽已經發行到 SharePoint 伺服器的資料服務文件。 在資料摘要庫中擁有資料服務文件存取權限的資訊工作者可以參照文件的 SharePoint URL，將資料摘要匯入其活頁簿及應用程式。  
  
1.  開啟網站管理員所建立的資料摘要庫。 如需詳細資訊，請參閱[建立或自訂資料摘要庫 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md)。  
  
2.  在 [文件庫工具] 中，按一下 [文件]。  
  
3.  按一下 [新增文件]。  
  
4.  請提供檔案名稱和描述。  
  
5.  指定一個或多個提供摘要的 URL：  
  
    1.  [基底 URL] 是選擇性的。 如果資料服務文件提供多個摘要，則您應該指定它。 基底 URL 應該指定所有摘要通用的 URL 部分 (例如，伺服器名稱和網站)。 如果您要建立 Reporting Services 報表的資料服務文件，基底 URL 將是報表伺服器 URL 與報表。  
  
    2.  [Web 服務 URL] 是必要的。 沒有基底 URL，這個值必須包含`http://`或`https://`地址。 如果您有指定基底 URL，Web 服務 URL 就是基底 URL 後面的部分。 例如，如果完整的 URL 是`http://adventure-works/inventory/today.aspx`，基底 URL 將是`http://adventure-works/inventory`，和 Web 服務 URL 將是 /today.aspx。  
  
         Web 服務 URL 可以包含篩選或選取資料子集的參數。 提供摘要的應用程式或服務必須支援您在 URL 中指定的參數。  
  
6.  輸入 [資料表名稱]，每個摘要各使用一個資料表。 此為必要值。 資料表名稱是由取用資料摘要的用戶端應用程式所使用。 在 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中，資料表名稱用來命名 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 視窗中，將包含已匯入之資料的資料表。  
  
## <a name="see-also"></a>請參閱＜  
 [在管理中心為網站集合啟用 Power Pivot 功能整合](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [使用資料摘要庫共用資料摘要 &#40;Power Pivot for SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
