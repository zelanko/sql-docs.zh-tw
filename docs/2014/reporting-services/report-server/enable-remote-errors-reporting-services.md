---
title: 啟用遠端錯誤 (Reporting Services) | Microsoft Docs
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
- remote data source [Reporting Services]
- EnableRemoteError server property
ms.assetid: 5f05022b-d557-43e0-b50a-f5e2a1846b83
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 14586062cadbdf08646ff7a6080b2849d2900d7d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133619"
---
# <a name="enable-remote-errors-reporting-services"></a>啟用遠端錯誤 (Reporting Services)
  您可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器上設定伺服器屬性，以便傳回有關遠端伺服器上發生之錯誤狀況的其他資訊。 如果錯誤訊息包含「如需有關此錯誤的詳細資料，請導覽至本機伺服器電腦上的報表伺服器，或啟用遠端錯誤」這段文字，您可以設定 `EnableRemoteErrors` 屬性來存取可幫助您排解疑難問題的其他資訊。 如需詳細資訊，請參閱[報表伺服器系統屬性](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
 **本主題內容：**  
  
-   [啟用 SharePoint 模式的遠端錯誤](#bkmk_sharepoint)  
  
-   [透過 SQL Server Management Studio 啟用遠端錯誤 (原生模式)](#bkmk_mgtStudio)  
  
-   [透過指令碼啟用遠端錯誤 (原生模式)](#bkmk_script)  
  
-   [修改 ConfigurationInfo 資料表 (原生模式)](#bkmk_ConfigurationInfo)  
  
##  <a name="bkmk_sharepoint"></a> 啟用 SharePoint 模式的遠端錯誤  
 您可以透過兩種不同的程序啟用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式的遠端錯誤。 兩種不同的報表伺服器架構會採用不同的程序。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本中導入的較新 SharePoint 服務架構會使用可針對每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式進行的設定。 較舊的架構則使用單一網站層級設定。  
  
#### <a name="enable-remote-errors-for-a-reporting-services-service-application"></a>啟用 Reporting Services 服務應用程式的遠端錯誤  
  
1.  針對隨 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或較新版本 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]一併安裝的 SharePoint 模式報表伺服器，請啟用服務應用程式設定 **[啟用遠端錯誤]**。 此設定可針對每個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式設定。  
  
2.  在 [SharePoint 管理中心] 的 **[應用程式管理]** 群組中，按一下 **[管理服務應用程式]** 。  
  
3.  尋找您的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，然後按一下服務應用程式的名稱。  
  
4.  按一下 **[系統設定]**。  
  
5.  按一下 **[安全性]** 區段中的 **[啟用遠端錯誤]** 。  
  
6.  按一下 [確定] 。  
  
#### <a name="enable-remote-errors-for-a-sharepoint-site"></a>啟用 SharePoint 網站的遠端錯誤  
  
1.  針對隨 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之前的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]版本一併安裝的 SharePoint 模式報表伺服器，請啟用網站設定 **[在本機模式中啟用遠端錯誤]**。  
  
2.  在 **[網站動作]** 中，按一下您要修改之網站的 **[網站設定]** 。  
  
3.  按一下 **[Reporting Services]** 群組中的 **[Reporting Services 網站設定]** 。  
  
4.  按一下 **[在本機模式中啟用遠端錯誤]**。  
  
5.  按一下 **[確定]**。  
  
##  <a name="bkmk_mgtStudio"></a> 透過 SQL Server Management Studio 啟用遠端錯誤 (原生模式)  
  
1.  啟動 Management Studio，然後連接到報表伺服器執行個體。 如需詳細資訊，請參閱[連接到 Management Studio 中的報表伺服器](../tools/connect-to-a-report-server-in-management-studio.md)中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]線上叢書 》。  
  
2.  以滑鼠右鍵按一下報表伺服器節點，然後選取 [屬性]。  
  
3.  按一下 **[進階]** ，即可開啟屬性頁面。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的[伺服器屬性 &#40;進階頁面&#41; - Reporting Services](../tools/server-properties-advanced-page-reporting-services.md)。  
  
4.  在`EnableRemoteErrors`，選取`True`。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="bkmk_script"></a> 透過指令碼啟用遠端錯誤 (原生模式)  
  
1.  建立一個文字檔案，然後將下列指令碼複製到這個檔案中。  
  
    ```  
    Public Sub Main()  
      Dim P As New [Property]()  
      P.Name = "EnableRemoteErrors"  
      P.Value = True  
      Dim Properties(0) As [Property]  
      Properties(0) = P  
      Try  
        rs.SetSystemProperties(Properties)  
        Console.WriteLine("Remote errors enabled.")  
      Catch SE As SoapException  
        Console.WriteLine(SE.Detail.OuterXml)  
      End Try  
    End Sub  
    ```  
  
2.  請這個檔案儲存為 EnableRemoteErrors.rss。  
  
3.  按一下 **[開始]**，然後指向 **[執行]**，再輸入 **cmd**，並按一下 **[確定]** ，開啟命令提示字元視窗。  
  
4.  瀏覽至包含您剛剛建立之 .rss 檔案的目錄。  
  
5.  輸入下列命令列，以伺服器的實際名稱來取代 *servername* 。  
  
    ```  
    rs -i EnableRemoteErrors.rss -s http://servername/ReportServer  
    ```  
  
6.  如需詳細資訊，請參閱 [RS.exe 公用程式 &#40;SSRS&#41;](../tools/rs-exe-utility-ssrs.md)  
  
##  <a name="bkmk_ConfigurationInfo"></a> 修改 ConfigurationInfo 資料表 (原生模式)  
  
1.  > [!NOTE]  
    >  您可以編輯**ConfigurationInfo**設定報表伺服器資料庫中的資料表`EnableRemoteErrors`至`True`，但是如果目前正在使用報表伺服器，您應該使用 SQL Server Management Studio 或指令碼修改的設定。 如果您修改資料庫中的設定，則須先重新啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務，變更才會生效。  
  
  