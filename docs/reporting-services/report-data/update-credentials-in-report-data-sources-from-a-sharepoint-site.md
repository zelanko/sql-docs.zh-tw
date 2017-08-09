---
title: "更新報表資料來源，從 SharePoint 網站中的認證 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85652be59a369ff3b571f8858a744962b5b3f619
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>從 SharePoint 網站更新報表資料來源的認證
  本主題描述如何更新內嵌於報表內的資料來源，以及儲存在 SharePoint 文件庫中的共用資料來源。  
  
 許多報表可能包含資料來源或使用設定為使用 Windows 驗證的共用資料來源。 在某些情況下 (例如在儲存到 SharePoint 文件庫的報表上建立資料警示)，您需要將資料來源認證更新至預存認證或是不需要認證。  
  
 為了使用報表中的預存認證，您可能會決定建立並使用新的 SQL Server 登入。 如需詳細資訊，請參閱 [建立登入](../../relational-databases/security/authentication-access/create-a-login.md)。  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>更新內嵌資料來源以使用預存認證  
  
1.  移至儲存報表所在的 SharePoint 文件庫。  
  
2.  按一下報表上用來展開下拉式功能表的圖示，然後按一下 [管理資料來源]。  
  
     [管理資料來源] 頁面隨即開啟。  
  
3.  在 [名稱] 資料行中，按一下資料來源。  
  
4.  確認已針對 [連接類型] 選取 [自訂資料來源] 選項。  
  
     這個選項表示資料來源內嵌於報表中。  
  
5.  除非您要將報表連接到其他類型的資料來源、其他伺服器或資料存放區，否則讓 [資料來源類型] 和 [連接字串] 選項保持不變。  
  
6.  針對 [認證] 選取 [預存認證]。 只有在資料來源未接受認證，或是使用一些其他方式傳送認證時，這個選項才有用。  
  
     在某些情況下也可以使用 [不需要認證] 選項。  
  
     針對某些資料來源類型，必須在報表伺服器上設定自動執行帳戶。 如需詳細資訊，請參閱[從外部資料來源加入資料 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) 和[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) 中對應資料來源類型的主題。  
  
7.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，會將它指定格式如下：\<網域 >\\< 帳戶\>，然後選取**當做 Windows 認證連接到資料來源時使用**。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 **[連接到資料來源時做為 Windows 認證]**。 如果資料庫伺服器支援模擬或委派，您可以選取 **[設定執行內容到這個帳戶]**。  
  
8.  若要驗證資料來源能夠使用更新的認證連接，請按一下 [測試連接]。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>更新共用資料來源以使用預存認證  
  
1.  移至儲存共用資料來源所在的 SharePoint 文件庫。  
  
2.  按一下共用資料來源上用來展開下拉式功能表的圖示，然後按一下 [編輯資料來源定義]。  
  
     [資料來源] 頁面隨即開啟。  
  
3.  除非您要將共用資料來源連接到其他類型的資料來源、其他伺服器或資料存放區，否則讓 [資料來源類型] 和 [連接字串] 選項保持不變。  
  
4.  針對 [認證] 選取 [預存認證]。  
  
     在某些情況下也可以使用 [不需要認證] 選項。 只有在資料來源未接受認證，或是使用一些其他方式傳送認證時，這個選項才有用。  
  
     針對某些資料來源類型，必須在報表伺服器上設定自動執行帳戶。 如需詳細資訊，請參閱[從外部資料來源加入資料 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) 和[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) 中對應資料來源類型的主題。  
  
5.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，會將它指定格式如下：\<網域 >\\< 帳戶\>，然後選取**當做 Windows 認證連接到資料來源時使用。**  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 **[連接到資料來源時做為 Windows 認證]**。 如果資料庫伺服器支援模擬或委派，您可以選取 **[設定執行內容到這個帳戶]**。  
  
6.  若要驗證資料來源能夠使用更新的認證連接，請使用 [測試連接]。  
  
7.  驗證是否已選取 [啟用此資料來源]。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>請參閱＜  
 [將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  
