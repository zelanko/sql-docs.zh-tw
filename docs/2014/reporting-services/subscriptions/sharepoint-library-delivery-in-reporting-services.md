---
title: Reporting Services 中的 SharePoint 文件庫傳遞 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], report delivery
- delivering reports [Reporting Services]
- subscriptions [Reporting Services], SharePoint library delivery
ms.assetid: cb4e4f71-f2d5-475a-9284-ea324c93c7de
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cf32579a40b3290e0126b3a1a92665643ae8c3cf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264194"
---
# <a name="sharepoint-library-delivery-in-reporting-services"></a>Reporting Services 中的 SharePoint 文件庫傳遞
  針對 SharePoint 整合所設定的報表伺服器包含您可以用來將報表傳送至 SharePoint 文件庫的傳遞延伸模組。  
  
 若要使用 SharePoint 傳遞延伸模組，您必須從 SharePoint 網站上的應用程式頁面建立訂閱，然後選取 [SharePoint 文件庫] 作為傳遞類型。 您無法針對您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或報表管理員中建立的訂閱，使用 SharePoint 傳遞延伸模組。  
  
> [!NOTE]  
>  如果報表伺服器以原生模式執行，傳遞延伸模組不支援將報表傳遞至 SharePoint 網站。 如果您嘗試以程式設計的方式呼叫原生模式報表伺服器的傳遞延伸模組，伺服器將會傳回 `rsDeliveryExtensionNotFound` 錯誤，並在報表伺服器的記錄檔中記錄 `rsOperationNotSupportedSharePointMode` 錯誤。  
  
## <a name="requirements"></a>需求  
 將已轉譯報表傳遞至文件庫的需求包括：  
  
-   報表伺服器必須針對 SharePoint 整合模式設定。  
  
-   報表伺服器必須已經安裝並設定 SharePoint 傳遞延伸模組。  
  
-   報表必須是報表定義 (.rdl) 檔。 您無法透過訂閱來傳遞其他報表伺服器內容類型，如模型或資源。 您無法訂閱使用模型當做資料來源的特定報表。  
  
-   報表必須使用預存認證。 這是在報表上建立任何訂閱 (不管傳遞類型為何) 的必要條件。  
  
-   目的地必須是 SharePoint 文件庫。 選擇目標文件庫時，您必須選擇位於相同 SharePoint 網站上的文件庫。 您無法將報表傳遞至相同網站集合中，另一部伺服器或另一個網站上的文件庫。  
  
 報表傳遞時，不包含屬性與中繼資料。 首次傳遞報表時，此報表會繼承包含它之資料庫或清單的安全性設定。 如果您之後修改安全性設定或設定報表屬性，就會保留這些設定。 訂閱僅會重新整理儲存在指定位置的報表。  
  
## <a name="sharepoint-permissions"></a>SharePoint 權限  
 若要建立訂閱，您必須在報表上擁有「檢視項目」權限。 若要傳遞報表，您必須在報表要傳遞至其中的文件庫上擁有「新增項目」權限。  
  
## <a name="how-to-create-modify-and-delete-subscriptions"></a>如何建立、修改和刪除訂閱  
  
1.  移至您要存取報表的來源 SharePoint 網站。  
  
2.  選取報表、按一下報表旁的向下箭號，然後選取 [管理訂閱]。  
  
3.  按一下 [建立]、[編輯] 或 [刪除]。  
  
 [管理訂閱] 清單中的 [狀態] 訊息便會顯示關於訂閱的最新資訊，包括是否成功以及訂閱上次執行的日期和時間。  
  
## <a name="setting-delivery-options"></a>設定傳遞選項  
 您可以在將報表傳遞至 SharePoint 文件庫的訂閱上，設定下列傳遞選項。  
  
 轉譯輸出格式  
 指定您要用來傳遞報表的應用程式格式。 報表在傳遞之前，會以這個格式轉譯。 您選取的輸出格式將會決定預設的副檔名。  
  
 您可以從其中選取輸出格式的清單是安裝在報表伺服器上的轉譯延伸模組集。  
  
 請注意，您無法指定僅用於內部使用的輸出格式，或是以 SharePoint 整合模式執行之報表伺服器不支援的輸出格式。 這些格式包括 Null、RGDI 和 HTMLOWC。  
  
 檔案名稱與副檔名  
 將報表的檔案名稱與副檔名指定為您要顯示在目標文件庫中的檔案名稱與副檔名。 如果您沒有指定副檔名，報表伺服器會依據報表輸出格式來建立副檔名。 這是必要的值。 檔案名稱不得包含下列字元：: \ / * ? 「 \< > |# { } %  
  
 Title  
 指定選擇性`Title`目標文件庫中報表的屬性。 這是儲存在文件庫中之所有項目的標準屬性。 使用者可以在檢視 SharePoint 網站上的文件庫內容時，指定要顯示或隱藏此屬性。  
  
 路徑  
 指定指向 SharePoint 文件庫的完整 URL，包括 SharePoint Web 應用程式和網站。 例如： http://mySharePointWeb/MySite/MyDocLib; 其中 「http://mySharePointWeb"指出的 Web 應用程式中，"MySite"是 SharePoint 網站，以及"MyDocLib"是 SharePoint 文件庫傳遞報表。  
  
 您無法指定頁面、網站或清單。 目標容器必須是相同網站或伺服陣列中的文件庫。  
  
 覆寫選項  
 指定在處理訂閱時，具有相同名稱與副檔名的檔案是否要由較新的版本取代。 如果您要以較新的版本取代現有的檔案，選擇 [覆寫]。 如果您不要訂閱取代檔案，選擇 [無]。 在此情況下，如果有具有目標名稱與副檔名的檔案存在，則傳遞不會發生。 如果您要在檔案名稱結尾附加一個數字，藉此新增相同檔案的連續版本，選擇 [自動遞增]。  
  
 自動複製  
 如果您要使用 [自動複製] 功能，將檔案的最新版本自動複製到多個位置，當啟用 [覆寫] 時，就會複製該檔案。 如果您使用**Autoincrement**或是**無**，傳遞將會失敗而`rsDeliveryError`就會發生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [建立和管理 SharePoint 模式報表伺服器的訂用帳戶](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [訂閱與傳遞&#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [指定報表資料來源的認證及連線資訊](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
