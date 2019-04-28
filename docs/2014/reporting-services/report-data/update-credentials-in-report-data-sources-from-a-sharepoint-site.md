---
title: 從 SharePoint 網站更新報表資料來源的認證 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f46c31e3590098e3b58bb02e802991f686f2d568
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735821"
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
  
4.  確認已針對 [連線類型] 選取 [自訂資料來源] 選項。  
  
     這個選項表示資料來源內嵌於報表中。  
  
5.  除非您要將報表連接到其他類型的資料來源、其他伺服器或資料存放區，否則讓 [資料來源類型] 和 [連接字串] 選項保持不變。  
  
6.  針對 [認證] 選取 [預存認證]。 只有在資料來源未接受認證，或是使用一些其他方式傳送認證時，這個選項才有用。  
  
     在某些情況下也可以使用 [不需要認證] 選項。  
  
     針對某些資料來源類型，必須在報表伺服器上設定自動執行帳戶。 如需詳細資訊，請參閱[從外部資料來源新增資料 &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md) 和[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) 中對應資料來源類型的主題。  
  
7.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，請使用下列格式來指定它：\<網域>\\<帳戶\>，然後選取 [連線到資料來源時作為 Windows 認證]。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 **[連接到資料來源時做為 Windows 認證]**。 如果資料庫伺服器支援模擬或委派，您可以選取 **[設定執行內容到這個帳戶]**。  
  
8.  若要驗證資料來源能夠使用更新的認證連接，請按一下 [測試連線]。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>更新共用資料來源以使用預存認證  
  
1.  移至儲存共用資料來源所在的 SharePoint 文件庫。  
  
2.  按一下共用資料來源上用來展開下拉式功能表的圖示，然後按一下 [編輯資料來源定義]。  
  
     [資料來源] 頁面隨即開啟。  
  
3.  除非您要將共用資料來源連線到其他類型的資料來源、其他伺服器或資料存放區，否則讓 [資料來源類型] 和 [連接字串] 選項保持不變。  
  
4.  針對 [認證] 選取 [預存認證]。  
  
     在某些情況下也可以使用 [不需要認證] 選項。 只有在資料來源未接受認證，或是使用一些其他方式傳送認證時，這個選項才有用。  
  
     針對某些資料來源類型，必須在報表伺服器上設定自動執行帳戶。 如需詳細資訊，請參閱[從外部資料來源新增資料 &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md) 和[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) 中對應資料來源類型的主題。  
  
5.  輸入使用者名稱和密碼。  
  
    -   如果帳戶是 Windows 網域使用者帳戶，請使用下列格式來指定它：\<網域>\\<帳戶\>，然後選取 [連線到資料來源時作為 Windows 認證]。  
  
    -   如果使用者名稱和密碼是資料庫認證，請勿選取 **[連接到資料來源時做為 Windows 認證]**。 如果資料庫伺服器支援模擬或委派，您可以選取 **[設定執行內容到這個帳戶]**。  
  
6.  若要驗證資料來源能夠使用更新的認證連線，請使用 [測試連接]。  
  
7.  驗證是否已選取 [啟用此資料來源]。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  
