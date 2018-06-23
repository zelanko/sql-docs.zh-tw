---
title: 將報表發行至 SharePoint 文件庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: d19618eaa7997444e661ca9213a72f75bf1b3910
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034308"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>將報表發行到 SharePoint 文件庫
  若要將報表發行至有設定 SharePoint 整合的 SharePoint 網站，您必須在報表設計師中設定專案屬性。 在專案屬性中，伺服器、報表和共用資料來源的所有參考都必須是完整 URL。 在報表定義中，子報表、鑽研報表和資源 (如網路架構影像) 的所有參考都必須是完整 URLS。  
  
 您在 SharePoint 網站上必須具有「 **成員** 」或「 **擁有者** 」權限才能設定專案的屬性。 如需詳細資訊，請參閱 [SharePoint 模式在報表伺服器上已發行報表項目的 URL 範例 &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)。  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>將報表發行至 SharePoint 網站  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟現有或新的報表伺服器專案。  
  
2.  在 **[專案]** 功能表按一下 **[屬性]**。 [*\<專案>***屬性頁**] 對話方塊隨即開啟。  
  
3.  在 **[組態]** 清單中，選取用來建立及發行報表的方案組建組態的名稱。 目前的設定列為 [使用中](\<設定>)。  
  
4.  如果您想要發行專案中的共用資料來源，並覆寫之前發行的共用資料來源，請將 **OverwriteDataSources** 設定為 **True**。  
  
5.  （選擇性）如**TargetDataSourceFolder**，輸入指向 SharePoint 文件庫或文件庫資料夾的 URL (例如， *http://TestServer/TestSite/Documents/DataSources)*。  
  
     如果您未指定值，則會使用 **TargetReportFolder** 值。  
  
6.  如**TargetReportFolder**，輸入文件庫或文件庫資料夾的 URL (例如， *http://TestServer/TestSite/Documents/Reports)*。  
  
7.  為 **TargetServerURL**輸入 SharePoint 頂層網站或子網站的 URL。 如果您未指定站台，會使用預設的頂層站台 (例如， *http://servername*， *http://servername/site*，或*http://servername/site/subsite*)。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. 在方案總管中，以滑鼠右鍵按一下要發行的報表，然後按一下 [部署]。 報表便會發行至 **[TargetReportFolder]** 中所指定的位置。 此時，部署錯誤會出現在 [輸出] 視窗中。  
  
## <a name="see-also"></a>另請參閱  
 [專案屬性頁對話方塊](../tools/project-property-pages-dialog-box.md)   
 [設定部署屬性&#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [將報表發行至報表伺服器](publishing-reports-to-a-report-server.md)   
 [SharePoint 模式中報表伺服器上已發行報表項目的 URL 範例 &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [使用 Office 資料連線&#40;.odc&#41;報表&#40;的 Reporting Services SharePoint 整合模式&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  