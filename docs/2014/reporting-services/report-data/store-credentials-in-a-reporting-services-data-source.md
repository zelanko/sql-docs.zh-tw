---
title: 在 Reporting Services 資料來源中儲存認證 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4c94a9cbcacfa2851066682e0fb0859e500b95dd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311318"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Store Credentials in a Reporting Services Data Source
  您可以設定預存認證，讓 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 報表伺服器用來存取報表的外部資料。 如果報表會自動執行，便是使用預存認證 (例如以電子郵件形式發行報表的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 訂閱)。 排定或觸發報表處理時，報表伺服器會擷取和使用認證。 本主題會逐步引導您完成為原生模式和 SharePoint 模式報表伺服器設定預存認證的程序。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
 **本主題內容：**  
  
-   [為報表特定的資料來源設定預存認證 (原生模式)](#bkmk_stored_credentials_data_source_native)  
  
-   [為報表特定的資料來源設定預存認證 (SharePoint 模式)](#bkmk_stored_credentials_data_source_sharepoint)  
  
-   [為共用資料來源設定預存認證 (原生模式)](#bkmk_stored_credentials_shared_data_source_native)  
  
-   [為共用資料來源設定預存認證 (SharePoint 模式)](#bkmk_stored_credentials_shared_data_source_sharepoint)  
  
##  <a name="bkmk_top"></a> 預存認證的安全性原則需求  
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") 您必須在報表伺服器上，為預存認證所使用的帳戶設定下列其中一項安全性原則。 建議您為您的環境選取具備需要的最低層級權限的原則。  
  
1.  **允許本機登入**。 如需詳細資訊，請參閱 [允許本機登入](http://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx)。  
  
2.  **以批次工作登入**。 如需詳細資訊，請參閱 [以批次工作登入](http://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx)。  
  
3.  如需原則的一般資訊，請參閱 [編輯群組原則物件的安全性設定](http://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx)。  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> 為報表特定的資料來源設定預存認證 (原生模式)  
  
1.  在原生模式報表管理員中，瀏覽至包含報表的資料夾。 按一下項目操作功能表 ![報表管理員中適用於 SSRS 項目的操作功能表](../media/ssrs-report-manager-item-context-menu.png "報表管理員中適用於 SSRS 項目的操作功能表")。  
  
2.  按一下 [管理]  ，然後按一下 [資料來源] 。  
  
3.  選取 **[自訂資料來源]**。  
  
4.  在 [資料來源類型]  清單中，選取用來處理資料來源中之資料的資料處理延伸模組。  
  
5.  針對 **[連接字串]**，請指定報表伺服器用於連接到資料來源的連接字串。 下列範例說明用來連接的連接字串[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]資料庫：  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  針對 [連接方式] ，選取 [安全地儲存在報表伺服器中的認證] 。  
  
7.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，請使用下列格式來指定它：\<網域>\\<帳戶\>，然後選取 [連線到資料來源時作為 Windows 認證]。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 **[連接到資料來源時做為 Windows 認證]**。 如果資料庫伺服器支援模擬或委派，您就可以選取 **[連接到資料來源後，模擬已驗證的使用者]**。  
  
8.  按一下 **[套用]**。  
  
     ![搭配回到頁首連結使用的箭頭圖示](../../2014-toc/media/uparrow16x16.gif "搭配回到頁首連結使用的箭頭圖示") [預存認證的安全性原則需求](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> 為報表特定的資料來源設定預存認證 (SharePoint 模式)  
  
1.  瀏覽至包含報表的文件庫，然後按一下開啟功能表 ![適用於 SSRS 項目的文件庫操作功能表](../media/ssrs-sharepoint-item-context-menu.png "適用於 SSRS 項目的文件庫操作功能表")。  
  
2.  按一下第二個開啟功能表 ![適用於 SSRS 項目的文件庫操作功能表](../media/ssrs-sharepoint-item-context-menu.png "適用於 SSRS 項目的文件庫操作功能表")，然後按一下 [管理資料來源]。  
  
3.  按一下您要設定預存認證的 [自訂]  資料來源的名稱。  
  
4.  在 [資料來源類型]  清單中，選取用來處理資料來源中之資料的資料處理延伸模組。  
  
5.  針對 **[連接字串]**，請指定報表伺服器用於連接到資料來源的連接字串。 下列範例說明用來連接的連接字串[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]資料庫：  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  針對 [認證] 選取 [預存認證] 。  
  
7.  輸入 [使用者名稱]  和 [密碼] 。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，請使用下列格式來指定它：\<網域>\\<帳戶\>，然後選取 [連線到資料來源時作為 Windows 認證]。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 [當做 Windows 認證使用] 。 如果資料庫伺服器支援模擬或委派，您可以選取 **[設定執行內容到這個帳戶]**。  
  
8.  按一下 **ok**。  
  
     ![搭配回到頁首連結使用的箭頭圖示](../../2014-toc/media/uparrow16x16.gif "搭配回到頁首連結使用的箭頭圖示") [預存認證的安全性原則需求](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> 為共用資料來源設定預存認證 (原生模式)  
  
1.  在原生模式報表管理員中，瀏覽至共用資料來源項目。 ![共用資料來源圖示](../media/hlp-16datasource.png "共用資料來源圖示")  
  
2.  按一下操作功能表 ![報表管理員中適用於 SSRS 項目的操作功能表](../media/ssrs-report-manager-item-context-menu.png "報表管理員中適用於 SSRS 項目的操作功能表")，然後按一下 [管理]。  
  
3.  在 [資料來源類型]  清單中，指定用來處理資料來源中之資料的資料處理延伸模組。  
  
4.  針對 **[連接字串]**，請指定報表伺服器用於連接到資料來源的連接字串。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議您不要在連接字串中指定認證。  
  
     下列範例說明用來連接到本機 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 資料庫的連接字串：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，請使用下列格式來指定它：\<網域>\\<帳戶\>，然後選取 [連線到資料來源時作為 Windows 認證]。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 **[連接到資料來源時做為 Windows 認證]**。 如果資料庫伺服器支援模擬或委派，您就可以選取 **[連接到資料來源後，模擬已驗證的使用者]**。  
  
6.  按一下 **[套用]**。  
  
     ![搭配回到頁首連結使用的箭頭圖示](../../2014-toc/media/uparrow16x16.gif "搭配回到頁首連結使用的箭頭圖示") [預存認證的安全性原則需求](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> 為共用資料來源設定預存認證 (SharePoint 模式)  
  
1.  在文件庫中，瀏覽至共用資料來源項目。![共用資料來源的圖示](../media/hlp-16datasource.png "共用資料來源的圖示")  
  
2.  按一下操作功能表 ![適用於 SSRS 項目的文件庫操作功能表](../media/ssrs-sharepoint-item-context-menu.png "適用於 SSRS 項目的文件庫操作功能表")，然後按一下第二個操作功能表 ![適用於 SSRS 項目的文件庫操作功能表](../media/ssrs-sharepoint-item-context-menu.png "適用於 SSRS 項目的文件庫操作功能表")。  
  
3.  按一下 [編輯資料來源定義] 。  
  
4.  在 [資料來源類型]  清單中，指定用來處理資料來源中之資料的資料處理延伸模組。  
  
5.  針對 **[連接字串]**，請指定報表伺服器用於連接到資料來源的連接字串。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建議您不要在連接字串中指定認證。  
  
     下列範例說明用來連接到本機 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] 資料庫的連接字串：  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，請使用下列格式來指定它：\<網域>\\<帳戶\>，然後選取 [當作 Windows 認證使用]。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 [當做 Windows 認證使用] 。 如果資料庫伺服器支援模擬或委派，您可以選取 [設定執行內容到這個帳戶] 。  
  
7.  按一下 **[確定]**。  
  
     ![搭配回到頁首連結使用的箭頭圖示](../../2014-toc/media/uparrow16x16.gif "搭配回到頁首連結使用的箭頭圖示") [預存認證的安全性原則需求](#bkmk_top)  
  
## <a name="see-also"></a>另請參閱  
 [指定報表資料來源的認證及連接資訊](../../integration-services/connection-manager/data-sources.md)   
 [設定報表的資料來源屬性 &#40;報表管理員&#41;](configure-data-source-properties-for-a-report-report-manager.md)   
 [建立、 刪除或修改共用的資料來源&#40;報表管理員&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [資料來源屬性頁面 &#40;報表管理員&#41;](../data-sources-properties-page-report-manager.md)   
 [新增資料來源頁面 &#40;報表管理員&#41;](../new-data-source-page-report-manager.md)  
  
  
