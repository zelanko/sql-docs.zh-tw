---
title: 將共用資料來源發行至 SharePoint 文件庫 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 68c556abb719ba9642e7c1074866235e46c1f1e3
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50029117"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>將共用資料來源發行至 SharePoint 文件庫
  若要將共用資料來源發行到以 SharePoint 整合模式執行的報表伺服器，您必須在報表設計師中設定報表專案屬性。 在專案屬性中，伺服器、報表和共用資料來源的所有參考都必須是完整 URL。  
  
 您必須擁有 SharePoint 網站的**成員**或**擁有者**權限。 如需詳細資訊，請參閱 [SharePoint 模式在報表伺服器上已發行報表項目的 URL 範例 &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)。  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>將共用資料來源發行到 SharePoint 網站  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟現有或新的報表伺服器專案。  
  
2.  按一下 [專案] 功能表上的 [屬性]。 [*\<專案>***屬性頁**] 對話方塊隨即開啟。  
  
3.  選擇您用來發行至 SharePoint 網站的 [組態]。  
  
4.  如果您想要發行專案中的共用資料來源，並覆寫之前發行的共用資料來源，請將 **OverwriteDataSources** 設定為 **True**。  
  
5.  (選擇性) 為 **TargetDataSourceFolder**輸入 SharePoint 文件庫或文件庫資料夾的 URL。 例如， `http://TestServer/TestSite/Documents/DataSources`。  
  
     如果您未指定值，則會使用 **TargetReportFolder** 值。  
  
6.  為 **TargetReportFolder**輸入文件庫或文件庫資料夾的 URL。 例如， `http://TestServer/TestSite/Documents/Reports`。  
  
7.  為 **TargetServerURL**輸入 SharePoint 頂層網站或子網站的 URL。 若未指定網站，則會使用預設的最上層網站。 例如，`http://servername`、`http://servername/site` 或 `http://servername/site/subsite`。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. 在方案總管中，以滑鼠右鍵按一下您要發行的共用資料來源，然後按一下 [部署]。 資料來源便會發行到 **TargetDataSourceFolder**中指定的位置。 此時，部署錯誤會出現在 [輸出] 視窗中。  
  
    > [!NOTE]  
    >  當您將共用資料來源發行到 SharePoint 網站時，副檔名會變更為 .rsds。 您可以直接在 SharePoint 網站上編輯及管理共用資料來源。 如需詳細資訊，請參閱[建立及管理共用資料來源 &#40;SharePoint 整合模式的 Reporting Services&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)。  
  
## <a name="see-also"></a>另請參閱  
 [將報表發行到 SharePoint 文件庫](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [SharePoint 模式在報表伺服器上已發行報表項目的 URL 範例 &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [專案屬性頁對話方塊](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [將報表發行至報表伺服器](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [搭配報表使用 Office 資料連接 &#40;.odc&#41; &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
